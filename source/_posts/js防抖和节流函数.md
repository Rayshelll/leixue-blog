---
title: js节流和防抖函数
date: 2019-09-15 14:38:43
tags:
- js
---

##### 关于js节流函数throttle和防抖debounce
在浏览器中操作DOM比非DOM交互需要更多的内存和CPU的事件，连续尝试进行过多的DOM相关操作可能UI导致浏览器挂起，有时甚至会崩溃。尤其在IE中使用`onresize事件`处理程序的时候容易发生，当调整浏览器大小的时候，该事件会连续触发。
最常见的应用场景就是一些会频繁触发的事件：页面绑定事件`resize`、页面滚动条事件`scroll`、页面元素绑定拖拽事件`mousemove`等。如果为这些事件绑定一些操作 DOM 节点的操作的话，那就会引发大量的计算，在用户看来，页面可能就一时间没有响应，这个页面一下子变卡了变慢了。为了解决短时间内重复调用事件的这个问题，可以使用`节流`、`防抖`方法用于性能优化。

##### 节流函数throttle
**节流函数**允许一个函数在规定的时间内只执行一次。指定delay(延迟时间)，如果在delay内多次调用，`throttle`会舍弃中间的所有调用操作，直到用户停止行为后的delay后，执行一次预期执行函数。
代码实现：使用定时器。当我触发一个事件时，先 `setTimout` 让这个事件延迟一会再执行，如果在这个时间间隔内又触发了事件，那我们就 `clear` 掉原来的定时器，再 `setTimeout` 一个新的定时器延迟一会执行。每次触发事件时都判断当前是否有等待执行的延时函数：
``` js
// 定时器版
const throttle = function(fn, delay) {
    let runFlag = false;
    return function (e) {
        // 判断之前的调用是否完成
        if (runFlag) {
            return false;
        }
        runFlag = true;
        setTimeout(() => {
            fn();
            runFlag = false;
        }, delay)
    }
}
// 时间戳版
function throttle(func, wait) {
    let previous = 0;
    return function() {
        let now = Date.now();
        if (now - previous > wait) {
            func();
            previous = now;
        }
    }
}
```

##### debounce
所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间，只取最后一次。是常见的优化适用于：表单组件输入内容验证、防止多次点击导致表单多次提交等情况，防止函数过于频繁的不必要调用。(频繁操作完，再执行函数)
代码实现：用 `setTimeout` 实现计时，配合 `clearTimeout` 实现“重新开始计时”。即只要触发，就会清除上一个计时器，又注册新的一个计时器。直到停止触发 wait 时间后，才会执行回调函数。不断触发事件，就会不断重复这个过程，达到防止目标函数过于频繁的调用的目的。每次触发事件时都取消之前的延时调用方法
``` js
const debounce = function(fn, delay) {
    let handle;
    return function () {
        // 取消之前的延时调用
        if(handle) clearTimeout(handle);
        handle = setTimeout(() => {
            fn();
        }, delay);
    }
}
```
##### 总结
- 防抖动：将几次操作合并为一此操作进行。原理是维护一个计时器，规定在delay时间后触发函数，但是在delay时间内再次触发的话，就会取消之前的计时器而重新设置。这样一来，只有最后一次操作能被触发。
- 节流：使得一定时间内只触发一次函数。 它和防抖动最大的区别就是，节流函数不管事件触发有多频繁，都会保证在规定时间内一定会执行一次真正的事件处理函数，而防抖动只是在最后一次事件后才触发一次函数。原理是通过判断是否到达一定时间来触发函数，若没到规定时间则使用计时器延后，而下一次事件则会重新设定计时器。