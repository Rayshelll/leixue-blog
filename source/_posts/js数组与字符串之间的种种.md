---
title: js数组与字符串之间的种种
date: 2019-08-16 13:17:23
tags: 
- JavaScript
categories: 前端学习
---
#### js常用数组的方法：
##### [数组](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)
不会改变原来数组的有：
`toString()`  数组转字符串
`number.toString(2)`  数字转二进制数，默认是十进制
`toLocalString()`  数组转字符串
`concat()`  返回一个由当前数组和其它若干个数组或者若干个非数组值组合而成的新数组
`join("连接符")`  连接所有数组元素组成一个字符串。
`slice(start,end)`  从start开始切割，到位置`end-1`没有参数复制一个数组
`indexOf()`  返回数组中第一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1
`fill(0, 2, 4))`  将数组中指定区间2-4的所有元素的值，都替换成某个固定的值0
`some()`  如果数组中至少有一个元素满足测试函数，则返回 true，否则返回 false。
`includes()`  判断当前数组是否包含某指定的值，如果是返回 true，否则返回 false。
`every(条件)`  检测数组元素的每个元素是否都符合条件，如果都符合条件返回 true，否则返回 false。
`some()`  检测数组元素中是否有元素符合指定条件，如果一个符合条件返回 true，否则返回 false。
`filter()`  检测数组元素，并返回符合条件所有元素的数组。

<!-- more -->

会改变原来数组的有：
`pop()` 删除数组的最后一个元素，并返回这个元素。
`shift()` 删除数组的第一个元素，并返回这个元素。
`push()` 添加元素到数组的末尾，并返回这个元素
`unshift()` 在数组的开头增加一个或多个元素，并返回数组的新长度。
`splice(pos, n, item1,.....,itemX)` 通过从索引pos开始删除n个元素，在删除位置按顺序添加新元素item1,.....,itemX
`sort()` 对数组元素进行排序，默认升序，并返回当前数组。
``` js
// V8 引擎 sort 函数只给出了两种排序 InsertionSort 和 QuickSort，数量小于10的数组使用 InsertionSort，比10大的数组则使用 QuickSort。
// 升序
arr.sort((a, b) => a - b)
// 降序
arr.sort((a, b) => b - a)
// 属性排序
arr.sort(compare(property));
function compare(property){
    return function(a, b){
        var value1 = a[property];
        var value2 = b[property];
        return value1 - value2
    }
}

```
`reverse()` 颠倒数组中元素的排列顺序

#### 字符串方法：
##### [字符串](https://www.w3school.com.cn/js/js_obj_string.asp)
`str.charAt(index)`	返回在指定位置的字符。
`str.concat(str1)`	连接字符串。
`str.match(regExp)`	找到一个或多个正则表达式的匹配。找到的返回一个数组(多个值)，没找到返回null
`str.replace(regExp, "替换字符")`	替换与正则表达式匹配的子串。
`str.replace(/\s/g, '%20')`    `\s` 匹配任何空白字符(不加/g，只匹配找到的第一个)
`str.search(regexp)` 	检索与正则表达式相匹配的值。 没有匹配返回-1
`str.indexOf()`     返回某个指定的字符串值在字符串中首次出现的位置。没有匹配到返回 -1。
`str.lastIndexOf()` 返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。
`str.split("分隔符")`  分割字符串转为数组
`str.slice(start, end)`	 提取字符串的片断，并在新的字符串中返回被提取的部分。
`str.substr(start, length)`  从起始索引号提取字符串中指定数目的字符。
`str.substring(start, stop)`	提取字符串中两个指定的索引号之间的字符，不接受负数。
`toLocaleLowerCase()`	把字符串转换为小写。
`toLocaleUpperCase()`	把字符串转换为大写。
`toLowerCase()`	 把字符串转换为小写。
`toUpperCase()`	 把字符串转换为大写。
`toString()`   返回字符串
`valueOf()`	 返回字符串对象的原始值。

#### 数字、字符串、数组
判断数据类型：`typeof()` `number` `string` `boolean` `function` `undefined`  `object`
``` js
typeof(NaN) //number
```
判断类型： `a instanceof b` 就是判断一个实例是否属于某种类型，`instanceof` 可以在继承关系中用来判断一个实例是否属于它的父类型
``` js
function Foo(){}
function Bar(){}
Bar.prototype = new Foo()
let obj = new Bar()
obj instanceof Bar //true
obj instanceof Foo //true

Number instanceof Number //false
String instanceof String //false
Object instanceof Object //true
Function instanceof Function //true
Function instanceof Object //true
function Foo(){};
Foo instanceof Function //true
Foo instanceof Foo //false
```
是不是数字：`Number(str)` / `!isNaN(str)`
数字转字符串：`x.toString()`
字符串转数字：`parseInt(str)`
字符串转数组：`str.split("")`
数组转字符串：`arr.join("")`/`arr+=''`
字符串可以以数组的形式取里面的字符，字符串也是对象

