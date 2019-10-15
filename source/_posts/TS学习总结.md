---
title: ts基础总结
date: 2019-10-15 14:00:09
top: true
cover: false
password:
toc: true
mathjax: false
summary: 闲来无事，随便写写。
tags:
  - TS
categories:
  - TS
---

<div align="middle">
<!-- <iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=411214279&auto=1&height=66"></iframe> -->
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=28854182&auto=1&height=66"></iframe>
</div>

闲来无事，随便写写......

# ts 基础总结

---

**ts 有什么用**

类型检查, 拥抱 es6，支持部分的 esNext 草案，直接编译到原生 js、引入新的语法糖

**为什么用 ts**

> TypeScript 的设计目的应该是解决 JavaScript 的“痛点”：弱类型和没有命名空间，导致很难模块化，不适合开发大型程序。另外它还提供了一些语法糖来帮助大家更方便地实践面向对象的编程。
> typescript 不仅可以约束我们的编码习惯，还能起到注释的作用，当我们看到一函数后我们立马就能知道这个函数的用法，需要传什么值，返回值是什么类型一目了然，对大型项目的维护性有很大的提升。

**编译报错， 会生成编译结果么？**

答案是肯定的,当然可以在 tsconfig.json 的配置， noEmitONError

# 基础总结

## 数据类型

- boolean 、number、string、null、 undefined、 Symbol
- undefined 和 null 类型的数据只能被赋值 undefined 和 null， 但是这个类型是所有类型的子类型
- void 空类型
  // undefined 和 null 是所有类型子类型，都可以赋值
  let num: Symbol = undefined;ss
  let num: number = undefined;
  // undefined 类型， 只能给 undefined
  let u: undefined = undefined;
  let n: null = null;
- any 和类型推断
  // 在 ts 中，变量在声明的时候，如果没有定义其类型，会被识成默认类型
  let str;
  str = 'I am strgting';
  str = 1024;
  // 未定义类型，直接赋值
  let num= 124;
  // 等同于 let num:number = 124, 在后面代码如果赋予 num 一个 string 会被报错

## 多个可能属性

      //只能访问可能属性的共有属性
      function getLength(param: string| number) {
          return param.length;
      }
      // 会报错， 因为 length不是 sting和number类型的共有属性
      // 技巧--》 使用类型别名
      type possibleType = string | number;
      function getLength(param: possibleType) {
          return param.length;
      }

## 接口的概念

- 在 ts 中，interface 包括对行为的抽象，由类去实现（implements）
- 也包括对对象轮廓的描述

## 对象 interface -》动态属性

必选参数和可选参数的类型是动态属性类型的子集，所有在动态属性类型设置的时候要设置上所有类型

只读属性的约束力
注意点： 只读属性的约束力在于第一次给对象赋值的时候，而不是给属性赋值的时候 readonly 和 const 的区别： const 是变量， readonly 是属性

