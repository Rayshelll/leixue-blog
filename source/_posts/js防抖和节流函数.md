---
title: js节流和防抖函数
date: 2019-09-15 14:38:43
tags:
- js
---

##### 关于js节流函数throttle和防抖debounce
使用`节流`、`防抖`方法用于优化操作DOM节点引起频繁触发的事件时造成的大量计算，频繁触发的事件：页面绑定事件`resize`、页面滚动条事件`scroll`、页面元素绑定拖拽事件`mousemove`等。

##### 节流函数throttle
**节流函数的优化思想**`oninput`，`onkeypress`，`onscroll`，`resize`等事件触发频率非常高，在这些事件触发时执行代码，就会相应的将代码块执行很多次，通常大量的重复执行是没有必要的。降低这种操作的频率，保证一定时间内，核心代码只执行一次。
**节流函数的定义**保证一段时间内只执行一次核心代码。指定delay(延迟时间)，如果在delay内多次调用，`throttle`会舍弃中间的所有调用操作作，直到用户停止行为后的delay后，执行一次预期执行函数。
**代码实现**：每次触发事件时都判断当前是否有等待执行的延时函数。
``` js
// 定时器版
const throttle = function(fn, delay) {
    let runFlag = false; // 通过闭包保存一个函数是否运行的标记
    return function (e) {
        // 判断之前的调用是否完成，没有完成，直接return
        if (runFlag) {
            return
        }
        runFlag = true; // 设置为false
        setTimeout(() => {
            fn();//将外部传入的函数的执行放在setTimeout中
            runFlag = true; // 最后在setTimeout执行完毕后再把标记设置为true(关键)表示可以执行下一次循环了。当定时器没有执行的时候标记永远是false，在开头被return掉
        }, delay)
    }
}
function sayHi(e) {
      console.log(e.target.innerWidth, e.target.innerHeight);
    }
window.addEventListener('resize', throttle(sayHi,1000));
```

##### debounce
**防抖的定义**是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间，只取最后一次。
常见的优化适用于：表单组件输入内容验证、防止多次点击导致表单多次提交等情况，防止函数过于频繁的不必要调用。(频繁操作完，再执行函数)
**代码实现**：每次触发事件时都取消之前的延时调用方法。用 `setTimeout` 实现计时，配合 `clearTimeout` 实现“重新开始计时”。即只要触发，就会清除上一个计时器，又注册新的一个计时器。直到停止触发 wait 时间后，才会执行回调函数。不断触发事件，就会不断重复这个过程，达到防止目标函数过于频繁的调用的目的。每次触发事件时都取消之前的延时调用方法
``` js
const debounce = function(fn, delay) {
    let handle = null; // 创建一个标记用来存放定时器的返回值
    return function () {
        clearTimeout(handle);// 每当用户输入的时候把前一个 setTimeout clear 掉，取消之前的延时调用
        handle = setTimeout(() => {// 然后又创建一个新的 setTimeout, 这样就能保证输入字符后的delay间隔内如果还有字符输入的话，就不会执行 fn 函数
            fn();
        }, delay);
    }
}
function sayHi() {
    console.log('防抖成功');
}
var inp = document.getElementById('inp');
inp.addEventListener('input', debounce(sayHi,1000)); // 防抖
```

##### 总结
- 防抖动：根据操作来，将几次操作合并为最后一次操作进行。原理是维护一个计时器，规定在delay时间后触发函数，但是在delay时间内再次触发的话，就会取消之前的计时器而重新设置。这样一来，只有最后一次操作能被触发。
- 节流：根据时间来，使得一定时间内只触发一次函数。原理是通过判断是否到达一定时间来触发函数，若没到规定时间则使用计时器延后，而下一次事件则会重新设定计时器。
最大的区别就是，节流函数不管事件触发有多频繁，都会保证在规定时间内一定会执行一次真正的事件处理函数，而防抖动只是在最后一次事件后才触发一次函数。