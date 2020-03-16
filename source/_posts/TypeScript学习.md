---
title: TypeScript学习
date: 2020-03-12 17:02:10
tags: 
- js
---
#### TypeScript 是一种面向对象的编程语言。
面向对象主要有两个概念：对象和类。
**对象**：对象是类的一个实例，有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。
**类**：类是一个模板，它描述一类对象的行为和状态。
**方法**：方法是类的操作的实现步骤。

#### 基本数据类型
1. 任意类型：声明为 any 的变量可以赋予任意类型的值。
``` ts
let x: any = [1,3] 
x = 'hello'
```
2. 数字类型 `let index: number = 1;`（包括二进制、八进制、十进制、十六进制）
3. 字符串类型 `let name: string = "Runoob"`
4. 布尔值类型 `let flag: boolean = true;`
5. 数组类型 `let arr: number[] = [1, 2];`或者`let arr: Array<number> = [1, 2];`
6. 元组：元组类型用来表示已知元素数量和类型的数组，各元素的类型不必相同，对应位置的类型需要相同`let x: [string, number] = ['hello',1];`
7. 枚举:枚举类型用于定义数值集合。
``` ts
enum Color {Red, Green, Blue};
let c: Color = Color.Blue;
console.log(c);    // 输出 2
```
8. void ：用于标识方法返回值的类型，表示该方法没有返回值。
``` ts
function hello(): void {
    alert("Hello Runoob");
}
```
9. null
10. undefined
11. never:是其它类型（包括 null 和 undefined）的子类型，代表从不会出现的值。这意味着声明为 never 类型的变量只能被 never 类型所赋值。`let test: never;`

#### TypeScript 变量声明
1. 定义
语法格式：`var [变量名] : [类型] = 值;`
TypeScript 遵循强类型，如果将不同的类型赋值给变量会编译错误
`var num:number = "hello"`     // 这个代码会编译错误
2. 类型断言（Type Assertion）
类型断言可以用来手动指定一个值的类型，即允许变量从一种类型更改为另一种类型。
语法格式：`<类型>值` 或 `值 as 类型`
``` ts
var str = '1' 
var str2:number =<any> str   //str、str2 是 string 类型
var str3:number = str as any
console.log(str2,str3)
```
3. 类型推断
当类型没有给出时，TypeScript 编译器利用类型推断来推断类型`var num = 2`，类型推断为number，如果由于缺乏声明而不能推断出类型，那么它的类型被视作默认的动态any 类型。
4. 变量作用域
    - 全局作用域：全局变量定义在程序结构的外部，它可以在你代码的任何位置使用。
    - 类作用域：也可以称为字段，类变量声明在一个类里头，但在类的方法外面，该变量可以通过类的对象来访问，类变量也可以是静态的`static num = 10`，静态的变量可以通过类名直接访问。
    - 局部作用域：局部变量，局部变量只能在声明它的一个代码块（如：方法）中使用
``` ts
var global_num = 12          // 全局变量
class Numbers { 
   num_val = 13;             // 实例变量
   static sval = 10;         // 静态变量
   storeNum():void { 
      var local_num = 14;    // 局部变量
   } 
} 
console.log("全局变量为: "+global_num)  
console.log("静态变量为: "+Numbers.sval) 
var obj = new Numbers(); 
console.log("实例变量: "+obj.num_val)
```

#### TypeScrip与JavaScript一致的语法
1. TypeScript 运算符
2. TypeScript 条件语句
3. TypeScript 循环

