---
title: React Native 搭建小白教程
date: 2019-05-06 12:32:09
top: false
cover: false
password:
toc: true
mathjax: false
summary: 闲来无事，随便写写。
tags:
  - 开发环境
categories:
  - 开发环境
---

<div align="middle">
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1347529350&auto=1&height=66"></iframe>
</div>

前言：因为电脑是 windows 系统，为了开始 React-Native 的入坑之路，只能硬着头皮上了，搭建环境的路上走了很多的坑，现在我把我成功搭建的路子记录下来，希望帮助大家少走弯路，也让我以后再搭建的时候，有个记忆，现在正式开始......

# windows 环境下搭建 React-Native 开发环境

---

# RN-搭建开发环境-官网

- [RN-搭建开发环境-官网](https://reactnative.cn/docs/getting-started.html):https://reactnative.cn/docs/getting-started.html

# 详细搭建过程

## 第一步：安装 Node

    Node  (>8.3)

安装完 Node 后建议设置 npm 镜像以加速后面的过程（或使用科学上网工具）。

    npm config set registry https://registry.npm.taobao.org --global
    npm config set disturl https://npm.taobao.org/dist --global

注意：不要使用 cnpm！cnpm 安装的模块路径比较奇怪，packager 不能正常识别！

## 第二步： 安装 yarn

Yarn 是 Facebook 提供的替代 npm 的工具，可以加速 node 模块的下载。安装 yarn 需要用 npm

    npm install -g yarn

安装完 yarn 后同理也要设置镜像源：

    yarn config set registry https://registry.npm.taobao.org --global
    yarn config set disturl https://npm.taobao.org/dist --global

安装完 yarn 之后就可以用 yarn 代替 npm 了，例如用 yarn 代替 npm install 命令，用 yarn add 代替 npm install.

## 第三步: React Native 命令行工具（react-native-cli）

React Native 的命令行工具用于执行创建、初始化、更新项目、运行打包服务（packager）等任务。

     npm install -g react-native-cli

## 第四步: Python2.x (不支持 3.x)

[Python 的官网下载地址](https://www.python.org/downloads/):https://www.python.org/downloads/

![](python.jpg)

## 第五步: JDK (==1.8 , 不支持更高版本)

[React Native 要求 JDK 的版本为 1.8，官网的下载地址](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html):https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

选择本系统合适的版本，即可，本人是 Windows x64 版本，即：

![](jdk.jpg)

安装好了之后，可以测试一下是否安装好 打开命令窗口终端（按住 windows+r ） 输入 java -version 回车 如果出现下图就安装成功了，如果不行，重启一下电脑再试
![](2.jpg)

## 第六步: 安装 Android 环境

[安装 Android 环境，首先先安装 Android Studio，下载地址](http://www.android-studio.org/index.php/download);http://www.android-studio.org/index.php/download

![](1.jpg)

下载下来的是一个可安装程序，点击安装即可，在点击“Next”过程，有一步需要指定 Android SDK 的路径，如果之前电脑中已经存在 SDK，可以指定该路径，后续就可以不用下载 SDK；由于本地没有安装过 SDK 的场景，这里暂时可以指定一个后续将保存 SDK 的路径。

点击“Finish”后，开始自动下载 SDK，此时根据网速的快慢，决定这个步骤的时间的长短，下载完成后，则会进行 Android Studio 的欢迎画面，如图

![](3.jpg)

### 配置环境变量（特别重要）

- 鼠标右键点击计算机，选择属性之后再按下图操作
  ![](5.jpg)

然后在编辑系统变量的这个框里面的变量值中操作以下步骤

1. 找到 Android SDK 的目录的路径复制添加到 path
   ![](6.jpg)
2. 找到 android sdk 中 platform-tools 文件的路径地址添加到 pah，记住一定要打分号哦，跟前一个路径区分开

    例如我的路径就是 F:\android-sdk_r24.4.1-windows\android-sdk-windows\platform-tools
    ![](7.jpg)

3. 找到`android sdk 中 tools`文件的路径地址添加到`pah` 最后点击确定 确定 确定 就完事了

然后打开命令终端 `（windows + r）` 输入 adb，测试一下，只要没有报错，就成功了

`我们再把java sdk配置了，按下图操作`

![](8.jpg)

我因为第一次搭建失败了，查了很久了，我添加了一个 Android sdk 的系统变量，第二次搭建就成功了，不知道是不是这个原因，最好添加一下吧，以防万一

![](9.jpg)

Android SDK 默认的应该是在 C:\Users\Administrator\AppData\Local\Android\Sdk

这个地方我也有一个疑问，为什么我的 android sdk 压缩包是解压在 F 盘里的，C 盘也会有一个 sdk，这个地方的配置`要用c盘的sdk`，记住了

## 第七步: 安装一个模拟器 我选择的是夜神模拟器

- 安装夜神模拟器，安装好之后，最好将分辨率调成`手机端`
  [夜神官网](https://www.yeshen.com/):https://www.yeshen.com/

## 第八步: 打开命令窗口，输入 react-native init firstdemo 创建项目名为`firstdemo`的文件夹

之后在 firstdemo 项目目录中找到 android 目录，创建一个文件，如下图

![](10.jpg)
然后内容为：`sdk.dir=android sdk`目录路径，如下图，记住，一定是`双斜杠`，

![](11.jpg)

## 第九步: 连接模拟器，运行项目

打开项目目录，按住 shift 键，鼠标右键点击，选择在此处打开命令窗口，输入 react-native start （启动项目服务进程），如下图

![](12.jpg)

接下来，刚刚的命令窗口别关闭了，重新打开一个命令窗口，连接夜神模拟器

### 9.1 打开夜神模拟器

### 9.2 重新打开一个命令窗口，执行命令 `adb connect 127.0.0.1:62001`以连接模拟器，（这个地方主义一下，端口号`62001`，是夜神模拟器默认的，如果你是其他的模拟器，记得查阅一下，默认端口号是多少）如下图：

![](13.jpg)

### 9.3 再执行命令 react-native run-android ,这里需要说明一下，第一次启动这个命令的话，他要下载一些依赖的东西，最好是要有 t z，不然会很慢，也可能会失败，这直接关系到最后能不能成功搭建环境，我这里是已经执行过一次这个命令了，如下图：

![](14.jpg)
![](15.jpg)

成功之后，你会看到你的模拟器自动打开了一个 app，但是整个页面都是红色的，想报错一样，别慌张，还有最后一步

![](16.jpg)
![](17.jpg)

输入电脑地址(`ipconfig => IPv4 地址`)+ 端口号`8081`:如图
![](21.jpg)

![](18.jpg)

最后再运行命令 react-native run-android 模拟器会出现 app 界面，

![](20.jpg)

好了，恭喜你，环境搭建好了，开始你的 RN 踩坑之路吧，
