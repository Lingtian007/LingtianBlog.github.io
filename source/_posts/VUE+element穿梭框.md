---
title: 一个基于vue和element-ui的树形穿梭框组件
date: 2019-08-20 13:32:09
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
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=28854182&auto=1&height=66"></iframe>
</div>

闲来无事，随便写写......

# 开篇
---
一个基于vue和element-ui的树形穿梭框组件

**el-tree-transfer**

>el-tree-fransfer是一个基于VUE和element-ui的树形穿梭框组件，使用前请确认已经引入element-ui！ 此组件功能类似于element-ui的transfer组件，但是里面的数据是树形结构！ 实际上，el-tree-transfer依赖的element-ui组件分别是Checkbox 多选框，Button 按钮，和最主要的Tree 树形控件写成！并非是在element-ui的穿梭框组件上的扩展，而仅仅是参照了其外观样式和功能。ui完全按照element-ui风格。
注意：使用此插件时默认你已经引入了element-ui的button，check-box，tree组件！
第一层数据的 pid 请设定为 0！！
id推荐为string，但也可以是number，请不要混用，id不能重复！

**1.先npm下载插件**
     1. npm install el-tree-transfer --save
      或
     2.npm i el-tree-transfer -S

然后你可以像使用普通组件一样使用el-tree-transfer


      <template>
          <div>
          // 你的代码
          ...
          // 使用树形穿梭框组件
          <tree-transfer :title="title" :from_data='fromData' :to_data='toData' :defaultProps="{label:'label'}"             @addBtn='add' @removeBtn='remove' :mode='mode' height='540px' filter openAll>
          </tree-transfer>
        </div>
      </template>  
      <script>
      import treeTransfer from 'el-tree-transfer' // 引入

        export defult {
          data(){
            return:{
              mode: "transfer", // transfer addressList
              fromData:[
                {
                  id: "1",
                  pid: 0,
                  label: "一级 1",
                  children: [
                    {
                      id: "1-1",
                      pid: "1",
                      label: "二级 1-1",
                      children: []
                    },
                    {
                      id: "1-2",
                      pid: "1",
                      label: "二级 1-2",
                      children: [
                        {
                          id: "1-2-1",
                          pid: "1-2",
                          children: [],
                          label: "二级 1-2-1"
                        },
                        {
                          id: "1-2-2",
                          pid: "1-2",
                          children: [],
                          label: "二级 1-2-2"
                        }
                      ]
                    }
                  ]
                },
              ],
              toData:[]
            }
          },
          methods:{
            // 切换模式 现有树形穿梭框模式transfer 和通讯录模式addressList
            changeMode() {
              if (this.mode == "transfer") {
                this.mode = "addressList";
              } else {
                this.mode = "transfer";
              }
            },
            // 监听穿梭框组件添加
            add(fromData,toData,obj){
              // 树形穿梭框模式transfer时，返回参数为左侧树移动后数据、右侧树移动后数据、移动的        {keys,nodes,halfKeys,halfNodes}对象
              // 通讯录模式addressList时，返回参数为右侧收件人列表、右侧抄送人列表、右侧密送人列表
              console.log("fromData:", fromData);
              console.log("toData:", toData);
              console.log("obj:", obj);
            },
            // 监听穿梭框组件移除
            remove(fromData,toData,obj){
              // 树形穿梭框模式transfer时，返回参数为左侧树移动后数据、右侧树移动后数据、移动的{keys,nodes,halfKeys,halfNodes}对象
              // 通讯录模式addressList时，返回参数为右侧收件人列表、右侧抄送人列表、右侧密送人列表
              console.log("fromData:", fromData);
              console.log("toData:", toData);
              console.log("obj:", obj);
            }
          },
          comporents:{ treeTransfer } // 注册
        }
      </script>
      <style>
      ...
      </style>

# 文档
--- 



