---
title: 原生js
date: 2019-09-05 21:37:37
tags:
- JavaScript
---
#### 使用原生js给一个按钮绑定onclick事件
``` js
var btn = document.getElementById("btn");
btn.addEventListener("click",hello1);
function hello1(){
 alert("hello 1");
}

```

#### 怎样添加、移除、移动、复制、创建和查找节点？
``` js
// 创建新节点
createDocumentFragment() //创建一个DOM片段
createElement() //创建一个具体的元素
createTextNode() //创建一个文本节点
// 添加、移除、替换、插入
appendChild() //添加
removeChild() //移除
replaceChild() //替换
insertBefore() //插入
// 查找
getElementsByTagName() //通过标签名称
getElementsByName() //通过元素的Name属性的值
getElementById() //通过元素Id，唯一性
```