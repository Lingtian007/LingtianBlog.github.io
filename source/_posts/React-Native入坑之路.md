---
title: React-Native入坑之路 (一)
date: 2019-06-22 12:32:09
top: false
cover: false
password:
toc: true
mathjax: false
summary: 闲来无事，随便写写。
tags:
  - RN
categories:
  - RN
---

<div align="middle">
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=525454434&auto=1&height=66"></iframe>
</div>

闲来无事，随便写写......

# React-Native 入坑之路(一)

---

## 1. React-navigation 使用

 ###  1.导入依赖库

       npm install react-navigation --save

  然后在 package.json 文件中就可以看到，依赖库已经导入完毕：

       "react-native-tab-navigator": "^0.3.4",

### 2. 配置Navigator

+ 引入
![](1.jpg)

+ 使用
[React-navigation使用攻略](https://www.jianshu.com/p/f39f020197ef)

## 2. react-native-px2dp
+ 安装 
    npm install react-native-px2dp --save

+ 使用[React native 分辨率适配(px,dp)](https://www.jianshu.com/p/7836523b4d20)
      import px2dp from '../../util/px2dp'
      'use strict';

      import {Dimensions} from 'react-native'

      const deviceH = Dimensions.get('window').height
      const deviceW = Dimensions.get('window').width

      const basePx = 750

      export default function px2dp(px) {
          return px *  deviceW / basePx
      }

## 3. Dimensions 获取当前屏幕的宽高

    const { deviceWidth, deviceHeight } = Dimensions.get('window');

## 4. AsyncStorage 本都存储
[ReactNative之AsyncStorage本地存储](https://www.jianshu.com/p/abf4e19f245c):https://www.jianshu.com/p/abf4e19f245c

## 5. StatusBar的使用详解
[StatusBar的使用详解](https://www.jianshu.com/p/cff86e199c93):https://www.jianshu.com/p/cff86e199c93

## 6. ViewPagerAndroid
[官网](https://reactnative.cn/docs/next/viewpagerandroid.html)
[React-Native ViewPagerAndroid使用](https://www.jianshu.com/p/699a3b7da848)

## 7. React Native 高德地图组件的使用（react-native-amap3d）

[高德地图组件的使用](https://www.jianshu.com/p/fe90fc6a0308):https://www.jianshu.com/p/fe90fc6a0308

[高德地图组件react-native-amap3d](https://blog.csdn.net/IT_luntan/article/details/78982497)
