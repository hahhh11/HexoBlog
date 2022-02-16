---
title: 什么是矩阵（Matrix）
author: 98Percent
date: 2021-07-21 13:47:06
tags: 深度学习
---

什么是矩阵？我们说向量是对一个数的拓展，代表一组数，那么矩阵就是对向量的拓展，它代表一组向量。
看待矩阵有两种视角——行向量和列向量
例如下图就是一个4*4的矩阵它有4行4列，当行数和列数相同时我们叫它——方阵

<img src="/images/whatismatrix/img1.png" />

计算机世界中我们通常使用一个二维数组来表示一个矩阵
### 矩阵的基本运算：

##### 1、矩阵的加法

和向量加法一样，矩阵的加法的结果就是矩阵中的每一项相加组成的一个新矩阵

<img src="/images/whatismatrix/img2.png" />

举个例子：

<img src="/images/whatismatrix/img3.png" />

当我们想知道所有学生上下学期每门科目的成绩总和时就只需要A+B就能得出我们想要的结果

##### 2、矩阵的数量乘法

和向量数量乘法一样，矩阵的数量乘法的结果就是用标量k去乘以向量中的每一个元素而组成的新矩阵

<img src="/images/whatismatrix/img4.png" />

使用之前的例子，如果我们希望知道所有学生上下学期每一门课程的平均分就只需要1/2*(A+B)就能得出我们想要的结果
使用另一个视角再举个例子：

<img src="/images/whatismatrix/img5.png" />

矩阵P是一个3*2的矩阵 其中第一个列向量里表示x轴的坐标，第二个列向量里表示y轴坐标，那么矩阵P这时候就表示一个三角形，对这个P做数量乘法就是对P里的每一个元素做数量乘法，相当于将这个三角行缩放了两倍。

### 矩阵遵循的基本性质：

<img src="/images/whatismatrix/img6.png" />

### 矩阵和向量相乘：

<img src="/images/whatismatrix/img7.png" />

<img src="/images/whatismatrix/img8.png" />

如上图，这是一个线性方程组，我们可以把它写成矩阵的形式，这是一个矩阵乘以一个向量等于一个向量的形式。

<img src="/images/whatismatrix/img9.png" />

我们可以得出矩阵和向量相乘，等于矩阵的每一行的每一个元素分别乘以这个向量的每个元素再相加

<img src="/images/whatismatrix/img10.png" />

我们可以把矩阵看作是向量的函数（很多小伙伴会说函数？这个我熟！）——f(向量a)=向量b，矩阵就是那个f()

### 矩阵和矩阵相乘：

<img src="/images/whatismatrix/img11.png" />

由矩阵和向量的乘法我们可以推出和矩阵的乘法其实就是把后面的矩阵看作是好多个向量，矩阵和矩阵的乘法其实就是前一个矩阵和后一个矩阵的每一列进行矩阵和向量的乘法计算，最后组成的新矩阵就是两个矩阵相乘的结果。

<img src="/images/whatismatrix/img12.png" />

我们有矩阵P代表红色的三角形，我们希望它的x轴方向扩大1.5倍，y轴方向扩大2倍，就可以使用矩阵的乘法得出一个新的矩阵，它代表的就是图中蓝色的三角形。

<img src="/images/whatismatrix/img13.png" />

矩阵和矩阵相乘时必须保证前一个矩阵的行数和后一个矩阵的列数相同，否则无法进行计算。
即Aab*Bbc=Cac（下标表示几行几列）
另外A*B不一定等于B*A，有的甚至交换位置不能相乘。

### 矩阵的转置：

更多时候我们更愿意把矩阵写成这样：

<img src="/images/whatismatrix/img14.png" />

但是这个矩阵是无法和

<img src="/images/whatismatrix/img15.png" />

相乘，这时候我们就需要使用矩阵的转置。

我们把这个P矩阵推倒

<img src="/images/whatismatrix/img16.png" />

把原矩阵的列变行，行变列，即

<img src="/images/whatismatrix/img17.png" />

这个时候就能进行矩阵的乘法了

### 矩阵转置的性质：

<img src="/images/whatismatrix/img18.png" />
