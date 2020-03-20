---
title: VUE中使用echarts配合canvas绘制图例下载
date: 2019-10-24 13:06:09
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
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=411214279&auto=1&height=66"></iframe>
</div>

闲来无事，随便写写......

# VUE中使用echarts配合canvas绘制图例
---


## 什么是[canvas](https://www.runoob.com/html/html5-canvas.html)?
HTML5 `<canvas>` 元素用于图形的绘制，通过脚本 (通常是JavaScript)来完成.
`<canvas>` 标签只是图形容器，您必须使用脚本来绘制图形。
你可以通过多种方法使用 canvas 绘制路径,盒、圆、字符以及添加图像。


## 添加图例

  **html**

    <img src="../../../static/img/xx.png" id="zhinanzhen" alt="指南针" class="NS" v-if="NSShow" >
    <img src="../../../static/img/xx.png" id="bilichi" alt class="blc" v-if="NSShow" />

  **js**

        //点击下载
        downloadImg() {
        let canvas = document.getElementsByTagName('canvas')[0]; // 获取地图元素
        let tempcanvas = document.createElement('canvas');  // 创建地图元素
        tempcanvas.width = 700;
        tempcanvas.height = canvas.height;
        // tempcanvas.style.backgroundColor = '#fff'
        let ctx = tempcanvas.getContext('2d'); 


        ctx.drawImage(canvas, (canvas.width - 700) / 2, 0, 700, canvas.height, 0, 0, 700, canvas.height);
        //context.drawImage(img,sx,sy,swidth,sheight,x,y,width,height);
        let img1 = document.getElementById("zhinanzhen"); 
        img1.setAttribute('crossOrigin', 'anonymous'); // 图片跨域
        ctx.drawImage(img1, 550, 100, 82, 82)
        //ctx.drawImage(img1, 左右, 上下, 长, 宽)
        let img2 = document.getElementById("bilichi");
        img2.setAttribute('crossOrigin', 'anonymous');
        ctx.drawImage(img2, 50, canvas.height - 32, 165, 32)


        let url = tempcanvas.toDataURL("image/png"); // 生成图片 第二个参数0-1 默认0.94
        // let url=tempcanvas.toDataURL("image/jpeg", 1.0);

        var oA = document.createElement("a");
        oA.download = '';// 设置下载的文件名，默认是'下载'
        oA.href = url;
        document.body.appendChild(oA);
        oA.click();
        oA.remove(); // 下载之后把创建的元素删除
         }
         // 绘制底图 

        drawMap() {
        let _this = this
        this.$echarts.registerMap('maps', china);
        mapcontainerPro ? mapcontainerPro.dispose() : ''
        mapcontainerPro = this.$echarts.init(document.getElementById('mapcontainerPro'));
        mapcontainerPro.setOption({   
          title: [{
            text: this.imgTitle,
            left: 'center',
            top: '3%',
            textStyle: {
              color: 'black',
              fontSize: 16
            }
          }, {
            text: this.unit,
            left: '34%',
            bottom: '22%',
            textStyle: {
              fontSize: 16,
              fontWeight: 'bold'
            }
          }],
          tooltip: {
            show: true,
            formatter: '{b0}: {c0}'
          },
          toolbox: {
            show: false,
            feature: {
              dataView: {},
              // saveAsImage: {
              //   show: true,
              //   excludeComponents: ['toolbox'],
              //   pixelRatio: 2
              // }
            }
          },
          color: ['#5B9CD6'],
          visualMap: {            // 图例
            pieces: this.pieces,
            inverse: false,       // 图例排序
            orient: 'vertical', //图例方向
            left: '34%',
            top: '78%',
            // min: 0,//最小
            // max: this.range4,//最大
            // splitNumber: 4,//共分5层
            color: this.vColor,//颜色从高到低依次渐变
            textStyle: {
              fontSize: 16
              // color: '#00000',
              //text:'9jfhfhn'
            },
          },
          series: [
            {
              name: '全国地图',
              type: 'map',
              aspectScale: 0.9, //地图长宽比
              zoom: 1.1, //缩放比例
              top: '15%',
              left: 'center',
              label: {
                normal: {
                  fontSize: 12
                }
              },
              map: 'maps', // 自定义扩展图表类型
              symbolSize: function (val) {
                return val[2] / 10;
              },
              // label:{
              //   show:true,
              //   fontSize:12,
              //   offset:[30,40]
              // },
              itemStyle: {
                normal: {
                  label: {
                    show: true,
                    fontWeight: "bolder",
                    fontSize: 12
                  },
                  areaColor: 'blue',
                  borderColor: 'black',
                  borderWidth: 0
                },
                emphasis: { label: { show: true } },
              },
              data: this.showData
            }
          ]
        });
      }














