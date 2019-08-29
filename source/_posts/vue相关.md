---
title: vue相关
date: 2019-08-19 16:12:22
tags: 
- Vue
---
### 难点
1. vue-resource数据请求
2. promise回调
3. props、`watch`监听属性变化
4. render

<!-- more -->

#### 子组件向父组件传值
事件调用机制：父向子传递方法，父定义事件名，子调用这个方法（使用`$emit("事件名"，传的值)`调用），同时把数据当作参数传递给这个方法

#### 父组件向子组件传值
父组件里属性绑定`:a=""`，子组件里`props:["a"]`接收值（可使用watch来监听值的改变）

标签内使用`ref="box"`属性，可以拿到标签原生dom对象
`this.$refs.box`
v-on @ 时间绑定
v-bind : 数据单向绑定
v-model input 数据双向绑定
    ``` js
    <template>
    //渲染模版
    </template>
    // 组件的名称、数据、方法、子组件
    <script>
    export default {
        name:"",
        data(){
        return {
        
        }
        },
        created(){},
        methods: {
        
        },
        components:{}
    }
    </script>
    //样式
    <style lang="scss" scoped>

    </style>
    ```