---
title: 提高工作效率的常用js函数汇总
date: 2018-01-22 12:32:09
top: false
cover: false
password:
toc: true
mathjax: false
summary: 闲来无事，随便写写。
tags:
- 随笔
categories:
- 随笔
---

<div align="middle">
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=407679465&auto=1&height=66"></iframe>
</div>

闲来无事，随便写写......

# 前言
本文总结了项目开发过程中常用的js函数和正则，意在提高大家平时的开发效率，具体内容如下：

1. 常用的正则校验
2. 常用的设备检测方式
3. 常用的日期时间函数
4. 跨端事件处理
5. js移动端适配方案
6. xss预防方式
7. 常用的js算法(防抖，截流，去重，排序，模板渲染，观察者...)
8. ......


## 代码 
  ### 1. 正则
      // 匹配邮箱
      let reg = /^([a-zA-Z]|[0-9])(\w|\-)+@[a-zA-Z0-9]+\.([a-zA-Z]{2,4})$

      // (新)匹配手机号
      let reg = /^1[0-9]{10}$/;

      // (旧)匹配手机号
      let reg = /^1(3|4|5|7|8)[0-9]{9}$/;

      // 匹配8-16位数字和字母密码的正则表达式
      let reg = /^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{8,16}$/;

      // 匹配国内电话号码 0510-4305211
      let reg = /\d{3}-\d{8}|\d{4}-\d{7}/;

      // 匹配身份证号码
      let reg=/(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/;

      // 匹配腾讯QQ号
      let reg = /[1-9][0-9]{4,}/;

      // 匹配ip地址
      let reg = /\d+\.\d+\.\d+\.\d+/;

      // 匹配中文
      let reg = /^[\u4e00-\u9fa5]*$/;

### 2.检测平台（设备）类型

      let isWechat = /micromessenger/i.test(navigator.userAgent),
      isWeibo = /weibo/i.test(navigator.userAgent),
      isQQ = /qq\//i.test(navigator.userAgent),
      isIOS = /(iphone|ipod|ipad|ios)/i.test(navigator.userAgent),
      isAndroid = /android/i.test(navigator.userAgent);

### 3. 常用的日期时间函数
      // 时间格式化
      function format_date(timeStamp) {
          let date = new Date(timeStamp);
          return date.getFullYear() + "年"
              + prefix_zero(date.getMonth() + 1) + "月"
              + prefix_zero(date.getDate()) + "日 "
              + prefix_zero(date.getHours()) + ":"
              + prefix_zero(date.getMinutes());
      }
      // moment.js方法

      //require 方式
      var moment=require('moment');
      //import 方式
      import moment from 'moment';

      格式化时间类型
      1.取当天时间，以YYYY年MM月DD日形式显示

      var now=moment().format("YYYY年MM月DD日");
      2.任意时间戳格式化，以YYYY-MM-DD HH:mm:ss形式显示

      var t1=moment(1411641720000).format('YYYY-MM-DD HH:mm:ss');
      获取前一天日期，格式以YYYY-MM-DD形式显示
      var t11=moment().day(0).format('YYYY-MM-DD');
      获取本周五日期，格式以YYYY-MM-DD形式显示
      var t12=moment().weekday(5).format('YYYY-MM-DD');
      获取上周五日期，格式以YYYY-MM-DD形式显示
      var t13=moment().weekday(-3).format('YYYY-MM-DD');
      可以简单理解为上周倒数第几天，上周倒数第三天就是上周五了，和当天日期无关

      获取当前年份、月份、日期
      var t14=moment().year()
      var t15=moment().month()//此处月份从0开始，当前月要+1
      var t16=moment().date();

      
      // 数字格式化
      function prefix_zero(num) {
          return num >= 10 ? num : "0" + num;
      }

      // 倒计时时间格式化
      function format_time(timeStamp) {
          let day = Math.floor(timeStamp / (24 * 3600 * 1000));
          let leave1 = timeStamp % (24 * 3600 * 1000);
          let hours = Math.floor(leave1 / (3600 * 1000));
          let leave2 = leave1 % (3600 * 1000);
          let minutes = Math.floor(leave2 / (60 * 1000));
          let leave3 = leave2 % (60 * 1000);
          let seconds = Math.floor(leave3 / 1000);
          if (day) return day + "天" + hours + "小时" + minutes + "分";
          if (hours) return hours + "小时" + minutes + "分" + seconds + "秒";
          if (minutes) return minutes + "分" + seconds + "秒";
          if (seconds) return seconds + "秒";
          return "时间到！";
      }

### 4.跨端事件处理

      // 是否支持触摸事件
      let isSupportTouch = ("ontouchstart" in document.documentElement) ? true : false;

      //禁用Enter键表单自动提交
      document.onkeydown = function(event) {
          let target, code, tag;
          if (!event) {
              event = window.event; //针对ie浏览器
              target = event.srcElement;
              code = event.keyCode;
              if (code == 13) {
                  tag = target.tagName;
                  if (tag == "TEXTAREA") { return true; }
                  else { return false; }
              }
          }
          else {
              target = event.target; //针对遵循w3c标准的浏览器，如Firefox
              code = event.keyCode;
              if (code == 13) {
                  tag = target.tagName;
                  if (tag == "INPUT") { return false; }
                  else { return true; }
              }
          }
      };

### 5. 移动端适配方案

      (function (doc, win) {
          var docEl = doc.documentElement,
              resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
              recalc = function () {
                  var clientWidth = docEl.clientWidth;
                  var fontSize = 20;
                  docEl.style.fontSize = fontSize + 'px';
                  var docStyles = getComputedStyle(docEl);
                  var realFontSize = parseFloat(docStyles.fontSize);
                  var scale = realFontSize / fontSize;
                  console.log("realFontSize: " + realFontSize + ", scale: " + scale);
                  fontSize = clientWidth / 667 * 20;
                  if(isIphoneX()) fontSize = 19;
                  fontSize = fontSize / scale;
                  docEl.style.fontSize = fontSize + 'px';
              };
          // Abort if browser does not support addEventListener
          if (!doc.addEventListener) return;
          win.addEventListener(resizeEvt, recalc, false);
          doc.addEventListener('DOMContentLoaded', recalc, false);

          // iphoneX判断
          function isIphoneX(){
              return /iphone/gi.test(navigator.userAgent) && (screen.height == 812 && screen.width == 375)
          }

      })(document, window);

### 6.xss预防方式
      // 敏感符号转义
      function entities(s) {
          let e = {
              '"': '&quot;',
              '&': '&amp;',
              '<': '&lt;',
              '>': '&gt;'
          }
          return s.replace(/["<>&]/g, m => {
              return e[m]
          })
      }

### 7. JS方法 
      // 数组去重方法 
      1. 过滤+indexof
      function distinct(arr = testArr) {
          return arr.filter((v, i, array) => array.indexOf(v) === i)
      }

      2. 双重for循环
      var array = [1, 1, '1', '1'];
      function unique(array) {
          // res用来存储结果
          var res = [];
          for (var i = 0, arrayLen = array.length; i < arrayLen; i++) {
              for (var j = 0, resLen = res.length; j < resLen; j++ ) {
                  if (array[i] === res[j]) {
                      break;
                  }
              }
              // 如果array[i]是唯一的，那么执行完循环，j等于resLen
              if (j === resLen) {
                  res.push(array[i])
              }
          }
          return res;
      }
      console.log(unique(array)); // [1, "1"]

      3.排序后相邻去除法 
      var array = [1, 1, '1'];
      function unique(array) {
          var res = [];
          var sortedArray = array.concat().sort();
          var seen;
          for (var i = 0, len = sortedArray.length; i < len; i++) {
              // 如果是第一个元素或者相邻的元素不相同
              if (!i || seen !== sortedArray[i]) {
                  res.push(sortedArray[i])
              }
              seen = sortedArray[i];
          }
          return res;
      }
      console.log(unique(array));

      4.Object 键值对
      var array = [1, 2, 1, 1, '1'];
      function unique(array) {
          var obj = {};
          return array.filter(function(item, index, array){
              return obj.hasOwnProperty(item) ? false : (obj[item] = true)
          })
      }
      console.log(unique(array)); // [1, 2]

      //-----------------------------------------
      var array = [{value: 1}, {value: 1}, {value: 2}];
      function unique(array) {
          var obj = {};
          return array.filter(function(item, index, array){
              console.log(typeof item + JSON.stringify(item))
              return obj.hasOwnProperty(typeof item + JSON.stringify(item)) ? false : (obj[typeof item + JSON.stringify(item)] = true)
          })
      }
      console.log(unique(array)); // [{value: 1}, {value: 2}]
      
      5.ES6
      var array = [1, 2, 1, 1, '1'];
      function unique(array) {
        return Array.from(new Set(array));
      }
      console.log(unique(array)); // [1, 2, "1"]


      // 置换函数
      function swap(arr, indexA, indexB) {
          [arr[indexA], arr[indexB]] = [arr[indexB], arr[indexA]];
      }













