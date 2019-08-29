---
title: 2019.8.18bytedance
date: 2019-08-19 16:09:08
tags: 面试
categories: 面试总结
---
1. 自我介绍
2. 项目或是实习项目介绍，遇到的问题，怎么解决的？
3. 技术问题：
    - 讲讲进程和线程
    - http和tcp的关系？
    - HTTPS怎么加密的，加密方法
    - 哪些方法优化前端性能，优化渲染性能？
<!-- more -->
4. 编程：
    - (算法基础) 用递归编写一个函数，计算 n 个数字的和，n >= 0。要求：不能使用循环；必须使用尾递归；算法复杂度为O(n)
    ``` js
    // 尾递归，进入下一个函数不再需要上一个函数的环境了，得出结果以后直接返回。
    function fn(n){
        if (n==1) return 1; // 终点
        return fn(n-1) + n; // 递归关系
    }
    console.log(fn(4));
    ```
    - (数据结构) 使用链表实现一个队列，可以向队尾插入(push)数据，并按照插入顺序获取(shift)数据。
    ``` js 
    function Node(ele){
    this.ele = ele;
    this.next = null;
    }
    function LinkList(){
        this.head = null;
        this.push = push;
        this.print = print;
    }
    function push(item){
        var node = new Node(item);
        if (this.head == null){
            this.head = node;
        }else {
            var currNode = this.head;
            while (currNode.next != null){
                currNode = currNode.next;
            }
            currNode.next = node;
        }
    }
    function print(){
        var currNode = this.head;
        while (currNode.next != null){
            console.log(currNode.ele);
            currNode = currNode.next;
        }
    }

    var list = new LinkList();
    for (var i = 1; i < 6; i++) {
        list.push(i);
    }
    list.print();
    ```
    - 下面代码打印出啥，使用闭包怎么改善
    ``` js
    for(var i = 0, len = 5; i< len; i++){
      setTimeout({console.log('No.' + i)}, 0);
      console.log(i);
    }
    //先打印出0 1 2 3 4 
    // NO.5 NO.5 NO.5 NO.5 NO.5 NO.5 setTimeout是异步执行的，0毫秒后向任务队列里添加一个任务，只有主线上的全部执行完才会执行任务队列里的任务，所以当主线程for循环执行完之后 i 的值为5，这个时候再去任务队列中执行任务，i全部为5；
    //解决办法： var i 换成 let i 的是区块变量，每个i只能存活到大括号结束，并不会把后面的for循环的  i  值赋给前面的setTimeout中的i；而var i  则是局部变量，这个 i 的生命周期不受for循环的大括号限制
    ```