---
title: 基础js学习
date: 2019-10-04 09:51:16
tags:
- js
---
1. 基础数据类型：
    - 基本类型：String(任意字符串) Number(任意数字) boolean(true/false) null(null) undefined(undefined)
    - 对象类型（引用类型）：Object(任意对象) Array(一种特别对象，数值下表，内部数据有序) Function(一种特别对象)
    - 分类：typeof instanceof
        - typeof:可以判断number string boolean undefined function；不可以判断：array与object、null与object；返回数据类型是字符串表达式
        - instanceof：判断对象的具体类型；可以判断undefined和null