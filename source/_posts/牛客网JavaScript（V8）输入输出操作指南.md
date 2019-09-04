---
title: 牛客网JavaScript（V8）输入输出操作指南
date: 2019-08-25 21:28:15
tags:
- 编程
---
### JavaScript（V8）引擎操作指南
1. 单行输入：
牛客网V8引擎是利用了`readline()`接收输入的每一行，该行字符数不能超过1024个，否则会报错。
赛码网是`read_line()`
``` js
var str = readline(); // 输入字符串
var num = paresInt(readline()); // 输入数字
```

2. 多行输入：
``` js
// 输入任意行数
while (lines = readline()) {   
    var arr = lines.split(" ");
}

/* 输入：
eg: q w e
    w e r
    w e q
输出：lines = ['q w e','w e r','w e q']; arr=[[q, w, e], [w, e, r], [w, e, q]]
*/

// 输入固定行数
var lineNum = paresInt(readline()); // 输入行数
var lines = [];
for (var i=0; i<lineNum; i++){
    var lines = lines.push(readline());
}
/* 输入：
eg: 3
    1 2
    2 3
    3 4
输出：lineNum = 3; lines = ['1 2', '2 3', '3 4']
*/

// 输入矩阵
var lineNum = paresInt(readline()); // 输入行数
var lines = [];
for (var i=0; i<lineNum; i++){
    var lines = lines.push(readline().split(" "));
}
/* 输入：
eg: 3
    1 2 4
    2 3 4
    3 4 4
输出：lineNum = 3; lines = [[1, 2, 4], [2, 3, 4], [3, 4, 4]]
*/
```

3. 输出
``` js
print()
console.log()
```