---
title: js相关知识
date: 2019-08-19 16:04:14
tags: JavaScript
---
### [JS作用域和作用域链](https://www.cnblogs.com/hfxm/p/5547922.html)
#### 作用域就是变量和函数的可访问范围，或者说变量或函数起作用的区域。
1. javascript函数的作用域：
函数内的区域，就是这个函数的作用域，变量和函数在这个区域都可以访问操作。最外层函数外的区域叫全局作用域，函数内的区域叫局部作用域。
2. javascript变量的作用域：
在源代码中变量所在的区域，就是这个变量的作用域，变量在这个区域内可以被访问操作。在全局作用域上定义的变量叫全局变量，在函数内定义的变量叫局部变量。

#### 作用域链
作用域链（Scope Chain）是javascript内部中一种变量、函数查找机制，它决定了变量和函数的作用范围，即作用域。每个作用域都有一条对应的作用域链，链头是全局作用域，链尾是当前函数作用域。作用域链的作用是保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到`window`对象即被终止，作用域链向下访问变量是不被允许的。
<!-- more -->
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
#### 1. 闭包：函数可以使用函数之外定义的变量（例如：使用全局变量）, 闭包就是能够读取其他函数内部变量的函数。
创建闭包最常见方式，就是在一个函数内部创建另一个函数。
闭包的简单实例
``` js
function fun(){
    let a=1,b=6;
    function fn(){//闭包
        return a+b;
    }
    return fn;//闭包函数
}
let myfun = fun();
myfun();
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


### js同步和异步的区别
javascript语言是一门“单线程”的语言，所谓单线程就是按次序执行，执行完一个任务再执行下一个。同步和异步的差别就在于这单线程上各个流程的`执行顺序不同`。
- 同步：在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；
- 异步：不进入主线程、而进入"任务队列"（task queue）的任务，自己做自己的任务，只有等主线程任务执行完毕，自己下面的任务也做完了，"任务队列"开始通知主线程，请求执行任务，该任务才会进入主线程执行。
- 在JS中，异步编程只有四种情况：
    - 定时器都是异步编程的，setTimeout和setInterval函数；setTimeout(function(){ alert("Hello"); }, 3000);
    - 所有的事件绑定都是异步编程的，click事件等；
    - Ajax读取数据都是异步编程的，我们一般设置为异步编程；
    - 回调函数callback都是异步编程的；

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
        }
    }
    window.o.fn();
    ```
4. 情况4：如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值不是一个对象那么this还是指向函数的实例。
    ``` js
    function fn()  
    {  
        this.user = '追梦子';  
        return 1;
    }
    var a = new fn;  
    console.log(a.user); //追梦子

    function fn()  
    {  
        this.user = '追梦子';  
        return function(){};
    }
    var a = new fn;  
    console.log(a.user); //undefined
    ```
    ``` js
    function Fn(){
        this.user = "追梦子";
    }
    var a = new Fn();
    console.log(a.user); //追梦子
    ```
`补充`：在严格版中的默认的this不再是window，而是undefined。

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
    ```



