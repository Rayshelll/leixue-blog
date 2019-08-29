---
title: js数组操作
date: 2019-08-16 13:17:01
tags: 
- JavaScript
categories: 前端学习
---
#### js去重
##### ES6数组去重，无法去{}空对象
``` js
let arr = ['1','hello','ree','ke','yi','1','e','1']
function unique(arr){
    return Array.from(new Set(arr))
}
console.log(unique(arr))
```
##### splice去重，一个数据和后面所有数据比较，splice(j,1)删除在j位置上的数据
``` js
function unique(arr){
    for (let i=0; i<arr.length; i++){
        for (let j=i+1; j<arr.length; j++){
            if (arr[i]==arr[j]){
                arr.splice(j,1)
                j--
            }
        }
    }
    return arr
}
```

<!-- more -->

##### 使用indexOf去重，新建一个数组，newarr.indexOf(arr[i])===-1（新数组里没有arr[i]这个值），不存在就push进去，存在的就跳过
``` js
function unique(arr){
    let newarr=[]
    for (let i=0; i<arr.length; i++){
        if(newarr.indexOf(arr[i])===-1){
            newarr.push(arr[i])
        }
    }
    return newarr
}
```
##### 使用sort去重，先将数组排序，然后前后数据相比较，不存在就push进新的数组
``` js
function unique(arr){
    let newarr=[]
    arr= arr.sort()
    for (let i=0; i<arr.length; i++){
        if(arr[i]!==arr[i+1]){
            newarr.push(arr[i])
        }
    }
    return newarr
```
#### js排序
##### js数组冒泡排序，相邻元素比较交换
``` js
let arr=[9,-2,1,30,-59]
function bubbleSort(arr){
    for(let i=0; i<arr.length-1; i++){
        for(let j=0; j<arr.length-1-i; j++){
            if (arr[j]>arr[j+1]){
                let temp=arr[j]
                arr[j]=arr[j+1]
                arr[j+1]=temp
            }
        }
    }
    return arr
}
console.log(bubbleSort(arr))
```
#### js降维
##### 二维数组变一维数组，遍历数组两遍，放入新数组
``` js
let arr=[[1,2,3],["sy",1,"jh",null],["",9],1]
function reduceArr(arr){
    let newarr=[]
    arr.forEach(item => {
        //判断是不是数组，是进入下一个判断，不是直接push
        item.forEach?item.forEach(val => {
        newarr.push(val)
        }):newarr.push(item)
    });
    return newarr
}
console.log(reduceArr(arr))
```
##### 用apply的特性，将数组作为参数展开传入新的空数组[]，再contact
``` js
function reduceArr(arr){
    let newarr=[]
    newarr=newarr.concat.apply(newarr,arr)
    return newarr
}
```
##### 使用ES6特性-扩展运算符将数组展开
``` js
function reduceArr(arr){
    let newarr=[]
    newarr=[].concat(...arr)
    return newarr  
}
```
##### 数组字符串化，二维和多维降维
``` js
let arr = [3, ['a', [0, 1], null], [4, '4j', [3]], -2]
function reduceArr(arr){
    arr += '';//多维数组变字符串3,a,0,1,,4,4j,3,-2
    arr = arr.split(',');//把一个字符串分割成字符串数组
    return arr
}
console.log(reduceArr(arr))
```
##### 多维数组变成一维数组，es6新增的flat方法
``` js
function reduceArr(arr){
    return arr.flat(3); 
}
```