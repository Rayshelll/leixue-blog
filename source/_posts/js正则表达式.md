---
title: js正则表达式
date: 2019-09-05 15:21:35
tags:
- JavaScript
---
#### js正则表达式
1. 创建一个正则表达式
    ``` js
    let re = /ab+c/
    // 或者
    let re = new RegExp("ab+c", 'g')//ab+c/g
    /* g 是全局搜索; 
     i 不区分大小写;
     m 多行搜索; 
     s 允许 . 匹配换行符; 
     u 使用unicode码的模式进行匹配; 
     y	执行“粘性”搜索,匹配从目标字符串的当前位置开始，可以使用y标志。*/
    ```

2. [正则表达式中的特殊字符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)
`^`  匹配开始符
`$`  匹配结束符
`\d` 匹配一个数字。等价于`[0-9]`。
`\D` 匹配一个非数字字符。等价于`[^0-9]`。
`\s` 匹配一个空白字符，包括空格、制表符、换页符和换行符。
`\w` 匹配一个单字字符
[^0-9a-zA-Z]
....

3. 使用正则表达式
``` js
reg.exec(str)	    //查找字符串str是否匹配reg规则，它返回一个数组（未匹配到则返回 null）。 [ 'abbc', index: 0, input: 'abbc', groups: undefined ]
reg.test(str)	    //测试字符串str否匹配reg规则，匹配返回 true 或 不匹配返回false。
str.match(reg)	    //一个在字符串中执行查找匹配的String方法，它返回一个数组，在未匹配到时会返回 null。
str.matchAll(reg)	//一个在字符串中执行查找所有匹配的String方法，它返回一个迭代器（iterator）。Object [RegExp String Iterator] {}
str.search(reg)	    //一个在字符串中测试匹配的String方法，它返回匹配到的位置索引，或者不存在时返回-1。
str.replace(reg, str2)	    //一个在字符串中执行查找匹配的String方法，并且使用替换字符串替换掉匹配到的子字符串。
str.split(reg)	        //一个使用正则表达式，并将分隔后的子字符串存储到数组中。
```

4. 例子
    ``` js 
    function match(s, pattern)
    {
        var pattern = '^' + pattern + '$'; // ^ab*a$
        var pat = new RegExp(pattern,'g'); // /^ab*a$/g  new RegExp('^ab*a$','g')
        return pat.test(s); // s匹配pat, pat是否包含s
    }
    ```