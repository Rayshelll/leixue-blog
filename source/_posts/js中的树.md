---
title: js中的树
date: 2019-08-16 13:17:50
tags: JavaScript
categories: 前端学习
---
#### [js树](https://juejin.im/entry/59979aaaf265da24817a5928)
树是一种**非顺序数据结构**（节点，根节点，内部节点，外部节点，子树，深度）

**节点**包括（key left right）

**二叉搜索树**是二叉树的一种，左节点key值`<`父节点key值，右节点key值`>=`父节点key值

四种遍历的主要思想：
前序遍历：根左右;
中序遍历：左根右;
后序遍历：左右根;
广度遍历：按照层次一层层遍历;

<!-- more -->

``` js
// 创建一个树节点
function Node(key){
    this.key = key;
    this.left = null;
    this.right = null;
}
// 创建树的类
function treeList(){
    this.root = new Node('root'); // 根节点
    this.insertNode = insertNode; // 插入节点
    this.findNode = findNode; // 查找节点
    this.removeNode = removeNode; // 删除节点
    this.finMaxNode = findMaxNode; // 这棵树中的最小值在最后一层最左侧的节点
    this.findMinNode = findMinNode; // 最大值在最右端的节点。

    //先序遍历 主左右 先序遍历的一种应用是打印一个结构化的文档。
    this.preOrderTraverseNode = preOrderTraverseNode;
    // 中序遍历 左主右 是一种上行访问BST所有节点的遍历方式，也就是从最小到最大的顺序访问所有节点。中序遍历的一种应用就是对树进行排序操作。
    this.inOrderTraverseNode = inOrderTraverseNode;
    // 后序遍历 左右主 后序遍历的一种应用是计算一个目录和它的子目录中所有文件所占用空间的大小。
    this.postOrderTraverseNode = postOrderTraverseNode;
}

function insertNode(node, root){
    if (root === null){
        root = node;
    }else{
        if (node.key < root.key){
            if (root.left == null){
                root.left = node
            }else {
                insertNode(node, root.left)
            }
        }else {
            if (root.right == null){
                root.right = node
            }else {
                insertNode(node, root.right)
            }
        }
    }
}

function findNode(node, key){
    if (node == null){
        return false
    }else {
        if (key < node.key){
            return findNode(node.left, key)
        }else if(key > node.key) {
            return findNode(node.right, key)
        }else{
            return true
        }
       
    }
}

function findMaxNode(node){
    if (node){
        while(node && node.right !== null){
            node = node.right
        }
        return node.key
    }else{
        return null
    }
}

function findMinNode(node){
    if (node){
        while(node && node.left !== null){
            node = node.left
        }
        return node
    }else{
        return null
    }
}

// 三种情况：删除节点没有子节点，删除节点有一个子节点，删除节点有两个子节点，从node来删除
function removeNode(node, key){
    if (node === null){
        return null;
    }
    if (key < node.key){
        node.left = removeNode(node.left, key)
        return node
    }else if (key > node.key){
        node.right = removeNode(node.right, key)
        return node
    } else {
        // 找到删除的节点，删除，分三种情况
        // case1 删除节点没有子节点
        if (node.left === null && node.right === null){
            node = null;
            return node;
        }
        //case 2 删除节点有一个子节点
        if (node.left === null){
            node = node.right;
            return node;
        } else if (node.right === null){
            node = node.left;
            return node;
        }
        //case 3 删除节点有两个子节点，最复杂，用该右子树的最小节点aux的值代替删除节点值de，并删除aux
        var aux = findMinNode(node.right);// findMinNode返回的是节点
        node.key = aux.key;
        node.right = removeNode(node.right, aux.key);
        return node;
    }
}

// 回调函数用来定义我们对遍历到的每个节点进行操作
// 先序中左右
function preOrderTraverseNode(node, callback){
    if (node !== null) {
        callback(node.key)
        preOrderTraverseNode(node.left, callback)
        preOrderTraverseNode(node.right, callback)
    }
}
// 中序遍历左中右
function inOrderTraverseNode(node, callback){
    if (node !== null) {
        inOrderTraverseNode(node.left, callback);
        callback(node.key)
        inOrderTraverseNode(node.right, callback)
    }
}
// 后序遍历左右中
function postOrderTraverseNode(node, callback){
    if (node !== null) {
        postOrderTraverseNode(node.left, callback);
        postOrderTraverseNode(node.right, callback)
        callback(node.key)
    }
}
```
``` js
// 用例测试，树用object来表示
// 普通二叉树
let obj = {
    key: 10,
    left: {
        key: 11, 
        left: {
            key: 21, 
            left: {
                key: 31, 
                left: null,
                right: null
            },
            right: {
                key: 32,
                left: null,
                right: null
            }
        }, 
        right: {
            key: 22,
            left: null,
            right: null
        }
    },
    right: {
        key: 12,
        left: {
            key: 23,
            left: null,
            right: null
        },
        right: {
            key: 24,
            left: null,
            right: null
        }
    }
}
// 搜索二叉树
let treeObj = {
    key: 14,
    left: {
        key: 12, 
        left: {
            key: 9, 
            left: {
                key: 6, 
                left: null,
                right: null
            },
            right: null
        }, 
        right: {
            key: 13,
            left: null,
            right: null
        }
    },
    right: {
        key: 16,
        left: {
            key: 10,
            left: null,
            right: null
        },
        right: {
            key: 20,
            left: {key: 18, left: null, right: null},
            right: {key: 21, left: null, right: null}
        }
    }
}
var tree = new treeList();
// tree.preOrderTraverseNode(obj, console.log)
// tree.inOrderTraverseNode(obj, console.log)
// tree.postOrderTraverseNode(obj, console.log)


// console.log(tree.findMinNode(treeObj)) // 6
// console.log(tree.findNode(treeObj, 6)) // true
var node = new Node(30)
// tree.insertNode(node, treeObj)
// tree.inOrderTraverseNode(treeObj, console.log)
tree.removeNode(treeObj, 20)
tree.inOrderTraverseNode(treeObj, console.log)
// console.log(treeObj)
```