---
title: js相关知识
date: 2019-08-19 16:04:14
tags: 
- JavaScript
---
### [JS作用域和作用域链](https://www.cnblogs.com/hfxm/p/5547922.html)
#### 作用域就是变量和函数的可访问范围，或者说变量或函数起作用的区域。
1. javascript函数的作用域：
函数内的区域，就是这个函数的作用域，变量和函数在这个区域都可以访问操作。最外层函数外的区域叫全局作用域，函数内的区域叫局部作用域。
2. javascript变量的作用域：
在源代码中变量所在的区域，就是这个变量的作用域，变量在这个区域内可以被访问操作。在全局作用域上定义的变量叫全局变量，在函数内定义的变量叫局部变量。

#### 作用域链
作用域链（Scope Chain）是javascript内部中一种变量、函数查找机制，它决定了变量和函数的作用范围，即作用域。每个作用域都有一条对应的作用域链，链头是全局作用域，链尾是当前函数作用域。作用域链的作用是保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到`window`对象即被终止，作用域链向下访问变量是不被允许的。

### [JS原型和原型链](https://baijiahao.baidu.com/s?id=1594082266903998359&wfr=spider&for=pc)
1. 函数对象
所有引用类型（函数，数组，对象）：拥有`__proto__`属性（隐式原型）
所有函数：拥有`prototype`属性（显式原型）（仅限函数）
原型对象：拥有prototype属性的对象，在定义函数时就被创建
2. 构造函数
**实例p的隐式原型**指向它**构造函数Person()的显式原型**，指向的意思是恒等于
`p.__proto__ === Person.prototype`
3. 原型和原型链
查找属性，如果本身没有，通过__proto__向上进行查找，也就是它构造函数的prototype中调用查找，最终到null结束，如果没有则返回undefined。
    - `p.__proto__.constructor == function Person(){}`
    - `p.___proto__.__proto__== Object.prototype`
    - `p.___proto__.__proto__.__proto__== Object.prototype.__proto__ == null`
    - **原型链**通过`__proto__`形成而非`protrotype`

### js闭包、继承
#### 1. 闭包：闭包就是能够读取函数之外定义的变量或其他函数内部变量的函数。简单理解成“定义在一个函数内部的函数”。
#### 优点和缺点？
1. 优点：
    - 能够读取函数内部的变量 
    - 可以使变量长期保存在内存中，生命周期比较长。
2. 缺点：
    - 内存消耗：读取的变量一直存在于内存中，不会在调用结束后，被垃圾回收机制回收，内存消耗很大（解决办法是，退出函数之前，将不使用的局部变量删除，将引用变量指向null变成垃圾对象，等待回收。）
    - 性能问题：使用闭包时，会涉及到跨作用域访问，每次访问都会导致性能损失。（解决方法：通过把跨作用域变量存储在局部变量中，然后直接访问局部变量，来减轻对执行速度的影响。）
创建闭包最常见方式，就是在一个函数内部创建另一个函数。
闭包的简单实例
``` js
function outer(n) {
    function inner(m) {//闭包
        return n + m;
    }
    return inner;//闭包函数
}
outer(1)(2)//3
```

#### 2. 继承：创建的子类将继承超类的所有属性和方法，包括构造函数及方法的实现。子类还可添加超类中没有的新属性和方法，也可以覆盖超类的属性和方法。继承的方式：
1. 借用构造函数继承：用.call()和.apply()将父类构造函数引入子类函数；call() 方法：`B.call(A, args1,args2)`;即A对象调用B对象的方法；apply() 方法：用作 this 的对象和要传递给函数的参数的数组 `B.apply(A, arguments)`;即A对象应用B对象的方法
``` js
function Animal(){
    this.species = 'animal';
    this.jump = function(){

    };
}
function Cat(name){
    Animal.call(this,args1,args2);//Animal.apply(this,[])
    this.name = name;
}
var cat1 = new Cat("大毛");　　
alert(cat1.jump()); // 动物
```

