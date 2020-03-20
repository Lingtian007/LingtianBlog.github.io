---
title: Node.js搭建本地服务模拟数据
date: 2019-10-18 14:32:09
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

# Node.js搭建本地服务模拟数据
---



## 1. 首先下载安装好Nodejs

`下载` : [Nodejs地址](http://nodejs.cn/download/)


## 2. 安装好了，打开cmd窗口，输入命令：npm -v 检验nodejs是否安装成功，如果出现以下界面则说明安装成功了

![](3.jpg)


## 3. 输入命令 npm install http-server -g（在全局安装本地服务器）

![](5.jpg)

## 4. 切换到你项目所在的路径

![](66.jpg)

## 5. 命令行输入http-server 即可在此文件夹下打开服务器

![](6.jpg)
域名和端口号是 127.0.0.1:8080、192.168.155.1:8080、192.168.1.122:8080

## 6. 在`项目`或者`桌面`下新建demo =>  data.json文件 
![](8.jpg)
![](10.jpg)
## 7. 打开浏览器，输入域名端口号（上面三个域名端口号都可以用）和文件名称
**http://127.0.0.1:8080/data.json**
![](12.jpg)

