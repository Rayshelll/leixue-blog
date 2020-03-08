---
title: ajax
date: 2019-08-19 16:07:05
tags:
---
#### 1. 什么是ajax？ajax作用是什么？
AJAX = Asynchronous JavaScript And XML(异步的javascript和xml)。`AJAX`不刷新页面更新网页。
工作流程：
1. 网页中发生一个事件（页面加载、按钮点击）
2. 由 JavaScript 创建 `XMLHttpRequest` 对象
3. XMLHttpRequest 对象向 web 服务器发送请求
4. 服务器处理该请求
5. 服务器将响应发送回网页
6. 由 JavaScript 读取响应
7. 由 JavaScript 执行正确的动作（比如更新页面）

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
//字符串转json对象，反序列化
JSON.parse(str,t1) //t1是方法
// json对象转字符串，序列化
JSON.stringify(json,t1,t2)//t1参数可以是array或是function，t2是分隔符
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

#### 6. [跨域解决方案有哪些](https://segmentfault.com/a/1190000011145364?utm_source=tag-newest)？
1. 通过jsonp跨域
2. document.domain + iframe跨域
3. location.hash + iframe
4. window.name + iframe跨域
5. postMessage跨域
6. 跨域资源共享（CORS）
7. nginx代理跨域
8. nodejs中间件代理跨域
9. WebSocket协议跨域

##### 1. [CORS：跨域资源共享](https://www.jianshu.com/p/98d4bc7565b2)
- 它允许浏览器向跨源服务器，发出`XMLHttpRequest`请求，从而克服了AJAX只能同源使用的限制。
- 原理：服务器端对于CORS的支持，主要就是通过设置`Access-Control-Allow-Origin`来进行的。如果浏览器检测到相应的设置，就可以允许Ajax进行跨域的访问。
- 限制：浏览器需要支持HTML5，可以支持POST，PUT等方法兼容ie9以上

，就可以实现跨域访问了
普通跨域请求：只需要在后台中加上响应头来允许域请求，在被请求的Response header中加入以下设置，前端无须设置，若要带cookie请求：前后端都需要设置。
需注意的是：由于同源策略的限制，所读取的cookie为跨域请求接口所在域的cookie，而非当前页。
``` js
// 前端
var xhr = new XMLHttpRequest(); // IE8/9需用window.XDomainRequest兼容
// 前端设置是否带cookie
xhr.withCredentials = true;

//需要后台设置
Access-Control-Allow-Origin: *              //允许所有域名访问，或者
Access-Control-Allow-Origin: http://a.com   //只允许所有域名访问
//响应类型
Access-Control-Allow-Methods:GET,POST
//响应头设置
Access-Control-Allow-Headers:x-requested-with,content-type
```

##### 2. jsonp 只能解决get跨域
- 原理：动态创建一个script标签。利用script标签的src属性不受同源策略限制。因为所有的src属性和href属性都不受同源策略限制。这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。所以jsonp是需要服务器端的页面进行相应的配合的。（即用JavaScript动态加载一个script文件，同时定义一个callback函数给script执行而已。）
- 步骤：
    ``` js
    //去创建一个script标签
    var  script = document.createElement("script");
    script.type = 'text/javascript';
    //script的src属性设置接口地址 并带一个callback回调函数名称(必须要带一个自定义函数名 要不然后台无法返回数据。)
    script.src = "http://127.0.0.1:8888/index.php?callback=jsonpCallback";
    //插入到页面
    document.head.appendChild(script);
    //通过定义回调函数名去接收后台index.php返回数据
    function jsonpCallback(data){
        //注意  jsonp返回的数据是json对象可以直接使用
        alert(JSON.stringify(data));
        //ajax  取得数据是json字符串需要JSON.parse(str)转换成json对象才可以使用。
    }
    ```
页面使用jquery，那么通过它封装的方法就能很方便的来进行jsonp操作了。jquery会自动生成一个全局函数来替换callback=?中的问号，之后获取到数据后又会自动销毁，实际上就是起一个临时代理函数的作用。$.getJSON方法会自动判断是否跨域，不跨域的话，就调用普通的ajax方法；跨域的话，则会以异步加载js文件的形式来调用jsonp的回调函数。

    ``` js
   ​<script type="text/javascript">
        $.getJSON('http://example.com/data.php?callback=?,function(jsondata)'){
            //处理获得的json数据
        });
    </script>
    ```

##### 3. [设置 document.domain](https://blog.csdn.net/sinat_36422236/article/details/79748688)
- `document.domain`用来得到当前网页的域名
- 原理：此方案仅限主域相同，子域不同的跨域应用场景。两个页面都通过js强制设置document.domain为基础主域，就实现了同域;
- 限制：同域document提供的是页面间的互操作，需要载入iframe页面
``` js
// 父窗口：(http://www.domain.com/a.html)
<iframe id="iframe" src="http://child.domain.com/b.html"></iframe>
<script>
    document.domain = 'domain.com';
    var user = 'admin';
</script>

// 子窗口：(http://child.domain.com/b.html)
<script>
    document.domain = 'domain.com';
    // 获取父窗口中变量
    alert('get js data from parent ---> ' + window.parent.user);
</script>
```

##### 4. 使用HTML5的window.postMessage方法跨域
HTML5引入了一个全新的API：跨文档通信 API（Cross-document messaging）。 这个API为window对象新增了一个`window.postMessage`方法，允许跨窗口通信，不论这两个窗口是否同源。目前IE8+、FireFox、Chrome、Opera等浏览器都已经支持`window.postMessage`方法。 
``` js
//发送方
<iframe id="frame1" src="http://127.0.0.1/JSONP/b.html" frameborder="1"></iframe>
document.getElementById('frame1').onload = function(){
    var win = document.getElementById('frame1').contentWindow;
    win.postMessage("我是来自a页面的","http://127.0.0.1/JSONP/b.html")
}
//接收方
window.onmessage = function(e){
    e = e || event;
    console.log(e.data);//我是来自a页面的
}
```

##### 5. 通过WebSocket进行跨域
web sockets是一种浏览器的API，它的目标是在一个单独的持久连接上提供全双工、双向通信。(同源策略对web sockets不适用)
web sockets原理：在js创建了web socket之后，会有一个HTTP请求发送到浏览器以发起连接。取得服务器响应后，建立的连接会使用HTTP升级从HTTP协议交换为`web sockt`协议。
只有在支持web socket协议的服务器上才能正常工作。
``` js
var socket = new WebSockt('ws://www.baidu.com');//http->ws; https->wss
socket.send('hello WebSockt');
socket.onmessage = function(event){
    var data = event.data;
}
```