2. 原型链继承
``` js
function Animal(){
    this.species = 'animal';
    this.jump = function(){

    };
}
function Cat(name){
    this.name = name;
}

Cat.prototype = new Animal();//这样就能继承父类原型上的属性了，但是存在更改父类原型的问题
Animal.prototype.color = "d";
var cat1=new Cat("张");  
cat.jump(); 
cat.color;//使用构造函数是继承不了的
```
3. 混合方式：组合继承（组合原型链继承和借用构造函数继承）
``` js
function Animal(){
    this.species = 'animal';
    this.jump = function(){

    };
}
function Cat(name){
    Animal.call(this,args1,args2);
    this.name = name;
}

Cat.prototype = Object.create(Animal.prototype);//创建一个父类的原型对象，并返回这个新对象
Cat.prototype.constructor = Cat;

var cat1=new Cat("张");  
cat1.jump(); 
cat1.color;//使用构造函数是继承不了的
console.log(cat1 instanceof Animal) //true
```
4. 对象冒充
``` js
function Animal(){
    this.species = 'animal';
    this.jump = function(){

    };
}
function Cat(name){
    this.newMethod = Animal;//为 Animal 赋予了方法 newMethod（请记住，函数名只是指向它的指针）。
    this.newMethod();//        然后调用该方法
    delete this.newMethod;//所有新属性和新方法都必须在删除了新方法的代码行后定义。否则，可能会覆盖超类的相关属性和方法

    this.name = name;
}
```
5. 寄生式继承
es5实现继承

### 深拷贝与浅拷贝
浅拷贝：是指只复制一层对象，当对象的属性是引用类型时，实质复制的是其引用，当引用指向的值改变时也会跟着变化（`就是假设B复制了A，当修改A时，B也变化了）`
深拷贝：是指复制对象的所有层级`（当修改A时，B没变化）`。
实现方法
- 通过递归实现，递归去复制所有层级属性
- 通过JSON解析实现，借用JSON对象的parse和stringify
- 借用JQuery的extend方法

### click和onclick的区别
click 是方法，由程序员写语句调用；onclick是事件；
click本身是方法作用是触发onclick事件，只要执行了元素的click()方法，就会触发onclick事件；`方法触发事件`

### JS 的引用赋值与传值赋值
`number`,`string`类型都是基本类型是通过传值赋值的，而基本类型存放在栈区，访问时按值访问，赋值是按照普通方式赋值；
`Object`和`Array`是通过引用来赋值的，所以改变arr1的同时arr2也会跟着改变;

### js内存泄漏
内存泄漏可以定义为一个应用，由于某些原因不再需要的内存没有被操作系统或者空闲内存池回收。3种常见的JavaScript泄漏
1. 意外的全局变量 
2. 被遗忘的计时器`setTimeout`或回调`calback`
3. 超出DOM引用
4. 闭包

### js改变this指向的方法
#### [`this`的指向](https://www.cnblogs.com/pssp/p/5216085.html)
1. 情况1：如果一个函数中有this，但是它没有被上一级的对象所调用，那么this指向的就是window。
    ``` js
    var x=1;
    console.log(this.x);//输出 1
    console.log(this);////Window
    ```
    ``` js
    var x=1;
    function fn(){
        var x=2;
        console.log(this.x);//输出 1
        console.log(this);////Window
    }
    fn();
    ```
2. 情况2：如果一个函数中有this，这个函数有被上一级的对象所调用，那么this指向的就是上一级的对象。
    ``` js
    var o = {
        user:"追梦子",
        fn:function(){
            console.log(this.user);  //追梦子 
            console.log(this);  //this指向o这个对象
        }
    }
    o.fn();
    ```
3. 情况3：如果一个函数中有this，这个函数中包含多个对象，尽管这个函数是被最外层的对象所调用，this指向的也只是它上一级的对象。
    ``` js
    var o = {
        user:"追梦子",
        fn:function(){
            console.log(this.user); //追梦子
            console.log(this);  //this指向o这个对象
        }
    }
    window.o.fn();
    ```
