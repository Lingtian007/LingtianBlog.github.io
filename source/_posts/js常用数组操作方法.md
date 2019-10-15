---
title: js常用数组操作方法
date: 2018-01-22 12:32:09
top: false
cover: false
password:
toc: true
mathjax: false
summary: 闲来无事，随便写写。
tags:
- 方法
categories:
- 方法
---

<div align="middle">
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=407679465&auto=1&height=66"></iframe>
</div>

闲来无事，随便写写......

# 开篇
---
你真的了解JS数组的那些方法吗？


>寄语：
JS数组的方法非常的丰富和琐碎，学习和使用过程中总是需要反复的记忆、查看文档，但作为JS基础这样真的不应该，我们应该把它记得滚瓜烂熟，深入理解才对。
但是要怎样才能做到呢？这正是我也本文的初衷，根据个人的经验总结了一下，希望能够帮助和我一样困惑的人，搞定这个头疼的问题。



**数组的方法**
JavaScript的数组方法包括数组原型的方法、构造函数的方法（ES6新增部分）
针对每一个方法我们主要了解四个方面：**作用、参数、返回值、原数组是否改变**

**（一）. 原型上的方法**

**1. push()**
作用：向数组的末尾添加一项或多项
参数：ele1[, ele2[, ...[, elen]]]
返回值：添加元素后数组的长度
原数组是否改变：是

let arr = [1, 2, 3];
let temp = arr.push('a', 'b');
console.log(arr, temp); // [1, 2, 3, 'a', 'b'] 5

**2. pop()**
作用：删除数组最后一项
参数：无
返回值：删除的那一项
原数组是否改变：是

let arr = [1, 2, 3];
let temp = arr.pop();
console.log(arr, temp); // [1, 2] 3

**3. unshift()**
作用：向数组开头添加一项或多项
参数：ele1[, ele2[, ...[, elen]]]
返回值：添加元素后数组的长度
原数组是否改变：是
let arr = [1, 2, 3];
let temp = arr.unshift('a', 'b');
console.log(arr, temp); // ['a', 'b', 1, 2, 3] 5












