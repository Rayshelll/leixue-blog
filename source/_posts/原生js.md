---
title: 原生js
date: 2019-09-05 21:37:37
tags:
- JavaScript
---
#### js事件监听方法的添加
`addEventListener()` 和 `removeEventListener()`是用来分配和删除事件的函数。 这两个方法都需要三个参数，分别为：事件名称（String）、要触发的事件处理函数(Function)、指定事件处理函数的时期或阶段(boolean)。
使用事件监听的原因：
``` js
elm.onclick = function( ) { //handler } 这样的写法兼容主流的浏览器，但是存在一个问题，当同一个elm绑定多个事件时，只有最后一个事件会被添加
elm.onclick = handler1;
elm.onclick = handler2;
elm.onclick = hander3;
//只有handler3会被添加执行，所以我们使用另外一种方法添加事件；
```
``` js
//IE：attachEvent
    elm.attachEvent("onclick",handler1);
    elm.attachEvent("onclick",handler2);
    elm.attachEvent("onclick",handler3);
    //三个方法执行的顺序是3 - 2  -1；
//标准:addEventListener( ):
    elm.addEventListener( "click",handler1,false );
    elm.addEventListener( "click",handler2,false );
    elm.addEventListener( "click",handler3,false );
    //执行的顺序：1 - 2 - 3 
//该方法的第三个参数是泡沫获取，是一个布尔值：当为false时表示由里向外：捕获阶段，true表示由外向里：冒泡阶段，DOM事件流捕获过程先于冒泡过程
```

``` js
var btn = document.getElementById("btn");
btn.addEventListener("click",hello1,false);
function hello1(){
 alert("hello 1");
}
btn.removeEventListener("click",hello1,false);

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