4. 情况4：如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值不是一个对象或者不存在返回对象那么this还是指向函数的实例。
    ``` js
    //有返回值，返回值不是对象
    function fn()  
    {  
        this.user = '追梦子';  
        return 1;
    }
    var a = new fn;  
    console.log(a.user); //追梦子 

    //有返回值，返回值是对象
    function fn()  
    {  
        this.user = '追梦子';  
        return function(){};
    }
    var a = new fn;  
    console.log(a.user); //undefined 

    //无返回值
    function Fn(){
        this.user = "追梦子";
    }
    var a = new Fn();
    console.log(a.user); //追梦子 
    ```
`补充`：在严格版中的默认的this不再是window，而是undefined。
例题：
``` js
var length = 10;
function fn(){
    console.log(this.length)
}
var obj = {
    length:5,
    method:function (fn){
        fn(); // 这里fn没有被上级调用, this指向window
        arguments[0]()//调用fn，这里this指向arguments，arguments.0()
    }
}
obj.method(fn)
obj.method(fn,123)
/*
arguments = {
    0: fn, //也就是 functon() {alert(this.length)} 
    1: 第二个参数, //没有 
    2: 第三个参数, //没有
    ..., 
    length: 1 //只有一个参数
}
*/
```

#### 改变this指向的三种方法：`call()`, `apply()`,`bind()`
1. bind:不会调用本函数,而是生成一个新的函数,这个函数的代码逻辑和原函数一样,但是this指向不一样，指向`.bind(window)`window
    ``` js
    var name = 'sally';
    function sayName(){
        return this.name;
    }
    function sayName2(){
        return this.name
    }
    var o = {
        'name':'John',
        sayName:sayName,
        sayName2:sayName2.bind(window)
    };
    console.log(o.sayName()); //John
    console.log(o.sayName2());//sally   
    ```
2. call和apply:
    - 相同点：call和apply均可以改变this指向，
    - 不同点：call接受的参数为一个一个的，但是apply接受的参数只能为一个严格的数组`test.call(obj,1,3);` `test.apply(obj,[1,3]);`都指向obj
    ``` js
    var name = 'sally';
    function sayName(){
        return this.name;
    }
    var o = {
        'name':'John',
        sayName:sayName
    };
    sayName();
    sayName.call(o,1,3);
    ayName.apply(o,[1,2,3])
    ```

### 事件机制之冒泡、捕获、传播和委托。
DOM事件流（event flow ）存在三个阶段：`事件捕获阶段`、`处于目标阶段`、`事件冒泡阶段`。
`事件捕获`（event capturing）：通俗的理解就是，当鼠标点击或者触发dom事件时，浏览器会从根节点开始由外到内进行事件传播，即点击了子元素，如果父元素通过事件捕获方式注册了对应的事件的话，会先触发父元素绑定的事件。
`事件冒泡`（dubbed bubbling）：与事件捕获恰恰相反，事件冒泡顺序是由内到外进行事件传播，直到根节点。
dom标准事件流的触发的先后顺序为：先捕获再冒泡，即当触发dom事件时，会先进行事件捕获，捕获到事件源之后通过事件传播进行事件冒泡。

### js匿名函数与普通函数
    ``` js
    //匿名函数
    var getSize = function(){
        
    }
    getSize();
    //普通函数
    function getSize(){}
    //注意：普通函数可以在任意位置调用，匿名函数只能在函数声明之后调用

    //立即调用函数
    (function(a, b){
    console.log(a + b);
    })(1, 2)
    ```

### js同步和异步的区别
javascript语言是一门“单线程”的语言，所谓单线程就是按次序执行，执行完一个任务再执行下一个。同步和异步的差别就在于这单线程上各个流程的`执行顺序不同`。
- 同步任务：在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；
- 异步任务：不进入主线程、而进入"任务队列"（task queue）的任务，自己做自己的任务，只有等主线程任务执行完毕，自己下面的任务也做完了，"任务队列"开始通知主线程，请求执行任务，该任务才会进入主线程执行。
- 在JS中，异步编程只有四种情况：
    - 定时器都是异步编程的，`setTimeout`和`setInterval`函数；setTimeout(function(){ alert("Hello"); }, 3000);
    - 所有的事件绑定都是异步编程的，`click`事件等；
    - `Ajax`读取数据都是异步编程的，我们一般设置为异步编程；
    - 回调函数`callback`都是异步编程的；

