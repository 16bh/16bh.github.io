---
title: 斐波那契数列问题
categories:
tags: [algorithm,math,php]
toc: false
comment: true
date: 2017-06-08 15:20:02
---

斐波那契数列：

```
1,1,2,3,5,8,13,21... ...
```


<!--more-->

可以用来解决诸如下面的问题：
> 有n个台阶，你每次只能跨一阶或两阶，上楼有几种方法？
>
> 第一个月初有一对刚诞生的兔子
第二个月之后（第三个月初）它们可以生育
每月每对可生育的兔子会诞生下一对新兔子
兔子永不死去



``` php
<?php

function Fibo($n)
{
	return n<2 ? 1 : Fibo(n-1)+Fibo(n-2);
}
```
