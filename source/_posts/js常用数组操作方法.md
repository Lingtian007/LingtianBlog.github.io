---
title: js常用数组操作方法
date: 2019-01-22 12:32:09
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

**4. splice()**
作用：删除、插入、替换数组项
参数：startIndex[, deleteCount[, item1[, ...[, itemN]]]]
返回值：删除项组成的数组
原数组是否改变：是
let arr = [1, 2, 3];

// 插入元素
let temp = arr.splice(1, 0, 'a', 'b'); // 在索引1的位置插入元素'a'和'b' 
console.log(arr, temp); // [1, 'a', 'b', 2, 3] []

// 删除元素
let temp1 = arr.splice(1, 2); // 删除从索引1的位置开始的2项 
console.log(arr, temp1); // [1, 2, 3] ['a', 'b']

// 替换一个元素
let temp2 = arr.splice(1, 1, 'a'); // 将索引1的位置的元素替换为'a'
console.log(arr, temp2); // [1, 'a', 3 ] [2]

// 替换多个元素
let temp3 = arr.splice(0, 2, 'b', 'c'); // 将索引0的位置开始的两项，替换成’b‘和’c‘
console.log(arr, temp3); // [’b‘, 'c', 3] [1, 'a']

// 只传第一个参数，则删除从第一个参数指定的位置到数组结尾的所有项
let temp4 = arr.splice(0); //从索引0的位置开始，删除后面的所有项
console.log(arr, temp4); // [] [’b‘, 'c', 3]

**6. copyWithin()**

作用：将数组指定位置（start到end）的元素复制到当前数组的其他位置（target开始），这种复制会替换原位置的元素（ES6新增）
参数说明：target[,start[,end]]
参数说明：

target: 复制的目标位置（包括），即要被替换的元素开始的位置
start: 要copy的元素的开始位置，默认0
end: 要copy的元素的结束位置，默认为数组最后一个元素

返回值：复制替换之后的数组
原数组是否改变：是
let arr = [1, 2, 3, 4, 5];
// 用索引0~4范围内的元素，替换索引3~4范围内的元素，因为要替换的位置只有两个，所以只将4，5替换为了1，2
let temp = arr.copyWithin(3);
console.log(arr, temp); //  [1, 2, 3, 1, 2] [1, 2, 3, 1, 2]

let arr1 = [1, 2, 3, 4, 5];
// 用索引2~4范围内的元素，替换索引3~4范围内的元素，因为要替换的位置只有两个，所以只将4，5替换为了3，4
let temp1 = arr1.copyWithin(3, 2);
console.log(arr1, temp1); // [1, 2, 3, 3, 4] [1, 2, 3, 3, 4]

>小结：
总结上述的描述，copyWithin的作用就是在数组长度的范围内，复制start(包括)到end(不包括)范围内的元素，然后用上述的元替换掉从target（包括）开始到数组结尾的元素，能替换多少就替换多少

**7. reverse**
作用：翻转原数组
参数：无
返回值：翻转后的数组
原数组是否改变：是
let arr = [1, 2, 3];
let temp = arr.reverse();
console.log(arr, temp); // [ 3, 2, 1 ] [ 3, 2, 1 ]

**8. sort()**
作用：数组排序
参数：compareFunction
参数说明：

compareFunction返回值大于0时调换当前比对项的顺序，否则顺序不 变;
参数可以不传，不传默认按照Unicode编码的顺序排列
返回值：排序后的数组
原数组是否改变：是
// 数组从小到大排序
let arr = [1, 4, 6, 7, 8, 3, 2];
let temp = arr.sort((a, b) => {
    return a - b;
})
console.log(arr, temp); // [ 1, 2, 3, 4, 6, 7, 8 ] [ 1, 2, 3, 4, 6, 7, 8 ]

// 一个实用的数组排序的例子，根据对象元素的排序，排序对象在数组中的位置
let objArr = [{id: 3, name: "lilei"},{id: 1, name: "hanmeimei"},{id: 2, name: "yimi"}];
let tempArr = objArr.sort((a, b) => {
    // 按照id从小到大的顺序，对数组中的对象进行排序
    // 这个示例说明回调函数的形参a,b实际就是数组中当前进行比对的两个元素
    return a.id - b.id;
}); 
console.log(objArr); //  [{id: 1, name: 'hanmeimei'}, {id: 2, name: 'yimi'}, { id: 3, name: 'lilei' }]
console.log(tempArr); // [{id: 1, name: 'hanmeimei'}, {id: 2, name: 'yimi'}, { id: 3, name: 'lilei'}]

