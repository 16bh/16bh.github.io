---
title: echo字符串时字符串头部出现空格bug
toc: true
comment: true
date: 2018-02-06 18:51:50
categories: [IT]
tags: [php]
---


echo字符串时字符串头部出现了未知的空格
如果是单纯的展示问题不大
但是如果作为接口的返回值，调用方判断字符串时多出的空格就会报错



<!--more-->

以下面的代码为例，

```
 <?php

echo 2233;
```

输出结果为：

> 2233


注意2233前面多了个空格，其实是把php文件的头部`<?php`之前的空格打印出来了

上面只是个简单的示例，实际情况可能更加复杂：比如use了别的文件或者使用了别的类的方法，那么别的文件头部的字符也会被打印出来


可以通过下面的命令检查项目中所有文件的头部是否有多余的空格

```
cd /project_root
find . *|xargs grep "^ <?php"
```
