---
title: js链表
date: 2019-08-08 18:04:56
tags: 
- JavaScript
categories: 前端学习
---
### [链表](<https://juejin.im/entry/59cb70995188256aa423b680>)
链表是一个对象{}，有`element`、`next`、`previou`等属性；

#### 单向链表
链表包含两个类，一个是 Node 类用来表示节点，element属性表示节点数据，next属性表示指向后驱节点的链接，另一个 LinkedList 类提供插入节点、删除节点等一些操作。
``` js
// 节点类，用来生成节点
function Node(value) {
    this.value = value;
    this.next = null;
}

//链表类
function LinkList() {
    this.head = null;
    this.pushNode = pushNode;//向链表尾部追加元素
    this.getSize = getSize;//获得链表长度
    this.printNode= printNode;//打印链表
    this.findNode = findNode; //查找节点
    this.insertNode = insertNode; //插入节点 
    this.findPrevNode = findPrevNode; //插入节点
    this.removeNode = removeNode; //删除节点 
    
}

//向链表尾部追加元素
function pushNode(value) {
    var node = new Node(value);
    if (this.head == null) {
        this.head = node;
    } else {
        var currNode = this.head;
        while (currNode.next != null) {
            currNode = currNode.next;//查找尾节点
        }
        currNode.next = node;
    }
}


//获得链表长度
function getSize(){
    var i=0;
    if (this.head == null){
        return 0;
    }else {
        var currNode = this.head;
        while (currNode.next != null){
            currNode = currNode.next;
            i++;
        }
    }
    return i;
}

//打印链表
function printNode(){
    if (this.head == null){
        return null
    }else {
        var currNode = this.head;
        while(currNode.next != null){
            console.log(currNode.value);
            currNode = currNode.next;
        }
    }
}

//查找节点
function findNode(value){
    if (this.head == null){
        return null
    }else {
        var currNode = this.head
        while (currNode.value != value){
            currNode = currNode.next
            if(currNode.next == null){//查找到最后没有对应的节点
                return null
            }
        }
        return currNode
    }
}

//插入节点
function insertNode(newValue, item){
    var newNode = new Node(newValue)
    if (this.findNode(item)){
        var currNode = this.findNode(item);
        newNode.next = currNode.next
        currNode.next = newNode
    }
    
}

//查找指定值的上一个节点
function findPrevNode(item){
   if (this.head.value == item){ //查找的前一节点为head的前节点
       return null
   }else{
        var currNode = this.head
        while (currNode.next.value != item){
            currNode = currNode.next
        }
        return currNode
   }
    
    
}
//删除节点，前提节点就存在
function removeNode(item){
    if (this.findPrevNode(item)){
        var deletePrevNode = this.findPrevNode(item);
        deletePrevNode.next = deletePrevNode.next.next;
    }else{
        this.head = this.head.next //删除头结点
    }
    
}
//用例测试
var list = new LinkList();
for (var i = 1; i < 6; i++) {
    list.pushNode(i);
}
list.printNode();
console.log(list.findPrevNode(2));
// list.insertNode("11", 8)
list.removeNode(1);
list.printNode();

```
#### 双向链表
给Node类增加一个previous属性，让其指向前驱节点的链接，这样就形成了双向链表
``` js
//节点类
function Node(element) {
    this.element = element;   //当前节点的元素
    this.next = null;         //下一个节点链接
    this.previous = null;     //上一个节点链接
}
//链表类
function LinkList() {
    this.head = null;
    // 查找、打印等方法和单向链表差不多，可以直接使用
    this.insertNode = insertNode; //插入节点 
    this.removeNode = removeNode; //删除节点 
    this.dispReverse = dispReverse; //反向显示链表
}

function insertNode(newItem, item){
    var newNode = new Node(newItem);
    var currNode = this.findNode(item);
    newNode.previous = currNode;
    newNode.next = currNode.next;
    currNode.next = newNode;
}

function removeNode(item){
    var deleteNode = this.findNode(item);
    //删除节点不是表头也不是表尾
    if (deleteNode.next != null){
        //变换指针
        deleteNode.previous.next = deleteNode.next;
        deleteNode.next.previous = deleteNode.previous;
        //删除节点前后指针置null
        deleteNode.next = null;
        deleteNode.previous = null;
    }
    //删除节点是表头
    if (eleteNode == this.head){
        this.head = this.head.next
    }
    //删除节点是表尾
    if (deleteNode.next == null){
        deleteNode.previous = null
    }
}

function dispReverse(){
    var findLastNode = function(){
        var currNode = this.head;
        while (currNode.next != null){
            currNode = currNode.next
        }
        return currNode
    }
    var node = findLastNode();
    while(node.previous != null){
        node = node.previous
    }
}
```

#### 循环链表：单向循环链表和双向循环链表
多了一个head的指向
`this.head.next = this.head;`