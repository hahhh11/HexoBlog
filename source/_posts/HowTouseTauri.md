---
title: tauri的使用探索
date: 2022-02-09 14:32:19
categories: 其他
---


## 什么是[tauri](https://tauri.studio/)
Tauri 是一个跨语言的通用系统，具有很高的组合性，允许工程师开发各种各样的应用。她使用 Rust 工具和在 Webview 中渲染HTML 相结合构建桌面应用。Tauri构建的应用可以用任意数量的 JS API / Rust API 组合，使 Webview 可以通过消息控制整个系统。
任何可以在网站上显示东西，都可以在 Tuari 中显示！
### 为什么使用tauri
够小

### 如何上手
#### mac环境配置
需要安装 gcc 和 xcode-selec和Rustc依次执行
``` bash
brew install gcc
xcode-select --install
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
#### Windows环境配置
点击跳转下载安装 [Visual Studio C++](https://visualstudio.microsoft.com/visual-cpp-build-tools/) 、 [WebView2](https://developer.microsoft.com/en-us/microsoft-edge/webview2/#download-section) 、Rustc（[64位下载](https://win.rustup.rs/x86_64)｜[32位下载](https://win.rustup.rs/i686)）

#### 公用环境配置（mac、Windows）
##### 1.修改host文件加速 github
#mac 打开访达，commnd+shift+g，输入/etc/hosts
#windows  打开文件夹访问 C:\Windows\System32\drivers\etc

在hosts的最后加上
140.82.112.3 github.com
199.232.69.194 github.global.ssl.fastly.net
##### 2.node环境（node 12以上）建议替换npm或者yarn的源（建议使用nrm、yrm 如下);
```bash
npm install -g nrm 
nrm test 
nrm use taobao

npm install -g yarn 
npm install -g yrm 
yrm test 
yrm use tabao


rustc --version //检查rust版本
cargo --version //检查cargo版本
```
修改cargo源 
mac版本 
##### 3.修改rust的Cargo源
先检查rust是否安装成功
```bash
rustc --version //检查rust版本
cargo --version //检查cargo版本
```
再打开.cargo文件夹下面的config文件,mac通过 vim $HOME/.cargo/config 进入

window通过安装的时候选择的目录可以进入直接编辑就可以了

全改成下面的字段如果没用这个文件直接创建就可以了。

[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"

#替换成你偏好的镜像源
replace-with = 'sjtu'

#清华大学
#[source.tuna]
#registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"

#中国科学技术大学
#[source.ustc]
#registry = "git://mirrors.ustc.edu.cn/crates.io-index"

#上海交通大学
[source.sjtu]
registry = "https://mirrors.sjtug.sjtu.edu.cn/git/crates.io-index"

#rustcc社区
#[source.rustcc]
#registry = "git://crates.rustcc.cn/crates.io-index"
##### 4.修改完毕安装tauri-bundler
```bash
cargo install tauri-bundler --force
```
#可能需要很长时间不要着急
#安装完毕过后执行
mac:source $HOME/.cargo/env或者重启命令行
windows:重启命令行
```bash
//结束后全局安装下
cargo install tauri-cli --version ^1.0.0-beta
```