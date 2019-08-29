---
title: ajax
date: 2019-08-19 16:07:05
tags:
---
#### 1. 什么是ajax？ajax作用是什么？
异步的javascript和xml  
AJAX 是一种用于创建快速动态网页的技术。  
ajax用来与后台交互
<!-- more -->
#### 2. 原生js ajax请求有几个步骤？分别是什么
``` js
//创建 XMLHttpRequest 对象
var ajax = new XMLHttpRequest();
/* 规定请求的类型、URL 以及是否异步处理请求。
method：请求的类型；GET 或 POST
url：文件在服务器上的位置
async：true（异步）或 false（同步）*/
ajax.open('GET',url,true);
//发送信息至服务器时内容编码类型
ajax.setRequestHeader("Content-type", "请求文件"); 
//发送请求
ajax.send();  
//接受服务器响应数据
ajax.onreadystatechange = function () {
    if (obj.readyState == 4 && (obj.status == 200 || obj.status == 304)) { 
        // 相应操作
    }
};
```
#### 3. json字符串转换集json对象、json对象转换json字符串
``` js
//字符串转json对象
JSON.parse(json) 
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
    //通过定义函数名去接收后台返回数据
    function jsonpCallback(data){
        //注意  jsonp返回的数据是json对象可以直接使用
        //ajax  取得数据是json字符串需要转换成json对象才可以使用。
    }
    ```

##### 2. CORS：跨域资源共享
- 原理：服务器设置Access-Control-Allow-OriginHTTP响应头之后，浏览器将会允许跨域请求
- 限制：浏览器需要支持HTML5，可以支持POST，PUT等方法兼容ie9以上
``` js
//需要后台设置
Access-Control-Allow-Origin: *              //允许所有域名访问，或者
Access-Control-Allow-Origin: http://a.com   //只允许所有域名访问
```

##### 3. 设置 document.domain
- 原理：相同主域名不同子域名下的页面，可以设置document.domain让它们同域
- 限制：同域document提供的是页面间的互操作，需要载入iframe页面
``` js
// URL http://a.com/foo
var ifr = document.createElement('iframe');
ifr.src = 'http://b.a.com/bar'; 
ifr.onload = function(){
    var ifrdoc = ifr.contentDocument || ifr.contentWindow.document;
    ifrdoc.getElementsById("foo").innerHTML);
};

ifr.style.display = 'none';
document.body.appendChild(ifr);
```

##### 4. 用Apache做转发（逆向代理），让跨域变成同域