#### TypeScript 函数
##### 普通函数：可定义函数类型，返回值的类型需要与函数定义的返回类型(return_type)一致。
``` ts
function greet():string { // 返回一个字符串
    return "Hello World" 
} 
greet()
```
- 带参数函数
``` ts
function add(x: number, y: number): number {
    return x + y;
}
console.log(add(1,2))
```
##### 带参数的函数：包括内容（可选参数、默认参数、剩余参数）
- 可选参数:在 TypeScript 函数里，如果我们定义了参数，则我们必须传入这些参数，除非将这些参数设置为可选，可选参数使用问号标识 ？
``` ts
function buildName(firstName: string, lastName: string) {
    return firstName + " " + lastName;
}
let result1 = buildName("Bob");                  // 错误，缺少参数
let result2 = buildName("Bob", "Adams", "Sr.");  // 错误，参数太多了
let result3 = buildName("Bob", "Adams");         // 正确
// 设置lastName为可选参数
// 可选参数必须跟在必需参数后面。 如果上例我们想让 firstName 是可选的，lastName 必选，那么就要调整它们的位置，把 firstName 放在后面。如果都是可选参数就没关系。
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}

let result1 = buildName("Bob");  // 正确
let result2 = buildName("Bob", "Adams", "Sr.");  // 错误，参数太多了
let result3 = buildName("Bob", "Adams");  // 正确
```
- 默认参数：我们也可以设置参数的默认值，这样在调用函数的时候，如果不传入该参数的值，则使用默认参数
``` ts
// 实例函数的参数 rate 设置了默认值为 0.50，调用该函数时如果未传入参数则使用该默认值：
// 参数不能同时设置为可选和默认
function calculate_discount(price:number,rate:number = 0.50) { 
var discount = price * rate; 
console.log("计算结果: ",discount); 
} 
calculate_discount(1000) // 500
calculate_discount(1000,0.30)// 300
```
- 剩余参数：
``` ts
function addNumbers(...nums:number[]) {  
    var i;   
    var sum:number = 0; 
    
    for(i = 0;i<nums.length;i++) { 
       sum = sum + nums[i]; 
    } 
    console.log(sum) 
 } 
 addNumbers(1,2,3) //6
 addNumbers(10,10,10,10,10)//50
```

##### 匿名函数、匿名函数自调用
``` ts
// 匿名函数
var res = function(a:number,b:number) { 
    return a*b;  
}; 
console.log(res(12,2))
// 匿名函数自调用
(function(a:number,b:number) { 
    return a*b;  
})(12,2)
```
##### 构造函数定义函数、递归函数、箭头函数（Lambda 函数）与JavaScript定义一致
``` ts
// 构造函数定义函数
var myFunction = new Function("a", "b", "return a * b"); 
var x = myFunction(4, 3); 
console.log(x);
// 递归函数
function factorial(number) {
    if (number <= 0) {         // 停止执行
        return 1; 
    } else {     
        return (number * factorial(number - 1));     // 调用自身
    } 
}; 
console.log(factorial(6));      // 输出 720
// 箭头函数 ( [param1, parma2,…param n] )=>statement或者{代码块};
// 我们可以不指定函数的参数类型，通过函数内来推断参数类型、无参数时可以设置空括号
var foo = (x:number)=>10 + x 
console.log(foo(100)) 
```

##### 函数重载
- 重载是方法名字相同，而参数不同，返回类型可以相同也可以不同。
- 每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。
``` ts
// 参数类型不同：
// 如果参数类型不同，则参数类型应设置为 any。
function disp(string):void; 
function disp(number):void;

// 参数数量不同：
// 参数数量不同你可以将不同的参数设置为可选。
function disp(n1:number):void; 
function disp(x:number,y:number):void;

//参数类型顺序不同：
function disp(n1:number,s1:string):void; 
function disp(s:string,n:number):void;
```

#### TypeScript的对象
##### 属性、方法与JavaScript一致的对象
1. Number
2. String
3. Array
##### 不同于JavaScript的对象
###### TypeScript 元组：存储不同数据类型的数组，any[] 类型的数组
``` ts
let x: [string, number] = ['hello',1];
let y: any[] = [10,"Runoob"];
let z = [10,"Runoob"];
```

###### TypeScript 联合类型
联合类型（Union Types）可以通过管道(`|`)将变量设置多种类型，赋值时可以根据设置的类型来赋值。
**注意**：只能赋值指定的类型，如果赋值其它类型就会报错。
``` ts
let val:string|number|string[]|number[] ;
val = 'hello';
val = 2;
val = [1,2];
val = ['a','b']
val = true; // 报错
```

###### TypeScript 接口
1. 定义：接口是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法。简单的来说就是一种集成的新数据类型，里面包括属性和方法
**注意**：需要注意接口不能转换为 JavaScript， 它只是 TypeScript 的一部分。
``` ts
// 接口语法 interface interface_name{}
// 抽象特征和方法的声明
interface IPerson { 
    firstName:string, 
    lastName:string, 
    sayHi: ()=>string ,
    commandline:string[]|string|(()=>string),// 也可以是联合类型

} 
// 具体的类对象去使用，实现
var customer:IPerson = { 
    firstName:"Tom",
    lastName:"Hanks", 
    sayHi: ():string =>{return "Hi there"},
    commandline: 'hello',//['a','b'] ():string =>{return "Hi there"}
} 
 
console.log("Customer 对象 ") 
console.log(customer.firstName) 
console.log(customer.lastName) 
console.log(customer.sayHi())  

// 接口中我们可以将数组的索引值和元素设置为不同类型，索引值可以是数字或字符串
interface ages { 
    [index:string]:number 
 } 
  
 var agelist:ages; 
 agelist["John"] = 15   // 正确 
```

