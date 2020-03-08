---
title: js数组与字符串之间的种种
date: 2019-08-16 13:17:23
tags: 
- JavaScript
categories: 前端学习
---
#### js常用数组的方法：
##### [数组](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)
1. 不会改变原来数组的有：
`toString()`  数组转字符串，返回字符串
`number.toString(2)`  十进制数字转二进制数，返回二进制数（不含符号位）
`toLocalString()`  数组转字符串
`toString()`和`toLocaleString()`两点区别：
``` js
//当数字是四位数及以上时，有区别
var a=1234
a.toString()//"1234"
a.toLocaleString()//"1,234"

//当目标是标准时间格式时，有区别
var day=new Date() //"Thu Mar 05 2020 14:44:11 GMT+0800 (GMT+08:00)"
day.toLocaleString()//2020-3-5 14:44:11
day.toString()//"Thu Mar 05 2020 14:44:11 GMT+0800 (GMT+08:00)"
day.toLocaleDateString()//2020-3-5
day.toUTCString()//Thu, 05 Mar 2020 06:44:11 GMT
```
`concat()`  数组连接数组或非数组，返回连接后的新数组
`join("连接符")`  连接所有数组元素，返回连接后的字符串
`slice(start,end)`  从start开始切割，到位置`end-1`，没有参数则复制数组，返回新数组
`indexOf()`  返回数组中第一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1
`lastIndexOf()`  返回数组中最后一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1
`fill(0, 2, 4))`  将数组中指定区间2-4的所有元素的值，都替换成某个固定的值0，返回新数组
`includes()`  判断当前数组是否包含某指定的值，如果是返回 true，否则返回 false。
`every(条件函数)`  检测数组元素的每个元素是否都符合条件，如果都符合条件返回 true，否则返回 false（只遍历到出结果位置）
`some(条件函数)`  检测数组元素中是否有元素符合指定条件，如果一个符合条件返回 true，否则返回 false（只遍历到出结果位置）
`filter(条件函数)`  过滤数组元素，返回符合条件所有元素的新数组
``` js
//every some filter也是数组遍历的一种形式
var arr=[1,2,3,1,5];
var b=arr.every(function(item,index,arr){
    console.log( 'item=' + item + ',index='+index+',array='+arr ); 
    return arr[index]%2==0
})
console.log(b)//item=1,index=0,array=1,2,3,1,5 false
```

2. 会改变原来数组的有：
`pop()` 删除数组的最后一个元素，返回这个元素
`shift()` 删除数组的第一个元素，返回这个元素
`push()` 在数组的末尾添加一个或多个元素，返回数组长度
`unshift()` 在数组的开头添加一个或多个元素，返回数组的新长度
`splice(pos, n, item1,.....,itemX)` 通过从索引pos开始删除n个元素，在删除位置按顺序添加新元素item1,.....,itemX，返回删掉的部分
`reverse()` 颠倒数组中元素的排列顺序，返回颠倒后的数组
`sort()` 对数组元素进行排序，默认升序，返回排序后的数组
``` js
// V8 引擎 sort 函数只给出了两种排序 InsertionSort 和 QuickSort，数量小于10的数组使用 InsertionSort，比10大的数组则使用 QuickSort。
// 升序
arr.sort((a, b) => a - b)
// 降序
arr.sort((a, b) => b - a)
// 属性排序 升序
arr.sort(compare(property));
function compare(property){
    return function(a, b){
        var value1 = a[property];
        var value2 = b[property];
        return value1 - value2
    }
}

```

#### 字符串方法：
##### [字符串](https://www.w3school.com.cn/js/js_obj_string.asp)
`str.charAt(index)`	返回在指定位置的字符。
`str.concat(str1)`	连接字符串。
`str.match(regExp)`	找到一个或多个正则表达式的匹配，若不是全局搜索只匹配第一个，返回一个结果数组，没找到返回null
`str.replace(regExp, "替换字符")`	替换与正则表达式匹配的子串，若不是全局搜索只替换第一个，返回新的字符串
`str.search(regexp)` 	检索与正则表达式相匹配的值，返回第一个找的值得索引，没有匹配返回-1
`str.indexOf()`     返回某个指定的字符串值在字符串中首次出现的索引，没有匹配到返回 -1
`str.lastIndexOf()` 返回一个指定的字符串值最后出现的索引，在一个字符串中的指定位置从后向前搜索，没有匹配到返回 -1
`str.split("分隔符")`  分割字符串转为数组，返回数组
`str.slice(start, end)`	 提取字符串的片断，返回被提取的字符串
`str.substr(start, length)`  从起始索引号提取字符串中指定数目的字符，返回字符串
`str.substring(start, stop)`	提取字符串中两个指定的索引号之间的字符，不接受负数，返回字符串
`toLocaleLowerCase()`	把字符串转换为小写。最好使用这个
`toLowerCase()`	 把字符串转换为小写。两者针对部分地区语言Unicode大小写映射不同
`toLocaleUpperCase()`	把字符串转换为大写。
`toUpperCase()`	 把字符串转换为大写。
`toString()`   返回字符串
`valueOf()`	 返回字符串对象的原始值。

#### 数字、字符串、数组
基本数据类型：
基本类型（保存值）：`Number` `String` `boolean`  `undefined` `null` 和 引用类型（保存地址）：`Object` `Function` `Array`
1. 判断数据类型：`typeof()` 可以判断`number` `string` `boolean` `undefined` `function`；不可以判断：`array`与`object`、`null`与`object`；返回数据类型是字符串表达式
``` js
//typeof 可判断number string boolean function undifined
//但不能判断array和object null和object
typeof(NaN) //number
typeof([1,2]) //object
typeof(null) //object
```
2. 判断类型：`instanceof` 判断对象的具体类型；可以判断`undefined`和`null`
`a instanceof b` 就是判断一个实例是否属于某种类型
``` js
//继承关系中用来判断一个实例是否属于它的父类型
function Foo(){}
function Bar(){}
Bar.prototype = new Foo()
let obj = new Bar()
obj instanceof Bar //true
obj instanceof Foo //true

//判断数据类型
Number instanceof Number //false
String instanceof String //false
Object instanceof Object //true
Function instanceof Function //true
Array instanceof Array //true
Array instanceof Object //true
Function instanceof Object //true
function Foo(){};
Foo instanceof Function //true
Foo instanceof Foo //false
```
3. 其他
    - 是不是数字：`Number(str)` / `!isNaN(str)`
4. 转换
    - 数字转字符串：`x.toString()`
    - 字符串转数字：`parseInt(str)`
    - 字符串转数组：`str.split("")`
    - 数组转字符串：`arr.join("")`/`arr+=''`
    - 字符串可以以数组的形式取里面的字符，字符串也是可迭代对象（Array,string,Map,Set）