### 浏览器的eventloop（javascript的执行机制new Promise和setTimeout执行顺序）
`event loop`顾名思义就是事件循环，为什么要有事件循环呢？因为javascript是单线程的，即同一时间只能干一件事情，一般先执行主线程里的同步任务，将异步任务加入到一个callback queue事件队列里(task), 等到同步任务事件完成时，会读取callback queue队列中的函数，进入主线程执行，上述过程会不断重复，也就是常说的Event Loop(事件循环)。

`setTimeout`和`Promise`调用的都是异步任务，都是通过任务队列进行管理／调度，任务队列分为：`MacroTask Queue(宏任务队列)`和`MicroTask Queue(微任务队列)`
宏任务队列主要包括`setTimeout`,`setInterval`, `setImmediate`, `requestAnimationFrame`, NodeJS中的`I/O`,UI渲染等
微任务队列主要包括两类：
独立回调microTask：如`Promise`，其成功／失败回调函数相互独立；
复合回调microTask：如 Object.observe, MutationObserver 和NodeJs中的 `process.nextTick` ，不同状态回调在同一函数体；
`先执行微任务，再执行宏任务`
``` js
setTimeout(function() {
    console.log(1)
}, 0)
new Promise(function executor(resolve) {
    console.log(2)
    for (var i=0; i< 10000; i += 1){
        i == 9999 && resolve()
    }
    console.log(3)
}).then(function() {
    console.log(4)
})
process.nextTick(function() {
    console.log(6);
})
console.log(5)
// 2 3 5 6 4 1
```
- 这段代码作为宏任务进入主线程，首先会遇到`setTimeout`，将其回调函数分发到宏任务的`event queue`上；
- 然后回到`promise`，`new promise`会立即执行，`then`函数分发到微任务的`event queue`中， 记为`process 2`； process.nextTick 永远大于 promise.then
- 接下来`process.nextTick`分发到微任务的`event queue`中，记为`process 1`；
- 接下来遇到`console.log（）`立即执行；
- 然后，整体script代码作为第一个宏任务执行结束，接下来判断是否有微任务，我们发现then在微任务event queue里，执行；
- 第一轮循环事件结束，开始第二轮循环，当然是从宏任务的event queue开始，我们发现了宏任务event queue中的`setTimeout`对应的回调函数，则立即执行。
``` js
console.log('1'); 

setTimeout(function() {
    console.log('2');
    process.nextTick(function() {
        console.log('3');
    })
    new Promise(function(resolve) {
        console.log('4');
        resolve();
    }).then(function() {
        console.log('5')
    })
})
process.nextTick(function() {
    console.log('6');
})
new Promise(function(resolve) {
    console.log('7');
    resolve();
}).then(function() {
    console.log('8')
})

setTimeout(function() {
    console.log('9');
    process.nextTick(function() {
        console.log('10');
    })
    new Promise(function(resolve) {
        console.log('11');
        resolve();
    }).then(function() {
        console.log('12')
    })
})
// 1 7 6 8     2 4 3 5    9 11 10 12
```

