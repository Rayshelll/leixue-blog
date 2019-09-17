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

##### `reduce`为数组中的每一个元素依次执行回调函数`callback`，不包括数组中被删除或从未被赋值的元素，接受四个参数：(初始值（或者上一次回调函数的返回值），当前元素值，当前索引，调用 reduce 的数组)。
``` js
arr.reduce(callback,[initialValue])
/* callback （执行数组中每个值的函数，包含四个参数）
    1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
    2、currentValue （数组中当前被处理的元素）
    3、index （当前元素在数组中的索引）
    4、array （调用 reduce 的数组）
initialValue （作为第一次调用 callback 的第一个参数。）
*/
```
1. reduce的简单用法：数组求和，求乘积
``` js
var  arr = [1, 2, 3, 4];
var sum = arr.reduce((x,y)=>x+y, 0)
var mul = arr.reduce((x,y)=>x*y, 1)
console.log( sum ); //求和，10
console.log( mul ); //求乘积，24
```

2. reduce的高级用法：
    - 计算数组中每个元素出现的次数
    ``` js
    let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];
    // 初始值为{}
    let nameNum = names.reduce((pre, cur)=>{
    if(cur in pre){
        pre[cur]++
    }else{
        pre[cur] = 1 
    }
    return pre
    }, {})
    console.log(nameNum); //{Alice: 2, Bob: 1, Tiff: 1, Bruce: 1}
    ```

    - 数组去重
    ``` js
    let arr = [1,2,3,4,4,1]
    let newArr = arr.reduce((pre,cur)=>{
        if(!pre.includes(cur)){ // 当前值不再前面的数组里
        return pre.concat(cur)
        }else{
        return pre
        }
    },[])
    console.log(newArr);// [1, 2, 3, 4]
    ```

    - 二维降一维
    ``` js
    let arr = [[0, 1], [2, 3], [4, 5]]
    let newArr = arr.reduce((pre,cur)=>{
        return pre.concat(cur)
    },[])
    console.log(newArr); // [0, 1, 2, 3, 4, 5]
    ```

    - 多维降一维
    ``` js
    let arr = [[0, 1], [2, 3], [4,[5,[6],7]]]
    const newArr = function(arr){
    return arr.reduce((pre,cur)=>{
        return pre.concat(Array.isArray(cur) ? newArr(cur) : cur)
        }, [])
    }
    console.log(newArr(arr)); //[0, 1, 2, 3, 4, 5, 6, 7]
    ```

    - 对象里的属性求和
    ``` js
    var result = [
        {
            subject: 'math',
            score: 10
        },
        {
            subject: 'chinese',
            score: 20
        },
        {
            subject: 'english',
            score: 30
        }
    ];

    var sum = result.reduce(function(prev, cur) {
        return cur.score + prev;
    }, 0);
    console.log(sum) //60
    ```