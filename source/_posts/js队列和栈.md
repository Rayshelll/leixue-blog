---
title: js队列和栈
date: 2019-08-16 13:16:30
tags: 
- JavaScript
categories: 前端学习
---
#### [js队列和栈](<https://segmentfault.com/a/1190000007360621>)
##### 队列和栈介绍
- 队列：先进先出，表尾插入，表头删除
- 栈：先进后出，表尾删除插入
- 栈与队列的相同点：
    1. 都是线性结构。
    2. 插入操作都是限定在表尾进行。
    3. 都可以通过顺序结构和链式结构实现。
    4. 插入与删除的时间复杂度都是O(1)，在空间复杂度上两者也一样。
    5. 多链栈和多链队列的管理模式可以相同。
##### 栈：LIFO 先入后出
在JavaScript中实现队列和数组主要是通过**数组**，js数组中提供了以下几个方法可以让我们很方便实现队列和堆栈:
##### 队列
* unshift: 头，在数组的开头添加一个或更多元素，并返回新的**长度**
* shift: 头，从数组中把第一个元素删除，（出队）并返回这个**元素的值**。
##### 栈
* push: 尾，在数组的中末尾添加元素，（入队，入栈）并返回新的**长度**
* pop: 尾，从数组中把最后一个元素删除，（出栈）并返回这个**元素的值**。

<!-- more -->

##### 通过javascript提供的API，实现栈
``` js
function Stack() {
    let items = [];

    this.push = function(element){
        items.push(element);
    };

    this.pop = function(){
        return items.pop();
    };

    this.peek = function(){
        return items[items.length-1];
    };

    this.isEmpty = function(){
        return items.length == 0;
    };

    this.size = function(){
        return items.length;
    };

    this.clear = function(){
        items = [];
    };

    this.print = function(){
        console.log(items.toString());
    };

    this.toString = function(){
        return items.toString();
    };

    this.min = function(){
    // 栈中所含最小元素
    return Math.min.apply(this, items)
    }
}
```
##### 通过javascript提供的API，实现队列
``` js
function Queue() {
    let items = [];

    this.enqueue = function(element){
        items.push(element);
    };

    this.dequeue = function(){
        return items.shift();
    };

    this.front = function(){
        return items[0];
    };

    this.isEmpty = function(){
        return items.length == 0;
    };

    this.clear = function(){
        items = [];
    };

    this.size = function(){
        return items.length;
    };

    this.print = function(){
        console.log(items.toString());
    };
}
```