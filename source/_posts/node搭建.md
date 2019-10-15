---
title: 从0搭建自己的webpack开发环境
date: 2018-04-22 12:32:09
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
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=411214279&auto=1&height=66"></iframe>
</div>

闲来无事，随便写写......

# 从0搭建自己的webpack开发环境
---



**1.什么是Webpack?**
**webpack**是一个现代 **JavaScript** 应用程序的**静态模块打包器**(module bundler)，当 webpack 处理应用程序时，它会递归地构建一个**依赖关系图**(dependency graph)，其中包含应用程序需要的每个**模块**，然后将所有这些模块打包成一个或多个 **bundle**
![](node.jpg)

使用Webpack作为前端构建工具：

· 代码转换：TypeScript 编译成 JavaScript、SCSS 编译成 CSS 等；
· 文件优化：压缩 JavaScript、CSS、HTML 代码，压缩合并图片等；
· 代码分割：提取多个页面的公共代码、提取首屏不需要执行部分的代码让其异步加载；
· 模块合并：在采用模块化的项目里会有很多个模块和文件，需要构建功能把模块分类合并成一个文件；
· 自动刷新：监听本地源代码的变化，自动重新构建、刷新浏览器；
· 代码校验：在代码被提交到仓库前需要校验代码是否符合规范，以及单元测试是否通过；
· 自动发布：更新完代码后，自动构建出线上发布代码并传输给发布系统。

在**webpack**应用中有两个核心:

模块转换器，用于把模块原内容按照需求转换成新内容，可以加载非 JS 模块；

扩展插件，在 Webpack 构建流程中的特定时机注入扩展逻辑来改变构建结果或做你想要的事情。

**2.初始化项目**