参数：width 说明：宽度 类型：String 必填：false 默认：100% 补充：建议在外部盒子设定宽度和位置
参数：height 说明：高度 类型：String 必填：false 默认：320px
参数：title 说明：标题 类型：Array 必填：false 默认：["源列表", "目标列表"]
参数：button_text 说明：按钮名字 类型：Array 必填：false 默认：空
参数：from_data 说明：源数据 类型：Array 必填：true 补充：数据格式同element-ui tree组件，但必须有id和pid
参数：to_data 说明：目标数据 类型：Array 必填：true 补充：数据格式同element-ui tree组件，但必须有id和pid
参数：defaultProps 说明：配置项-同el-tree中props 必填： false 补充：用法和el-tree的props一样
参数：node_key 说明：自定义node-key的值，默认为id 必填：false 补充：必须与treedata数据内的id参数名一致，必须唯一
参数：pid 说明：自定义pid的参数名，默认为"pid" 必填：false 补充：有网友提出后台给的字段名不叫pid，因此增加自定义支持
参数：leafOnly 说明：是否只返回叶子节点 类型：Boolean 必填：false 补充：默认false，如果你只需要返回的末端子节点可使用此参数
参数：filter 说明：是否开启筛选功能 类型：Boolean 必填：false
参数：openAll 说明：是否默认展开全部 类型：Boolean 必填：false
参数：renderContent 说明：自定义树节点 类型：Function 必填：false 补充：用法同element-ui tree
参数：mode 说明：设置模式，字段可选值为transfer|addressList 类型：String 必填：false 补充：mode默认为transfer模式，即树形穿梭框模式，可配置字段为addressList改为通讯录模式，通讯录模式时按钮不可自定义名字，如要自定义标题名在title数组传入四个值即可，addressList模式时标题默认为通讯录、收件人、抄送人、密送人
参数：transferOpenNode 说明：穿梭后是否展开穿梭的节点 类型：Boolean 必填：false 补充：默认为true即展开穿梭的节点，便于视觉查看，增加此参数是因为数据量大时展开会有明显卡顿问题，但注意，如此参数设置为false则穿梭后不展开，毕竟无法确定第几层就会有庞大数据
参数：defaultCheckedKeys 说明：默认展开节点 类型：Array 必填：false 补充：只匹配初始时默认节点，不会在你操作后动态改变默认节点
参数：placeholder 说明：设置搜索框提示语 类型：String 必填：false 补充：默认为请输入关键词进行筛选
参数：defaultTransfer 说明：是否自动穿梭一次默认选中defaultCheckedKeys的节点 类型：Boolean 必填：false 补充：默认false，用来满足用户不想将数据拆分成fromData和toData的需求
参数：arrayToTree 说明：是否开启一维数组转化为树形结构 类型：Boolean 必填：false 补充：数据必须存在根节点，并且不会断节，数据格式详见github上app.vue，根据id、pid对应关系转化，存在一定的性能问题
参数：addressOptions 说明：通讯录模式配置项{num: Number, suffix: String, connector: String} 类型：Object 必填：false 补充：num-> 所需右侧通讯录个数,默认3 suffix-> label后想要拼接的字段（如id，即取此条数据的id拼接在后方）默认suffix connector -> 连接符（字符串）默认-
参数：lazy 说明：是否启用懒加载 类型：Boolean 必填：false 补充：默认false，效果动el-tree懒加载，不可和openAll或默认展开同时使用
参数：lazyFn 说明：懒加载的回调函数 类型：Function 必填：true 补充：当适用lazy时必须传入回调函数，示例:lazyFn='loadNode',返回参数loadNode(node, resolve, from), node->当前展开节点node，resolve->懒加载resolve，from -> left|right 表示回调来自左侧|右侧
事件：addBtn 说明：点击添加按钮时触发的事件 回调参数：function(fromData,toData,obj),树形穿梭框transfer模式分别为1.移动后左侧数据，2.移动后右侧数据，3.移动的节点keys、nodes、halfKeys、halfNodes对象；通讯录addressList模式时返回参数为右侧收件人列表、右侧抄送人列表、右侧密送人列表
事件：removeBtn 说明：点击移除按钮时触发的事件 回调参数：function(fromData,toData,obj),树形穿梭框transfer模式分别为1.移动后左侧数据，2.移动后右侧数据，3.移动的节点keys、nodes、halfKeys、halfNodes对象；通讯录addressList模式时返回参数为右侧收件人列表、右侧抄送人列表、右侧密送人列表
事件：left-check-change 说明：左侧源数据勾选事件 回调参数：function(nodeObj, treeObj)见el-tree组件check事件返回值
事件：right-check-change 说明：右侧目标数据勾选事件 回调参数：function(nodeObj, treeObj)见el-tree组件check事件返回值
Slot：left-footer, right-footer 说明：穿梭框左侧、右侧底部slot
Slot: title-left, title-right 说明：穿梭框标题区左侧、右侧自定义内容