2. 接口继承：接口可以通过其他接口来扩展自己。Typescript 允许接口继承多个接口。继承使用关键字` extends`。
    - 单接口继承语法格式：Child_interface_name extends super_interface_name
    - 多接口继承语法格式：Child_interface_name extends super_interface1_name, super_interface2_name,…,super_interfaceN_name
    继承的各个接口使用逗号 `,` 分隔。
``` ts
// 单接口继承
interface Person { 
   age:number 
} 
 
interface Musician extends Person { 
   instrument:string 
} 
 
var drummer = <Musician>{}; // var drummer : Musician{age:27,instrument:"Drums"} 
drummer.age = 27 
drummer.instrument = "Drums" 
console.log("年龄:  "+drummer.age)
console.log("喜欢的乐器:  "+drummer.instrument)
// 多接口继承
interface IParent1 { 
    v1:number 
} 
 
interface IParent2 { 
    v2:number 
} 
 
interface Child extends IParent1, IParent2 { } 
var Iobj:Child = { v1:12, v2:23} 
console.log("value 1: "+Iobj.v1+" value 2: "+Iobj.v2)
```

###### TypeScript 类
1. 类的定义：定义类的关键字为 class，后面紧跟类名，类可以包含以下几个模块（类的数据成员）：
    - 字段 − 字段是类里面声明的变量。字段表示对象的有关数据。
    - 构造函数 − 类实例化时调用，可以为类的对象分配内存。
    - 方法 − 方法为对象要执行的操作。
``` ts
class Car { 
// 字段
engine:string; 
// 构造函数
constructor(engine:string) { 
    this.engine = engine 
}  
// 方法
disp():void { 
    console.log("函数中显示发动机型号  :   "+this.engine) 
} 
} 
// 创建一个实例化对象
var obj = new Car("XXSY1")
// 访问属性
console.log("读取发动机型号 :  "+obj.engine)  
// 访问方法
obj.disp()
```
2. 类的继承：使用关键字 `extends`，子类除了不能继承父类的私有成员(方法和属性)和构造函数，其他的都可以继承。TypeScript 一次只能继承一个类，不支持继承多个类，但 TypeScript 支持***多重继承***（A 继承 B，B 继承 C）。
``` ts
class Root { 
   str:string; 
} 
// 单继承Child继承Root
class Child extends Root {
    disp():void { 
      console.log("haha:  "+this.str) 
   } 
} 
class Leaf extends Child {} // 多重继承，继承了 Child 和 Root 类
 
var obj = new Leaf(); 
obj.str ="hehe" 
console.log(obj.str)
console.log(obj.disp())
```

3. 继承类的方法重写：类继承后，子类可以对父类的方法重新定义，这个过程称之为方法的重写。
``` ts
class PrinterClass { 
   doPrint():void {
      console.log("父类的 doPrint() 方法。") 
   } 
} 
 
class StringPrinter extends PrinterClass { 
   doPrint():void { 
      super.doPrint() // 调用父类的函数, super 关键字是对父类的直接引用，该关键字可以引用父类的属性和方法。
      console.log("子类的 doPrint()方法。")
   } 
}
```

4. 访问控制修饰符：TypeScript 中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。
    - static：用于定义类的数据成员（属性和方法）为静态的，静态成员可以直接通过类名调用。
    - public（默认） : 公有，可以在任何地方被访问。
    - protected : 受保护，可以被其自身以及其子类和父类访问。
    - private : 私有，只能被其定义所在的类访问。
``` ts
class Encapsulate { 
    static num:number;
    stativ disp():void{
        console.log("num 值为 "+ Encapsulate.num)
    }
    str1:string = "hello" 
    private str2:string = "world" 
}
StaticMem.num = 12 // 初始化静态变量，可直接通过类名调用，不需要实例化对象调用
Encapsulate.disp() // 同理，调用静态方法
var obj = new Encapsulate() 
console.log(obj.str1)     // 可访问，str1为公有变量
console.log(obj.str2)   // 编译错误， str2 是私有的，只能被其定义所在的类访问。
```

