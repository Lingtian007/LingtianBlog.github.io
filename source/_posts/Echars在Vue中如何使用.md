---
title: 如何在 Vue 项目中使用 Echarts
date: 2019-10-17 09:32:09
top: true
cover: false
password:
toc: true
mathjax: false
summary: 闲来无事，随便写写。
tags:
  - Vue
categories:
  - Vue
---

<div align="middle">
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=411214279&auto=1&height=66"></iframe>
</div>

废话不多说，那我们就看看如何在 Vue 的项目中使用 echarts......

# 如何在 Vue 项目中使用 Echarts

---

## 第一种方法 直接引入 Echarts

### 安装 echarts 项目依赖

        npm install echarts --save
        //或者
        npm install echarts -S

如果没有科学上网的朋友可以使用国内的淘宝镜像。

        npm install -g cnpm --registry=https://registry.npm.taobao.org
        cnpm install echarts -S

- 首先我们需要在自己的项目 main.js 中全局引入 Echarts

        import echarts from 'echarts';
        Vue.prototype.$echarts=echarts;

### 创建图表

        <template>
        <div id="app">
          <div id="main" style="width: 600px;height:400px;"></div>
        </div>
        </template>
        export default {
          name: "app",
          methods: {
            drawChart() {
              // 基于准备好的dom，初始化echarts实例
              let myChart = this.$echarts.init(document.getElementById("main"));
              // 指定图表的配置项和数据
              let option = {
                title: {
                  text: "ECharts 入门示例"
                },
                tooltip: {},
                legend: {
                  data: ["销量"]
                },
                xAxis: {
                  data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
                },
                yAxis: {},
                series: [
                  {
                    name: "销量",
                    type: "bar",
                    data: [5, 20, 36, 10, 10, 20]
                  }
                ]
              };
              // 使用刚指定的配置项和数据显示图表。
              myChart.setOption(option);
            }
          },
          mounted() {
            this.drawChart();
          }
        };
        </script>

### 入门实例

  ![](4.jpg)

## 第二种方法 使用 Vue-ECharts 组件

### 安装组件

      npm install vue-echarts -S

### 使用组件

      <template>
        <div id="app">
          <v-chart class="my-chart" :options="bar"/>
        </div>
      </template>
      <script>
      // 在对应组件内引用或者main.js全局引用
      import ECharts from "vue-echarts/components/ECharts";
      import "echarts/lib/chart/bar";`
      export default {
        name: "App",
        components: {
          "v-chart": ECharts
        },
        data: function() {
          return {
            bar: {
              title: {
                text: "ECharts 入门示例"
              },
              tooltip: {},
              legend: {
                data: ["销量"]
              },
              xAxis: {
                data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
              },
              yAxis: {},
              series: [
                {
                  name: "销量",
                  type: "bar",
                  data: [5, 20, 36, 10, 10, 20]
                }
              ]
            }
          };
        }
      };
      </script>
      <style>
      .my-chart {
        width: 800px;
        height: 500px;
      }
      </style>

### 入门实例

![](1679c3f7aa381aa7)

## 问题

### 问题1：父子组件传值，容易造成点开子组件后，echarts 图不出现

    原因：因此在另一个父组件进行应用的时候，他是首屏就加载，数据不变动。但是当数据变动之后，无法自动的更新图表。由于 mounted 只会在挂载的时候执行一次，因此无法后续进行更新。
    **解决办法：给父组件加上一个 v-if，使子组件重新渲染**

      <template>
       <div>
       <envy-pie :voltage="voltage" v-if="flag">
       </div>
      </template>
        //js部分
        data () {
              return {
                voltage: [],
                flag: false
              }
            },
            components: {
              envyPie
            },
            methods: {
              getEnvyContent () {
                axios.get('../../../static/mock/envy.json').then(this.getEnvyContentSucc)
              },
              getEnvyContentSucc (res) {
                if (res) {
                  const data = res.data
                  this.voltage = res.data.capacity_by_voltage
                  this.flag = true
                }
              }
            },
            mounted() {
              this.getEnvyContent()
            }

### 问题2:自动缩放
  Echarts 本身是不支持自动缩放的，但是 Echarts 为我们提供了 resize 方法。

        //在**调用方法**中加入下面这行代码
        window.addEventListener("resize", this.chart.resize);

### 问题3:支持数据自动刷新 
[原文链接](https://juejin.im/post/5ab220b8f265da237c68ca11)

    因为 Echarts 是数据驱动的，这意味着只要我们重新设置数据，那么图表就会随之重新渲染，这是实现本需求的基础。我们再设想一下，如果想要支持数据的自动刷新，必然需要一个监听器能够实时监听到数据的变化然后告知 Echarts 重新设置数据。所幸 Vue 为我们提供了==watcher==功能，通过它我们可以很方便的实现上述功能


      //在Chart.vue中加入watch
      watch: {    
        //观察option的变化
         option: {      
           handler(newVal, oldVal) {       
              if (this.chart) {          
              if (newVal) {            t
              his.chart.setOption(newVal);          
              } else {            
              this.chart.setOption(oldVal);   }      
              } else {            
              this.init();   
              } },      
              deep: true //对象内部属性的监听，关键。  
              } 
            }


### 问题4:图表太丑怎么破，ECharts神器带你飞！
[原文链接](https://juejin.im/post/59dcb823f265da432d270f26)
### 问题5:Echarts x轴文本内容太长的几种解决方案
[原文链接](https://juejin.im/post/5d255d69f265da1b80206db1)
### Echars 遇到问题汇总....
[原文链接](https://www.cnblogs.com/padding1015/p/9936533.html)