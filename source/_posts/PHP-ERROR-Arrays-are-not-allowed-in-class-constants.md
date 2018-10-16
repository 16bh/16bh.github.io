---
title: '[PHP ERROR]:Arrays are not allowed in class constants '
toc: false
date: 2017-03-27 18:38:37
categories:
tags: [php,error]
---



>FastCGI sent in stderr: "PHP message: PHP Fatal error:  Arrays are not allowed in class constants in xxxxx on line xx" while reading response header from upstream


<!--more-->

错误原因：PHP5.6以下的版本不支持在常量中定义数组（当时我们线上的php版本是5.4）
解决方案：
- 升级php版本
- 不在常量中定义数组



php5.6引入的新功能有：
- 可以使用表达式定义常量
- 使用 ... 运算符定义变长参数函数
- 使用 ** 进行幂运算
- use function 以及 use const
- 加入 hash_equals() 函数，以恒定的时间消耗来进行字符串比较，以避免时序攻击
- 加入 __debugInfo()