## 接口-》抽象方法的实现

      export interface ISRequest {
        fetch(url: string, arg?: Object, callback?: Function): Promise<Object>;
      }
      export class SafeRequest implements ISRequest {
            public async fetch(url: string, arg, callback?: Function): Promise<Object> {
              return new Promise((resolve, reject) => {

              })
      }

## 用接口表示数组

      interface NumberArray {
            [index: any]: number
        }
        let numArr: NumberArray = [1, 2, 3]

## 函数的类型

- 可选参数, 必须在必选参数后面
- 参数默认值
  function buildName(firstName: string, lastName?: string) {
    
   }
- 添加默认值的参数识别为可选参数
- 剩余参数

## 类型断言

## 疑惑--》 声明文件

当使用第三方库时，我们需要引用它的声明文件，才能获得对应的代码补全、接口提示等功能。
声明文件在哪里？

- 与 npm 包绑定在一起
- npm 包的维护者并没有提供声明文件， 只能由其他人将声明文件发布到@types 里面
- 自己写个声明文件

npm 包的声明文件 和全局变量的声明文件
在 npm 包的声明文件中，使用 declare 不再会声明一个全局变量，而只会在当前文件中声明一个局部变量。只有在声明文件中使用 export 导出，然后在使用方 import 导入后，才会应用到这些类型声明。
######declare global
使用 declare global 可以在 npm 包或者 UMD 库中扩展全局变量的类型

## 内置对象

[内置对象查询--》点击](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
ESMAScript 提供了 Boolean、Error、Date、RegExp

       interface obj = {
            param: Function
            param: Promise
        }

枚举--》 数据的双向映射

        enum companyList= {1: 'aaa', 2: 'bbb'}
        var companyList = {
            1: 'aaa',
            2: 'bbb',
            aaa: 1,
            bbb: 2
        }

## Vue in Typescript

### 三大利器

- vue-component-class
- 方法可以直接声明为类成员方法。
- 可以将计算属性声明为类属性访问器。
- 默认 data 被当作类属性
- data ， render 和 vue 的生命周期的钩子直接是类成员的方法，保留这些命名，不要冲突
- 对于其他的配置项，例如 prop、componets 等传递给装饰器函数


    import Vue from 'vue';
    import Component from 'vue-componet-class';
    Component.resgisterHooks([
        'beforeRouteEnter'
    ])
    @Componnet({
        props: {

        },
        components: {

        }
    })
    export default class App extends Vue {
        // aa = '';
        // 类型推断aa是个string， 后面aa只能赋值aa类型
        // 所以最好使用先声明后

        //  data
       public tableModelItems: Array<any>;
       constructor() {
           super();
           this.tableModelItems = [];
       }
       // computed
      public get filterTableData() {
    	return this.tableData.filter((i: any) => i.refundStatus === 0).length

    	// 方法
    	// 声明周期

    	// 此时需要路由函数的生命周期钩子咋办
    	beforeRouteEnterf() {
    	    next() // 一定要写，否则玩不下去，为什么？
    	}
    }


    }

    - vue-property-decorator(依赖vue-component-class提供了更多了装饰器，代码更加显示 )
    - @Emit
    - @Inject
    - @Prop
    - @Provide
    - @Watch
    - vuex-class（连接了vue和vuex）

    ## 还没搞定的bug

### 错误--》 类型报错
+ 添加script的类型
      <script lang="ts"></script>
      <!--否则下面的类型报错-->

### 错误之--》Vue中挂载propoty出错（如果还是爆红，重启ide）
声明再挂载

        <!--inject-->
          import _Vue from 'vue'
          import moment from "moment";
          export default {
            install(Vue: typeof _Vue, options: any) {
              Vue.prototype.$moment = moment;
              Vue.prototype.$log = () => {
                console.log(new Date())
              }
            }
          }
        <!--types-->
          import Vue from 'vue'
          declare module 'vue/types/vue' {
            interface Vue {
              $moment: Function
              $log: Function
            }
          }

### ts中不能识别.vue文件
 
 **TypeScript 默认只识别 .ts 文件，不识别 .vue 文件, 乖乖的写 import Component from 'components/component.vue'**
![](1.jpg)

### vuex-class的Emit传参数给父组件报错

    @emit("reset")
    reset(role, this.formData){}
    <!--此时报错-->

![](2.jpg)

### 错误--> 可选参数爆红
![](3.jpg)

# 参考链接 
 + [ts的官网](https://www.tslang.cn/docs/handbook/basic-types.html)
 + [vue+ts快速上手](https://juejin.im/post/5ba75b355188255c5e66e4d3)
 + [ts通俗易懂，比较清晰的文档](https://ts.xcatliu.com/)
 + [尤大大对于ts+vue的看法](https://mp.weixin.qq.com/s?__biz=MzUxMzcxMzE5Ng==&mid=2247490464&idx=1&sn=0c75aaab12002c76198a8d6f183cd686&chksm=f951aee3ce2627f50a5ac6799964919e54a7298288f8bf881931d7c6769b05e302418bdb8051&scene=27#wechat_redirect)
 + [蚂蚁金服的ts实践](https://juejin.im/post/5a9c004a6fb9a028b92c9e91#heading-7)
 ......



  