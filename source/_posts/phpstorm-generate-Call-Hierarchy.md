---
title: phpstorm生成函数调用关系
toc: true
comment: true
date: 2017-10-16 16:25:39
categories:
tags: php
---



知乎上有人提问如何生成函数调用路程图

原问题见：
https://www.zhihu.com/question/34495043/answer/244410441



<!--more-->

phpstorm也有检查函数调用这个功能

在偏好设置中搜索关键字 Call Hierarchy

找到快捷键 ctrl+alt+h

<img src="/images/20171016150814248321882.png" />


使用效果如下：

选中一个函数array_slice，按快捷键，在右边生成了该函数所有的调用关系

与查看用例find usage不同的是，Call Hierarchy功能会递归的寻找用例的用例，直到找到没有入口函数为止

<img src="/images/20171016150814276075001.png" />