**9. concat** 
作用：基于当前的数组拼接数组
参数：value1[, value2[, ...[, valueN]]
参数说明：

参数的类型可以是任意类型。
不是数组类型直接按顺序拼接到数组末尾，数组类型的则将数组元素逐一取出拼接到数组末尾
不传则相当于复制数组

返回值：拼接后的数组
原数组是否改变：否

let arr = [1,2];
let temp = arr.concat('a', {id:1}, ['lilei', 'hanmeimei']);
console.log(arr, temp); // [ 1, 2 ] [ 1, 2, 'a', { id: 1 }, 'lilei', 'hanmeimei']

// 用于复制数组
let arr = [1, 2];
let temp = arr.concat();
console.log(arr, temp);  // [ 1, 2 ] [ 1, 2 ]

**10. slice()**
作用：基于当前数组的一项或多项创建一个新的数组
参数：startIndex[,endIndex]
参数说明：返回的元素包含startIndex位置的元素，但不包括endIndex位置的元素
返回值：返回截取的元素组成的数组
原数组是否改变：否

let arr = [0, 1, 2, 3, 4];
let temp = arr.slice(1,3); // 返回从索引1（包括）位置到索引3（不包括）位置之前的元素
console.log(arr, temp); // [0, 1, 2, 3, 4] [1, 2]

// 用于复制数组
let arr = [0, 1, 2, 3, 4];
let temp = arr.slice(0); // 返回从索引0（包括）位置到数组结尾的所有元素
console.log(arr, temp); // [0, 1, 2, 3, 4] [0, 1, 2, 3, 4]

**11.indexOf()**:
作用：从数组开头查找元素在数组中的索引位置（ES5的方法）
参数：searchElement[, fromIndex]
返回值：searchElement在数组中的索引，没找到searchElement则返回-1
原数组是否改变：否
let arr = [1, 2, 3, 4, 5, 6, 2];
// 从数组开头开始查找
let temp = arr.indexOf(2);
console.log(arr, temp); // [ 1, 2, 3, 4, 5, 6, 2 ] 1
// 从指定的位置开始查找
let temp1 = arr.indexOf(2,3); // 从索引3(包括)的位置向后查找元素2
console.log(arr, temp1); // [ 1, 2, 3, 4, 5, 6, 2 ] 6
复制代码

**12.lastIndexOf():**
作用：从数组结尾查找元素在数组中的索引位置（ES5的方法）
参数：searchElement[, fromIndex]
返回值：searchElement在数组中的索引，没找到searchElement则返回-1
原数组是否改变：否
let arr = [1, 2, 3, 4, 5, 6, 2];
// 从数组末尾开始查找
let temp = arr.lastIndexOf(2);
console.log(arr, temp); // [ 1, 2, 3, 4, 5, 6, 2 ] 6
// 从指定的位置开始查找
let temp1 = arr.lastIndexOf(2,3); // 从索引3(包括)的位置向前查找元素2
console.log(arr, temp1); // [ 1, 2, 3, 4, 5, 6, 2 ] 1
复制代码

**13.every():**
作用：对数组中的每一项运行给定函数，如果该函数对每一项都返回true,则返回true（ES5方法）
参数：callback[, thisArg]
参数说明：callback有三个参数item(当前项),index(当前项索引)，array(数组对象本身)
返回值：true 或 false
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
let arr = [1, 2, 3, 4];
let temp = arr.every((item, index, array) => {
    return item > 2;
});
console.log(arr, temp); // [ 1, 2, 3, 4 ] false

// 方法的第二个参数可选，作用是设定第一个参数中的this指向，如果使用第二个参数，注意callback不能是箭头函数
// 后面的迭代方法涉及此参数的，用法相同，不在赘述
let arr = [1, 2, 3, 4];
let temp = arr.every(function(item, index, array) {
    return item > this.id;
}, {id: 2});
console.log(arr, temp); // [ 1, 2, 3, 4 ] false
复制代码

**14.some():**
作用：对数组中的每一项运行给定函数，如果该函数对任意一项返回true,则返回true（ES5方法）
参数：callback[, thisArg]
参数说明：callback有三个参数item(当前项),index(当前项索引)，array(数组对象本身)
返回值：true 或 false
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
let arr = [1, 2, 3, 4];
let temp = arr.some((item, index, array) => {
    return item > 2;
});
console.log(arr, temp); // [ 1, 2, 3, 4 ] true
复制代码

**15.filter():**
作用：对数组中的每一项运行给定函数，返回该函数返回true的项组成的数组（ES5方法）
参数：callback[, thisArg]
参数说明：callback有三个参数item(当前项),index(当前项索引)，array(数组对象本身)
返回值：函数返回true的项组成的数组
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
let arr = [1, 2, 3, 4];
let temp = arr.filter((item, index, array) => {
    return item > 2;
});
console.log(arr, temp); // [ 1, 2, 3, 4 ] [3, 4]
复制代码

**16.map():**
作用：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组（ES5方法）
参数：callback[, thisArg]
参数说明：callback有三个参数item(当前项),index(当前项索引)，array(数组对象本身)
返回值：函数每次调用结果组成的数组
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
let arr = [1, 2, 3, 4];
let temp = arr.map((item, index, array) => {
    return item * item;
});
console.log(arr, temp); // [ 1, 2, 3, 4 ] [ 1, 4, 9, 16]
复制代码

**17.forEach():**
作用：对数组中的每一项运行给定函数。无返回值（ES5方法）
参数：callback[, thisArg]
参数说明：callback有三个参数item(当前项),index(当前项索引)，array(数组对象本身)
返回值：无
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
let arr = [1, 2, 3, 4];
let temp = arr.forEach((item, index, array) => {
    // 不会有返回值，但可在这里执行某些操作
    return item * item;
});
console.log(arr, temp); // [ 1, 2, 3, 4 ] undefined
复制代码
注意：
forEach在所有项都遍历完成之前，无法像for循环一样提前终止循环



**18.reduce():**
作用：从数组的第一项开始，逐步遍历到最后，迭代数组的所有项（ES5方法）
参数：callback[, initialValue]
参数说明：

callback迭代函数，有四个参数（prev, cur, index, array）

prev 前一个值，（initialValue || 数组第一项 || 上一次迭代的结果）
cur 当前迭代项
index 当前迭代项索引
array 迭代的原数组


initialValue 迭代的基础值，不传基础值是数组第一项

返回值：数组迭代后，整体的迭代结果
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
// 数组求和
let arr = [1, 2, 3];
let sum = arr.reduce((prev, cur, index, array) => {
    return prev + cur;
});
console.log(arr, sum); // [ 1, 2, 3 ] 6

// 传initialValue 基础值的示例
let sum1 = arr.reduce((prev, cur, index, array) => {
    return prev + cur;
}, 10);
// 返回的值是：10+1+2+3
console.log(arr, sum1); // [ 1, 2, 3 ] 16
复制代码
reduce源码的实现：
Array.prototype.myReduce = function(callback, initialVal){
   let prev = initialVal || this[0]; 
    for(var i = pre ? 0 : 1; i < this.length; i++){
        prev = callback(prev, this[i], i, this);
   }
   return prev
}
复制代码


**19.reduceRight():**
作用：从数组的最后一项开始，逐步遍历到第一项，迭代数组的所有项（ES5方法）
参数：callback[, initialValue]
参数说明：

callback迭代函数，有四个参数（prev, cur, index, array）

prev 前一个值，（initialValue || 数组第一项 || 上一次迭代的结果）
cur 当前迭代项
index 当前迭代项索引
array 迭代的原数组


initialValue 迭代的基础值，不传基础值是数组第一项

返回值：数组迭代后，整体的迭代结果
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
// 拼接字符串,从后向前迭代数组进行拼接
let arr = ['h', 'e', 'l', 'l', 'o'];
let str = arr.reduceRight((prev, cur, index, array) => {
    return prev + cur;
});
console.log(arr, str); // [ 'h', 'e', 'l', 'l', 'o' ] 'olleh'
复制代码

**20.find():**
作用：查找数组中第一个符合条件的元素，返回该元素 (ES6新增)
参数：callback[, thisArg]
参数说明：参数的使用同上述的forEach、every、map、some、filter方法一致
返回值：查找到则返回该元素，没找到返回undefined
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
let arr = [1, 2, 3, 4, 5];
let temp = arr.find((item, index, array) => {
    return item > 2;
})
console.log(arr, temp); // [1, 2, 3, 4, 5] 3
复制代码

**21.findIndex():**
作用：查找数组中第一个符合条件的元素所在位置的索引，并返回该索引值
参数：callback[, thisArg]
参数说明：参数的使用同上述的forEach、every、map、some、filter方法一致
返回值：查找到则返回该索引值，没找到返回-1
原数组是否改变：涉及callback，因此不确定，具体详情见下文中的原型方法的小结部分。
let arr = [1, 2, 3, 4, 5];
let temp = arr.findIndex((item, index, array) => {
    return item > 2;
})
console.log(arr, temp); // [1, 2, 3, 4, 5] 2
复制代码

**22.fill():**
作用：用指定元素，填充数组从start(包括)到end（不包括）之间的元素，如果该区间内已经有元素，直接替换掉（ES6新增）
参数：value[, start[, end]]
返回值：填充后的数组
原数组是否改变：是
let arr = [1, 2, 3, 4, 5];
let temp = arr.fill('a', 2, 4);
console.log(arr, temp); // [1, 2, 'a', 'a', 5] [1, 2, 'a', 'a', 5]
复制代码

**23.includes():**
作用：判断数组中是否包含指定的元素（ES7新增）
参数：searchElement[, fromIndex]
返回值：true或false
原数组是否改变：否
let arr = [1, 2, 3, 4, 5];
let temp = arr.includes(5);
console.log(arr, temp); // [1, 2, 3, 4, 5] true

// 这个方法弥补了indexOf查看元素时的一个不足，即查找NaN的误差
let arr1 = [NaN, 'a'];
let temp1 = arr1.includes(NaN);
let temp2 = arr1.indexOf(NaN);
console.log(temp1, temp2); // true -1
复制代码

**24.toString()、toLocalString():**
作用：调用数组每一项的toString()方法，返回的是以逗号分隔的字符串
参数：无
返回值：转化后的字符串
原字数组是否改变：否
let arr = [1, [1, 2, [4]], {name: "zhangsan"}, 3];
let temp = arr.toString();
console.log(arr); [ 1, [ 1, 2, [ 4 ] ], { name: 'zhangsan' }, 3 ] 
console.log(temp); // '1,1,2,4,[object Object],3'
复制代码

**25.join():**
作用：将数组元素转化为字符串(调用每个元素的toString方法)，并使用指定的分隔符（默认为逗号）进行拼接，返回拼接后的字符串
参数：分隔符，默认为逗号（，）
返回值：拼接后的字符串
原数组是否改变：否
let arr = [1, [1, 2, [4]], {name: "zhangsan"}, 3];
let temp = arr.join();
console.log(arr); [ 1, [ 1, 2, [ 4 ] ], { name: 'zhangsan' }, 3 ] 
console.log(temp); // '1,1,2,4,[object Object],3'

// 数组求和
let arr1 = [1, 2, 3];
console.log(eval(arr1.join('+'))); // 6

**数组扩展运算符（ES6新增）**

数组的扩展运算符可以将数组转化为以逗号分割的参数序列。
几个简单使用的应用场景：

1.将数组通过扩展运算符转化为参数序列直接传参，无需使用apply转化了let arr = [1, 2, 3];

// apply写法
Math.min.apply(null, arr)

// 扩展运算符写法
Math.min(...arr)
复制代码
2.可以用于复制和拼接数组let arr1 = [2, 3, 4];
let arr2 = ['a', 'b', 'c'];

// 拼接数组arr1和arr2
console.log([...arr1, ...arr2]); // [2, 3, 4, 'a', 'b', 'c']
复制代码
3.可用于将字符串分解为真正的数组，[…'hello']  // [ 'h', 'e', 'l', 'l', 'o' ]













