---
title: 性能优化
date: 2022-02-16 11:57:39
tags: Canvas
---

[引用地址](https://g-next.antv.vision/zh/docs/guide/advanced-topics/performance-optimization)

### 方法一：减少 Draw Call

首先我们需要引入一个核心概念 Draw Call，以下介绍的优化方法大多围绕它展开。

#### 什么是 Draw Call

Draw Call就是CPU调用图形编程接口,比如DirectX或OpenGL,来命令GPU进行渲染的操作。
为啥 draw call 多了就会影响性能呢？因为在 CPU 和 GPU 进行异步协作的过程中，会向 command buffer 中提交需要 GPU 执行的命令，例如设置状态、绘制或者拷贝资源。CPU 准备这些命令的速度与 GPU 执行的速度存在不小差异，这就造成了性能瓶颈。

下图分别展示了每一帧中 CPU 和 GPU 的时间线，可以看出 GPU 总是在执行上一帧 CPU 提交的命令，与此同时 CPU 在准备下一帧的命令。当这些绘制命令数量不多时，两者协作没问题，但如果数量很多，GPU 在做完这一帧的渲染任务后就不得不等待，也就无法在 16ms 内完成了，这造成了卡顿的体感。
<img src="/images/drawcallprocess.png" />

#### 如何减少 Draw Call

因为以上原因，我们需要减少 Draw Call 的次数，能少画就少画，能不画就不画。

我们通常使用以下方法进行Draw Call的优化：

##### 剔除

在场景中的仅有一部分可见的情况下，我们通过剔除暂时不可见的元素，就能减少绘制命令的数量。
<img src="/images/drawcallmethod_img1.png" />

在判断一个图形是否在视口内时，我们通常会使用一种称作“包围盒”的结构。图形可以千变万化，但总可以找到一个包裹住它的最小基础几何结构，这个结构可以是“包围盒”，也可以是“包围球”，总之是为了后续计算元素与视口求交时方便。我们选择轴对齐包围盒。推广到 3D 场景中，视口也变成了视锥。
<img src="/images/drawcallmethod_img2.png" />

在每一帧都在 CPU 端进行这样的求交运算开销不小，特别当场景中图形数量较多时。另外在 3D 场景中视锥与包围盒（立方体）各个面的求交开销更大，因此我们也采用了一系列优化方法：

在 3D 场景进行视锥剔除时，我们尽量使用了如下[加速检测方法](https://github.com/antvis/GWebGPUEngine/issues/3)：

1. 基础相交测试 the basic intersection test
2. 平面一致性测试 the plane-coherency test
3. 八分测试 the octant test
4. 标记 masking
5. 平移旋转一致性测试 TR coherency test
更多可以参考：

- [Optimized View Frustum Culling Algorithms for Bounding Boxes](http://fileadmin.cs.lth.se/cs/Personal/Tomas_Akenine-Moller/pubs/vfcullbox.pdf.gz)
- [Efficient View Frustum Culling](http://old.cescg.org/CESCG-2002/DSykoraJJelinek/)
- [视锥体剔除 AABB 和 OBB 包围盒的优化方法](https://zhuanlan.zhihu.com/p/55915345)

##### 其他剔除手段：

在 WebGL / WebGPU 这样的渲染 API 中，还提供了其他剔除手段：

背面剔除，[gl.cullFace](https://developer.mozilla.org/zh-CN/docs/Web/API/WebGLRenderingContext/cullFace)
遮挡剔除，[gl.createQuery](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/createQuery)。至少需要 WebGL2

### 方法二：“脏矩形”渲染

有一种常见的交互是通过鼠标高亮某个图形。此时场景中仅有一小部分发生了改变，擦除画布中的全部图形再重绘就显得没有必要了。类比 React diff 算法能够找出真正变化的最小部分，“脏矩形”渲染能尽可能复用上一帧的渲染结果，仅绘制变更部分，特别适合 Canvas2D API。

#### 什么是“脏矩形”

脏矩形是2D图形性能优化一个重要的概念。

简单说脏矩形，就是画面刷新时，产生变化而需要重绘的舞台局部区域。

   什么叫脏，即什么情况下会弄脏？

   当我们的游戏中的元素 发生位置，大小，方向，动画，添加，删除等操作时，那么该元素原来对应的区域会弄脏，同时，新对应的区域也同样被弄脏。

使用脏矩形将大大减少无用的渲染工作量，降低额外性能消耗。

#### 实现“脏矩形”的思路

- 当鼠标悬停在圆上时，我们知道了对应的“脏矩形”，也就是这个圆的包围盒
- 找到场景中与这个包围盒区域相交的其他图形，这里找到了另一个矩形
- 使用 clearRect 清除这个“脏矩形”，代替清空整个画布
- 按照 z-index 依次绘制一个矩形和圆形
- 
<img src="/images/dirtyRect.png" />

在以上求交与区域查询的过程中，我们可以复用剔除方案中的优化手段，例如加速结构。

显然当动态变化的对象数目太多时，该优化手段就失去了意义，试想经过一番计算合并后的“脏矩形”几乎等于整个画布，那还不如直接清空重绘所有对象。因此例如 Pixi.js 这样的 2D 游戏渲染引擎就不考虑内置。

但在可视化这类相对静态的场景下就显得有意义了，例如在触发拾取后只更新图表的局部，其余部分保持不变。

### 方法三：批处理（batching）

以上两种方法当然有不适合的场景，例如希望总览一个大规模图场景的全貌时，无法应用剔除（所有节点/边都在视口内）。拖拽移动整个场景时，“脏矩阵”渲染效果也不佳（整个场景都变“脏”了）。

除了使用一些上层的 LOD 手段，例如缩放等级较高时，隐藏掉边和文本（因为也看不清），以此减少绘制命令数量之外，draw call batching 是非常合适的。

不同于 Canvas2D / Skia 提供的抽象层次较高的绘制 API，WebGL / WebGPU 提供了更低层次的 API，可以让我们将一批“同类”图形合并成一次绘制命令。在渲染引擎中，常用于渲染类似森林中大量树木这种场景。图场景同样十分契合，场景中包含大量同类但简单的图形（节点、边）。

### 离屏Canvas（Offscreen Canvas）

仅 g-webgl 下生效。

当主线程需要处理较重的交互时，我们可以将 Canvas 的渲染工作交给 Worker 完成，主线程仅负责同步结果。目前很多渲染引擎已经支持，例如 Babylon.js。

为了支持该特性，引擎本身并不需要做很多改造，只要能够保证 g-webgl 能在 Worker 中运行即可。

##### 局限性

由于运行在 Worker 环境，用户需要手动处理一些 DOM 相关的事件。
