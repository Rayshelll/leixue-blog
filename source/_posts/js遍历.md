---
title: js遍历
date: 2019-08-16 13:09:54
tags: 
- JavaScript
categories: 前端学习
---
#### js遍历
##### `for` 可迭代对象（包括 `Array` `string`)
``` js
for(let i; i<object.length; i++){
    object[i]
}
```

<!-- more -->

##### `for...of`语句在可迭代对象（包括 `Array` `Map(let a = new Map([['a', 1], ['b', 2], ['c', 3]]);)` `Set(let a= new Set([1, 1, 2, 2, 3, 3]);) ` `String` `TypedArray(let a = new Uint8Array([0x00, 0xff]);)` `arguments`对象等等）可以正确响应 `break` `continue` `return` 语句
```js
for(let item of object){
    item
}
```
##### `for...in`可迭代对象（包括 Array,string)，会遍历object的所有属性，性能差
```js
for(var i in object){
    object[i]
}
```
##### `map`创建一个新数组，使用原数组的数据，对每个数组进行操作，return新数组
```js
Array.map(item, index, Array){
    return 
}
Array.map(function(item, index, object))

```
#### `forEach`对原数组进行操作改变原数组，return undefined
``` js
Array.forEach(item, index, Array){
    item/array[index]
}
Array.forEach(function)
```
#### 返回过滤后条件满足item的条件的新数组
```js
array.filter(item => item%2==0)
```

##### reduce 遍历 initialValue初始值，求和initialValue=0积initialValue=1等
``` js
arr.reduce(function(total, currentValue, currentIndex, arr){}, initialValue)
```