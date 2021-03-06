---
title: ES6
date: 2019-08-19 16:05:58
tags:
- JavaScript
---
### JS ES6简介
ECMAScript 6 简称 ES6，是 JavaScript 语言的下一代标准，已经在2015年6月正式发布。
新特性：
1. `let`、`const`块级作用域
    - var 都可以换成let
    - 不存在变量提升：只能先声明在使用
    - 暂时性死区：只在自己的块级里面作用，出自己的块就不作用了
    - 不允许重复声明
    - 函数可以在块级里声明，加‘use strict’就不行了
2. `import`导入模块、`export`导出模块
3. ES6引入`class`(构造函数）、`extends`(继承)、`super`(原型)
    ``` js
    class Rectangle {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }
    }
    //extends继承 super()子类调用父类方法，超类
    ```
4. `arrow functions `（箭头函数）不需要 function 关键字来创建函数，省略 return 关键字，继承当前上下文的 this 关键字
    - 相当于函数使用bind()
    - `() => {}`
5. `template string `（模板字符串）用` `${name}` `嵌入
6. `destructuring` （解构）解构能让我们从对象或者数组里取出数据存为变量
    ``` js
    // 对象和数组逐个对应表达式
    //数组
    let arr = [1,2]
    var [x,y] = arr //一一对应，只多不少
    console.log(x,y) // 1, 2
    //对象
    var o = {p: 42, q: true};
    var {p, q} = o;
    console.log(p); // 42
    console.log(q); // true
    //嵌套解构
    //解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。
    ```
7. `default `函数默认参数
    ``` js
    function multiply(a, b = 1) {
        return a * b;
    }
    multiply(5, 2); // 10
    multiply(5);  // 5
    multiply(5, undefined); // 5 传undefined使用默认值
    ```
8. `rest arguments `（rest参数\剩余参数：拿到除开始参数外的参数）
    ``` js
    //剩余参数是真正的 Array实例，也就是说你能够在它上面直接使用所有的数组方法，比如 sort，map，forEach或pop
    function(a, b, ...theArgs) {
    // ...
    }
    ```
9. `Spread Operator`（展开运算符）(...person)对数组而言
    ``` js
    var arr1=['a','b','c'];
    var arr2=[...arr1,'d','e']; //['a','b','c','d','e']
    ```
10. 对象初始化简写
    ``` js
    let a = 3
    let obj = {
        a: a,
        b: 'b',
        func: function () {
            console.log(this.a,this.b)
        }
    }
    //简写 对象简写减少了重复代码，故其在基于对象的MVVM框架中被广泛应用。例如vue
    let a = 3
    let obj = {
        a,
        b:'b',
        func(){
            console.log(this.a, this.b)    // 3  b
        }
    }
    ```
11. `Promise`：用同步的方式去写异步代码 reject(), resolve()，`Promise`承诺将来的某个时候调用success函数或fail函数。
    Promise是一个立即执行函数，但是他的成功（或失败：reject）的回调函数resolve却是一个异步执行的回调。当执行到resolve()时，这个任务会被放入到回调队列中，等待调用栈有空闲时事件循环再来取走它。
    （在JavaScript的世界中，所有代码都是单线程执行的。由于这个“缺陷”，导致JavaScript的所有网络操作，浏览器事件，都必须是异步执行。）
    `Promise` 是一个对象，它代表了一个异步操作的最终完成或者失败
    ``` js
    //Promise构造函数执行时立即调用executor 函数，resolve 和 reject 两个函数作为参数传递给executor
    new Promise( function(resolve, reject) {...} /* executor */  );
    ```

    三种状态：
    1. `pending`: 初始状态，既不是成功，也不是失败状态；
    2. 调用resolve函数来将promise状态改成`fulfilled`；
    3. 调用reject 函数将promise的状态改为`rejected`。executor函数中抛出一个错误，那么该promise状态为`rejected`；

    ``` js
    const promise = new Promise((resolve, reject) => {//该构造函数接收两个函数作为参数，分别是resolve和reject。
    // do something here ...
    if (success) {
        resolve(value); // fulfilled
    } else {
        reject(error); // rejected
    }
    });
    promise.then(function(value) {
      // fulfilled时的回调函数
    }, function(error) {
        // rejected时的回调函数
    });
    ```

    `async`函数
    想要某个函数拥有promise功能，只需让其返回一个promise即可。`return new Promise((resolve, reject) => {}`
    当调用一个 `async` 函数时，会返回一个 `Promise `对象。当这个 async 函数返回一个值时，Promise 的 resolve 方法会负责传递这个值；当 async 函数抛出异常时，Promise 的 reject 方法也会传递这个异常值。
    async 函数中可能会有 `await` 表达式，这会使 async 函数暂停执行，等待 Promise  的结果出来，然后恢复async函数的执行并返回解析值（resolved）。
    注意， `await` 关键字仅仅在 `async function` 中有效。

12. `Generators`：生成器（ generator）是能返回一个迭代器的函数。
13. `set`与`map`数据集合
    Set是无重复值的有序列表。Set会自动移除重复的值，因此你可以使用它来过滤数组中重复的值并返回结果。
    Set的方法有：`.add(key)` `.has(key)` `.size` `.delete(key)` `.clear()`  `forEach()`
    ``` js
    //Set通过new Set()来创建，调用add()方法就可以向Set中添加项目。检查size属性还能查看其中包含多少项。使用has()方法来测试某个值是否存在于set中
    let set = new Set();
    set.add(5);
    set.add("5");
    set.has(5);//true
    console.log(set.size);//2

    //Set不会使用强制类型转换来判断值是否重复。还可以向Set添加多个对象，他们不会被合并为同一项。
    let key1 = {};
    let key2 = {};
    set.add(key1);
    set.add(key2);
    console.log(set.size);//2

    //使用delete()方法来移除单个值或者调用clear()方法将所有值从Set中移除
    let set = new Set([1, 2, 3, 4, 5, 2, 6, 5, 5, "5"]);
    console.log(set);
    set.delete(5);
    console.log(set.has(5));//false
    set.clear();
    console.log(set.size);//0

    //Set 上的forEach()方法
    let set = new Set([1, 2]);
    set.forEach(function(value, key, ownerSet) {
        console.log(`${key} ${value}`)
        console.log(ownerSet === set);
    })

    //将Set转换为数组
    let arr = [1,2,4,3,2,5,5];
    let set = new Set(arr);
    let arr1 = [...set];
    console.log(arr1);
    ```

    Map是有序的键值对，其中的键允许是任何类型
    Map的方法有：`.has(key)` `.get(key)` `.set(key, value)` `.delete(key)` `.clear()` `.size`

    ``` js
    //Map初始化
    let map = new Map([
        ["name", "cc"],
        ["age", 26]
    ]);

    console.log(map.has("name"));//true
    console.log(map.get("name"));//cc
    console.log(map.has("age"));//true
    console.log(map.get("age"));//26
    console.log(map.size);//2

    //Map上的forEach()方法
    let map = new Map([
        ["name", "cc"],
        ["age", 26]
    ]);

    //Map set方法
    map.set(key, value)
    map.forEach(function(value, key, source) {
        console.log(`${key}的值是${value}`);
        console.log(source === map);
    })
    ```
14. 装饰器 Decorator
装饰器（Decorator）是一种与类（class）相关的语法，用来注释或修改类和类方法。装饰器是一种函数，写成`@ + 函数名`。它可以放在类和类方法的定义前面。装饰器是在编译阶段运行
1. 类的装饰:装饰器可以用来装饰整个类。
装饰器是一个对类进行处理的函数。装饰器函数的第一个参数，就是所要装饰的目标类。
``` js
@testable 
class MyTestableClass {
  // ...
}

function testable(target) {
  target.isTestable = true;
}

MyTestableClass.isTestable // true
/*@testable就是一个装饰器。它修改了MyTestableClass这个类的行为，为它加上了静态属性isTestable。testable函数的参数target是MyTestableClass类本身。*/

@decorator
class A {}
// 等同于
class A {}
A = decorator(A) || A;
```
传递参数的修饰器函数，可以在装饰器外面再封装一层函数。
``` ts
function testable(isTestable) {
  return function(target) {
    target.isTestable = isTestable;
  }
}

@testable(true)
class MyTestableClass {}
MyTestableClass.isTestable // true

@testable(false)
class MyClass {}
MyClass.isTestable // false
```
添加实例属性，可以通过目标类的prototype对象操作。
``` ts
function testable(target) {
  target.prototype.isTestable = true;
}

@testable
class MyTestableClass {}

let obj = new MyTestableClass();
obj.isTestable // true
```