#### JavaScript中Null和Undefined的区别
null: null是js中的关键字，表示空值，null可以看作是object的一个特殊的值，如果一个object值为空，表示这个对象不是有效对象。
Undefined: undefined不是js中的关键字，其是一个全局变量，是Global的一个属性，以下情况会返回undefined:
- 使用了一个未定义的变量；var i;
- 使用了已定义但未声明的变量；
- 使用了一个对象属性，但该属性不存在或者未赋值；
- 调用函数时，该提供的参数没有提供：
- 函数没有返回值时，默认返回undefined
Null和Undefined的区别
相同点：都是原始类型的值，保存在栈中变量本地
不同点：
1. null表示定义并赋值为null，undifined表示定义未赋值
2. 类型不一样：
``` js
console.log(typeOf undefined);//undefined
console.log(typeOf null);//object
```
3. 转化为值时不一样：undefined为NaN ,null为0
``` js
console.log(Number(undefined));//NaN
console.log(Number(10+undefined));//NaN
 
console.log(Number(null));//0
console.log(Number(10+null));//10
```
4. 
``` js
console.log(undefined===null);//false
console.log(undefined==null);//true)
```
5. null当使用完一个比较大的对象时，需要对其进行释放内存时，设置为null;
``` js
var arr=["aa","bb","cc"];
arr=null;//释放指向数组的引用
```

### async/await 来处理异步
async/是一个立即执行函数
async/ await来发送异步请求，从服务端请求接口，获取数据。
async是一个关键字，放到函数前面，用于表示函数是一个异步函数， 异步函数也就意味着该函数的执行不会阻塞后面代码的执行。
``` js
async function timeout(){
    return 'hello'
}
timeout();//调用，不影响后面的代码执行；调用了但没执行
console.log(timeout()) // 返回的是一个promise对象
console.log('hello,world!')
//要获取到promise返回值，我们应该用then 方法
timeout().then(result => {
    console.log(result)
})

async function timeout(flag) {
    if (flag) {
        return 'hello world' // 返回一个值时，Promise 的 resolve 方法会负责传递这个值
    } else {
        throw 'my god, failure' // 抛出异常时，Promise 的 reject 方法也会传递这个异常值
    }
}
console.log(timeout(true))  // 调用Promise.resolve() 返回promise 对象。
console.log(timeout(false)); // 调用Promise.reject() 返回promise 对象。
// 抛出错误用.catch()进行捕获
timeout(false).catch(err => {
    console.log(err)
})
```
await是等待的意思，能在async或是返回对象是Promise的一个函数里使用，使用await关键字是等待后面的Promise对象执行完毕，然后拿到promise resolve的值并进行返回，返回值拿到之后，它继续向下执行。
``` js
// async await promise 执行顺序
async function async1(){
    console.log('1')
    await async2()
    console.log('2')
}
async function async2(){
    console.log('3')
}
console.log('4')
setTimeout(function(){
    console.log('5') 
},0)  
async1();
new Promise(function(resolve){
    console.log('6')
    resolve();
}).then(function(){
    console.log('7')
})
console.log('8')
// 4 1 3 6 8 2 7 5
```

### 变量提升，函数提升
变量提升就是把变量的声明提升到所在作用域的顶端，赋值在代码原来的位置。所以var 声明的变量可以先使用再赋值。
var a = 2;实际上javascript引擎将这个声明分为var a和a = 2两个单独的声明，第一个是编译阶段的任务，而第二个则是执行阶段的任务。
``` js
console.log("1", v1);
var v1 = 100;
function foo() {
    console.log("2", v1);
    var v1 = 200;
    console.log("3", v1);
}
foo();
console.log("4", v1);
// 1 undefined
// 2 undefined  
// 3 200
// 4 100
// 实际执行顺序
var v1;
console.log("1", v1); // undefined
v1 = 100;
function foo() {
    var v1
    console.log("2", v1);// undefined
    v1 = 200;
    console.log("3", v1); // 200
}
foo();
console.log("4", v1); //100
```

函数提升：
函数提升是整个代码块提升到它所在的作用域的最开始执行；函数提升所指的形式：function fn(){......}；不能是不能是函数表达式的形式
``` js
console.log(f1);    //函数提升，整个代码块提升到文件的最开始<br>
f1();
console.log(f2);

function f1(){
  console.log('我是函数f1。。。');
}
var f2 = function () {
  console.log('我是函数f2。。。');
};
//函数提升的执行过程
/*
function f1(){
  console.log('我是函数f1。。。');
}
var f2;

console.log(f1);
f1();

f2 = function(){
  console.log('我是函数f2。。。');
}*/
```