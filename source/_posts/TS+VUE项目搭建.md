---
title: TS+VUE项目搭建
date: 2019-10-16 15:00:09
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
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=574919767&auto=1&height=66"></iframe>
</div>

闲来无事，随便写写......

# TS+VUE项目搭建

---
自尤大推出vue对typescript的支持后，一直想开箱尝试，对于前端sr来说，vue的顺滑加上ts的面向对象，想着就非常美好~ 终于在两个月前，找到了个机会尝试了一把vue+ts的组合。 开文记录下vue和ts整合之旅和遇到的一些坑。
## Vue 
应该大部分人都知道vue，毕竟如今vue是与react肩并肩的存在，所以就不过多介绍啦。

[vue中文官网](https://cn.vuejs.org/index.html) 官网上的教程就是最好的入门教程

## TypeScript
我在前几篇文章就一直有在宣传typescript，简单列举下ts的优点

1. 始于JavaScript，归于JavaScript,typescript是JavaScript的超集，所以它可以重用JavaScriptd代码,使用JavaScript的库

2. JavaScript用的优点它都有，跨浏览器、跨操作系统等

3. 面向对象的编程思想,强大的类型检查

开源大法好

要说缺点的话，那就是不太适合太小的项目。
就凭这些优点，足够我们愉快的玩耍~

## TS安装
 先将node安装，然后在通过npm安装ts的包

      npm install -g typescript

      tsc -v //查看ts的版本号
## 创建项目
### 执行安装命令

    npm install -g @vue/cli

 安装完成后，可以通过 vue create 快速创建一个新项目的脚手架，或者直接通过 vue serve 构建新想法的原型。

### 创建项目
    vue create vue-ts  //vue-ts 是我们的项目名称，执行后如下
    ![](1.jpg)

可看到有这么几个选项，xiaoli这个选项是我之前创建的，稍后会介绍；default这个后面写着 babel eslint ，表示若选择这个，那么只会引入babel和 ealint；manually select features顾名思义，选择我们想要的。那么我们选择第三个

![](2.jpg)

可看到列表里有很多选项，我们以vue+ts为主，所以我们选择 babel typescript router vuex 这几个，选择完后，如下

![](3.jpg)

接下来会有好几个yes or no 的选项，大家根据自己项目的需要来选择就可以，最后一步，`Save this as a preset for future projects?` 若选择yes，就会将我们之前的选择存储起来，作为一个预设选项，方便后续一键创建新项目。所有步骤选完，回车，便开始创建项目文件结构和拉取npm包

## 项目结构
 **项目结构如下**

![](4.jpg)

**public:** 用于存放静态文件，`index.html`入口文件就放在里面，这个文件夹下的文件不会纳入webpack的打包中；
**src：**存放vue项目工程文件，其中已经帮我们关联好router和vuex，文件结构非常简洁
其他：webpack、babel等配置文件

## 与TypeScript复用

项目在构建中，已经引入 `vue-class-component` ，用于对ts的支持，或者使用 `vue-property-decorator`,这个库是在之前那个的基础上扩展。

以下列举tsvue写法的各种变化

### 组件声明 
     import { Component, Prop, Vue, Watch } from 'vue-property-decorator';

      @Component
      export default class Test extends Vue {

      }

### data对象

通过构造函数创建data里的数据

      import { Component, Prop, Vue, Watch } from 'vue-property-decorator';

      @Component
      export default class Test extends Vue {
          private name: string;
          constructor() {
              super();
              this.name = 'xiaoli';
          }
      }
**data里的数据使用方式如下**
      public getName(){
          return this.name
      }    

### Prop声明

      @Prop() public msg: string;
      @Prop({ default: 'default value' }) propB: string
      @Prop([String, Boolean]) propC: string | boolean

### 生命周期函数使用
      public created(): void {
          console.log('created');
      }

      public mounted():void{
          console.log('mounted')
      }

### 自定义方法
js下是需要在method对象中声明方法，现变成如下

      public clickFunc(): void {
          console.log(this.name)
          console.log(this.msg)
      }

### Watch监听属性 

      @Watch('name',{ immediate: true, deep: true })
      public onChildChanged(val: string, oldVal: string) {
          console.log('watch new name=' + val);
      }

### computed计算属性

      public get allname() {
          return 'computed ' + this.name;
      } 

allname是计算后的值，name是被监听的值

### emit事件
      @Emit()
        addToCount(n: number) {
          this.count += n
        }

        @Emit('reset')
        resetCount() {
          this.count = 0
        }

第一个的事件名称为 add-to-count,n为传过去的参数；第二个事件名为reset-count,参数为空

### 指令和过滤器 
>我尝试了下，发现之前在入口文件直接引入指令或者过滤器的方式不管用了，因为用了ts后，组件的作用域跟之前的不一样了，然后我找了官方的issue，截图如下.

![](5.jpg)


**一个自定义指令**

      // ./directive/index.ts
      export const focus = {
          // 当被绑定的元素插入到 DOM 中时……
          inserted: function (el:HTMLElement) {
              // 聚焦元素
              el.focus()
            }
      }

**一个过滤器**

      // ./filter/index.ts
      export const capitalize = function (value:string) {
          if (!value) return ''
          value = value.toString()
          return value.charAt(0).toUpperCase() + value.slice(1)
      }


**组件中使用**

      import { capitalize }from '@/filter/index'
      import { focus } from '@/directive/index'
      @Component({
          filters:{capitalize},
          directives:{focus}
      })
      export default class Test extends Vue {}
      复制代码<div>
          <input v-focus v-model="modelData">
          <div>{{modelData | capitalize}}</div>
      </div>

## Vuex与TS的糅合

因为vuex是个可选的，所以单独列出来。首先需要引用 `vuex-class` 库，该库有如下几个模块

      import {
          namespace,
          Action,
          Getter,
          Mutation,
          State
      } from 'vuex-class';
 
分别对应vuex中的 action、getter、mutation等，使用ts对vuex的影响主要在组件对vuex的调用上，vuex的定义还是按照之前的写法即可 

      @State('foo') stateFoo
      @State(state => state.bar) stateBar
      @Getter('foo') getterFoo
      @Action('foo') actionFoo
      @Mutation('foo') mutationFoo
      @someModule.Getter('foo') moduleGetterFoo

      // If the argument is omitted, use the property name
      // for each state/getter/action/mutation type
      @State foo
      @Getter bar
      @Action baz
      @Mutation qu

若不想使用vuex定义的方法名，可以自定义属性名，因为都是定义在当前this上，所以直接使用this调用即可

      this.getterFoo // -> store.getters.foo
      this.actionFoo({ value: true }) // -> store.dispatch('foo', { value: true })

## 小结
 ......


  