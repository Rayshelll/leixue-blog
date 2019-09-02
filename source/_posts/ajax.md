---
title: ajax
date: 2019-08-19 16:07:05
tags:
---
#### 1. 什么是ajax？ajax作用是什么？
AJAX = Asynchronous JavaScript And XML.(异步的javascript和xml)
AJAX 不刷新页面更新网页。  
工作流程：
1. 网页中发生一个事件（页面加载、按钮点击）
2. 由 JavaScript 创建 XMLHttpRequest 对象
3. XMLHttpRequest 对象向 web 服务器发送请求
4. 服务器处理该请求
5. 服务器将响应发送回网页
6. 由 JavaScript 读取响应
7. 由 JavaScript 执行正确的动作（比如更新页面）

<!-- more -->

#### 2. 原生js ajax请求有几个步骤？分别是什么
``` js
//创建 XMLHttpRequest 对象
var ajax = new XMLHttpRequest();
// 接受服务器响应数据
// 服务器响应属性: responseText responseXML status statusText readyState onreadystatechange (定义当readyState 属性发生变化时被调用的函数)
ajax.onreadystatechange = function () {
    if (obj.readyState == 4 && (obj.status == 200 || obj.status == 304)) { 
        //4:请求已完成且响应已就绪
        document.getElementById("demo").innerHTML = this.responseText;
    }
};
/* 规定请求的类型、URL 以及是否异步处理请求。
method：请求的类型；GET 或 POST
url：文件在服务器上的位置（"/example/js/ajax_info.txt"）
async：true（异步）或 false（同步）*/
ajax.open('GET',url,true);
//发送请求
ajax.send();  
```
#### 3. json字符串转换集json对象、json对象转换json字符串
``` js
//字符串转json对象
JSON.parse(str) 
// json对象转字符串
JSON.stringify(json)
```

#### 4. ajax几种请求方式？他们的优缺点？
常用的`post`,`get`,`delete`;
不常用`copy`、`head`、`link`等等。
##### 代码上的区别
 1. get通过`url`传递参数
 2. post设置请求头`Header`，需要规定请求数据类型
 
##### 使用上的区别
 1. post比get安全(因为post参数在请求体中，get参数在url上面)
 2. post传输文件大理论没有限制，get传输文件小大概7-8k，ie4k左右
 3. get传输速度比post快 根据传参决定的。(post通过请求体传参，后台通过数据流接收，速度稍微慢一些，而get通过url传参可以直接获取)
 4. get获取数据，post上传数据(上传的数据比较多，而且上传数据都是重要数据，所以不论在安全性还是数据量级 post是最好的选择)

#### 5. 什么情况造成跨域？
> 同源策略限制，不同源会造成跨域。同源策略：协议、域名、端口号都相同。

http://www.baidu.com/8080/index.html 协议(http)\域名(www.baidu.com)\端口号(8080)

#### 6. 跨域解决方案有哪些？
##### 1. jsonp 只能解决get跨域
- 原理：动态创建一个script标签。利用script标签的src属性不受同源策略限制。因为所有的src属性和href属性都不受同源策略限制。可以请求第三方服务器数据内容。
- 步骤：

    ``` js
    //去创建一个script标签
    var  script = document.createElement("script");
    //script的src属性设置接口地址 并带一个callback回调函数名称(必须要带一个自定义函数名 要不然后台无法返回数据。)
    script.src = "http://127.0.0.1:8888/index.php?callback=jsonpCallback";
    //插入到页面
    document.head.appendChild(script);
    //通过定义回调函数名去接收后台index.php返回数据
    function jsonpCallback(data){
        //注意  jsonp返回的数据是json对象可以直接使用
        //ajax  取得数据是json字符串需要转换成json对象才可以使用。
    }
    ```

##### 2. [CORS：跨域资源共享](https://www.jianshu.com/p/98d4bc7565b2)
- 它允许浏览器向跨源服务器，发出`XMLHttpRequest`请求，从而克服了AJAX只能同源使用的限制。
- 原理：服务器设置`Access-Control-Allow-Origin`等参数，浏览器将会允许跨域请求
- 限制：浏览器需要支持HTML5，可以支持POST，PUT等方法兼容ie9以上
``` js
//需要后台设置
Access-Control-Allow-Origin: *              //允许所有域名访问，或者
Access-Control-Allow-Origin: http://a.com   //只允许所有域名访问
```

##### 3. [设置 document.domain](https://blog.csdn.net/sinat_36422236/article/details/79748688)
- `document.domain`用来得到当前网页的域名
- 原理：相同主域名不同子域名下的页面，协议，端口都要一致，可以设置document.domain让它们同域，在两个页面中都设置`document.domain = "xxx.com"`;
- 限制：同域document提供的是页面间的互操作，需要载入iframe页面
``` js
// a.html和b.html交互
document.domain = 'a.com';
var ifr = document.createElement('iframe');
ifr.src = 'http://script.a.com/b.html'; 
ifr.onload = function(){
    var ifrdoc = ifr.contentDocument || ifr.contentWindow.document;
    // 在这里操纵b.html
};

ifr.style.display = 'none';
document.body.appendChild(ifr);
```

##### 4. 用Apache做转发（逆向代理），让跨域变成同域