5. 类和接口：类可以实现接口，使用关键字 implements
``` ts
// 定义接口
interface ILoan { 
   interest:number,
   x:string,
} 
// 使用 implements 实现类继承接口
class AgriLoan implements ILoan { 
   interest:number; // 必须的，将 interest 字段作为类的属性使用
   x:string; // 必须实现接口的所有成员
   rebate:number ;
   
   constructor(interest:number,rebate:number) { 
      this.interest = interest 
      this.rebate = rebate 
   } 
} 
 
var obj = new AgriLoan(10,1) 
console.log("利润为 : "+obj.interest+"，抽成为 : "+obj.rebate )
```
###### 接口和类的区别、联系
1. 不同点：
    - 接口不能直接实例化，要具体的类对象去使用实现。
    - 类是是用来描述事物以及他们的行为的，可以实例化。
    - 接口是定义一些公开的属性方法，这些属性方法是抽象的没有具体的内容，只是一个形式，不包含属性方法的实现。
    - 接口可以多继承，类只能单继承和多重继承。
    - 类定义可以在不同的源文件之间进行拆分。
2. 相同点：
    - 接口、类和结构都可以从多个接口继承。
    - 接口类似于抽象基类：继承接口的任何非抽象类型都必须实现接口的所有成员。
    - 接口和类都可以包含事件、索引器、属性。

###### TypeScript 对象
1.定义：TypeScript对象是包含一组键值对的实例。 值可以是标量、函数、数组、对象等（与js一致），示例如下：
``` ts
var sites = { 
    key1: "value1", // 标量
    key2: "value",  
    key3: function() {
        // 函数
    }, 
    sayHello1: function(){}, // 类型模板
    key4:["content1", "content2"] //集合
}
// 与js不一致，在对象中添加方法，JavaScript可以直接添加
sites.sayHello = function(){ return "hello";}
// 而Typescript添加对象必须是特定类型的实例。有了模板类型才不报错
sites.sayHello1 = function () {
    console.log("hello " + sites.key1);
};
sites.sayHello();

```

##### TypeScript 命名空间
1. 定义：命名空间一个最明确的目的就是解决重名问题。
2. 语法：TypeScript 中命名空间使用 `namespace` 来定义，语法格式如下：
    - 定义：
    ``` ts
    namespace SomeNameSpaceName { 
    export interface ISomeInterfaceName {      }  // 如果我们需要在外部可以调用 SomeNameSpaceName 中的类和接口，则需要在类和接口添加 export 关键字。
    export class SomeClassName {      }  
    }
    ```
    - 调用：
        - 要在另外一个命名空间调用SomeClassName的语法格式为：`SomeNameSpaceName.SomeClassName;`
        - 如果一个命名空间在一个单独的 TypeScript 文件中，则应使用三斜杠 /// 引用它，语法格式如下：
        /// <reference path = "SomeFileName.ts" />
3. 命名空间的嵌套：命名空间支持嵌套，即你可以将命名空间定义在另外一个命名空间里头。
``` ts
namespace namespace_name1 { 
    export namespace namespace_name2 {
        export class class_name {    } 
    } 
}
```
##### TypeScript 模块
ES6里的导入导出模块`export` `import`
``` ts
// 文件名 : SomeInterface.ts 
export interface SomeInterface { 
   // 代码部分
}
// 另一个文件
import shape = require("./SomeInterface"); 
```
##### TypeScript 声明文件
声明文件：解决引用其他第三方的 JavaScript 的库时发生的检查错误
``` ts
/* 
declare 定义的类型只会用于编译时的检查，编译结果中会被删除。
在 TypeScript 中，我们并不知道 $ 或 jQuery 是什么东西，当然现在有人给我们定义好了。
使用 declare 关键字来定义它的类型，帮助 TypeScript 判断我们传入的参数类型对不对：
*/
declare var jQuery: (selector: string) => any;// 声明变量
declare module Module_Name {
}// 声明模块或文件
/// <reference path = " runoob.d.ts" /> // TypeScript 引入声明文件语法格式：
// 声明文件以 .d.ts 为后缀，例如：xx.d.ts
```
