---
title: 剑值offer
date: 2019-09-02 16:59:41
tags:
- 题库
---
1. 跳台阶、矩形覆盖
- 题目：一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。
- 分析：青蛙每次只有一阶或者两阶两种跳法，找规律，那么：f(1) = 1; f(2) = 2; f(3) = 3; f(4) = 5....
    ``` js
    // 最终得出的是一个斐波那契数列：
            |  1，n = 1
    f(n) =  |  2, n = 2
            |  f(n-1) + f(n -2), n >= 3
    ```
    ``` js
    // 动态规则实现： 
    function jumpFloor(number)
    {
        // 跳台阶，找规律，斐波那契数列1，2，3，5，8
        if (number < 3){
            return number
        }else {
            var f0 = 1, f1 = 2;
            var f2 = f0 + f1;
            for (var i=3; i<=number; i++){
                f2 = f0 + f1;
                f0 = f1;
                f1 = f2;
            }
            return f2;
        }
    }
    // 递归方法实现：
    function jumpFloor(number)
    {
        // 跳台阶，找规律，斐波那契数列1，2，3，5，8
        if (number < 3){
            return number
        }else {
            return jumpFloor(number - 1) + jumpFloor(number - 2);
        }
    }
    ```

2. 变态跳台阶问题
- 题目：一个台阶总共有n级，如果一次可以跳1级，也可以跳2级......它也可以跳上n级。此时该青蛙跳上一个n级的台阶总共有多少种跳法？
- 分析：f(1) = 1; f(2) = 2; f(3) = 4; f(4) = 8; f(5) = 16....
    ``` js
    // 最终得出的：
            |  1，n = 1
    f(n) =  |  2, n = 2
            |  2 * f(n-1), n >= 3
    ```

    ``` js
    // 动态规则实现： 
    function jumpFloorII(number)
    {
        if (number < 3){
            return number
        }else {
            var f2 = 2;
            var f3 = 2 * f2;
            for (var i=3; i<=number; i++){
                f3 = 2 * f2;
                f2 = f3;
            }
            return f3;
        }
    }

    // 递归方法实现：
    function jumpFloorII(number)
    {
        if (number < 3){
            return number
        }else {
            return 2 * jumpFloorII(number-1)
        }
    }
    ```
3. 输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。
``` js
// 位运算
function NumberOf1(n)
{
    // 整数输入计算机都是以二进制来存储，正整数以原码来存储，负整数以补码来存储，十进制显示，可以使用位运算符
    var count = 0,flag=1;
    while(flag){
        if(n & flag){
            count++;
        }
        flag = flag << 1; //左移一位
    }
    return count;
}
// 十进制转二进制，统计1的个数
function NumberOf1(n)
{
    if(n < 0){
        n = n >>> 0;// 如果是负数，现将其转换为（负数+2的32次方），也就是32位负数补码的十进制
    }
    var res = n.toString(2); // 正整数转二进制
    var count = 0;
    for (var i=0; i<res.length; i++){
        if (res[i] == 1){
            count++;
        }
    }
    return count;
}
```
4. 滑动窗口
``` js
// 最大值用Math.max.apply
function maxInWindows(num, size)
{
    // write code here
    var arr = [];
    // 滑动num.length-size+1次
    for (var i=0; i<num.length-size+1; i++){
        var tempindex = i + size;
        var temparr = num.slice(i, tempindex);
        arr.push(Math.max.apply(this, temparr))// this调用Math.max方法
    }
    return arr;
}
// 最大值用循环
function maxInWindows(num, size)
{
    // write code here
    if (size == 0){
        return [];
    }
    var arr = [];
    // 滑动num.length-size+1次
    for (var i = 0; i < num.length - size + 1; i++){
        var temp = i + size - 1;
        // 排序选取最大值
        var max = num[i];
        for(var j = i; j <= temp; j++){     
            if (num[j] > max){
                max = num[j];
            }
        }
        arr.push(max);
    }
    return arr;
}
```
5. 出现数字超过一半、中位数、寻找第k大的数（计算数组中每个元素出现的次数）
6. 顺时针打印矩阵：
    - 方法一：
    ``` js
    function printMatrix(matrix)
    {
        // 记录top right bottom left的值，依次打印，打印一圈，left++, right--, top++, bottom--;
        var row = matrix.length;
        var col = matrix[0].length;
        var left = 0, right = col - 1, top = 0, bottom = row - 1;
        var res = [];
        if (row == 0 || col == 0){
            return res;
        }
        while (left <= right && top <= bottom){
            // 从左到右打印
            for (var i = left; i <= right; i++){
                res.push(matrix[top][i]);
            }
            // 从上到下打印
            for (var i = top + 1; i <= bottom; i++){
                res.push(matrix[i][right])
            }
            // 从右到左打印
            if (top != bottom){
                for (var i = right-1; i >= left; i--){
                    res.push(matrix[bottom][i])
                }
            }
            // 从下到上打印
            if (left != right){
                for (var i= bottom - 1; i > top; i--){
                    res.push(matrix[i][left])
                }
            }
            left++, right--, top++, bottom--;
        }
        return res;
    }
    ```
    - 方法二：
    ``` js
    // 使用矩阵转置的思想
    // 顺时针打印矩阵，打印第一排，然后剩下矩阵转置再上下交换，形成新的矩阵，在打印第一排，循环如此
    // 矩阵转置➕上下交换
    function reverseMatrix(matrix){
        // 初始化数组
        var matrix2=[];
        // console.log(matrix)
        for(var i=0;i<matrix[0].length;i++){
            matrix2[i]=[];
        }
        // 矩阵转置
        for(var i=0;i<matrix.length;i++){
            for(var j=0;j<matrix[i].length;j++){
                matrix2[j][i]=matrix[i][j];
            }
        }
        // 初始化
        var brr = [], len =matrix2.length;
        for(var i=0;i<matrix2.length;i++){
            brr[i]=[];
        }
        // 数组上下交换
        for(var i = 0; i < len; i++){
            for (var j = 0; j < matrix2[i].length; j++){
                brr[i][j] = matrix2[len-i-1][j]
            }
        }
        return brr;
    }

    function printMatrix(matrix){
        var res = [];
        var brr = matrix;
        for (var i=0; i<brr[0].length; i++){
            res.push(brr[0][i]);    
        }
        while(brr.length > 1){
            var crr = brr.slice(1, brr.length);
            var brr = reverseMatrix(crr); 
            for (var i=0; i<brr[0].length; i++){
                res.push(brr[0][i]); 
            }   
        }
        return res  
    }
    ```