---
title: mac下phpStorm配置使用phpmd
categories: Software
toc: false
comment: true
date: 2017-04-01 17:02:33
tags: [phpmd,phpstorm]
---


如果说phpcs规范了php代码的规范，那么phpmd就是aa检测php代码错误的利器


<!--more-->

## 什么是phpmd

>phpmd,short of PHP Mess Detector,is a tool that checks if you aren’t making a mess of your code. Think of methods of hundreds of lines, classes that extend class after class after class, lack of documentation, nested loops, etc. PHP Mess Detector points out these culprits and aids into writing more manageable code.


## 安装phpmd
```shell
brew install phpmd
```
安装之后查看phpmd的路径
![20170401149103931820920.png](phpmd-in-phpstorm-on-mac/20170401149103931820920.png)
路径就是`/usr/local/bin/phpmd`

## 配置phpmd
``Preferences/Languages & Frameworks/PHP/Mess Detector``
![20170401149103941390595.png](phpmd-in-phpstorm-on-mac/20170401149103941390595.png)
点开`Local`后的`...`,输入phpmd的路径`/usr/local/bin/phpmd`,点击`Validate`进行验证
![20170401149103954380798.png](phpmd-in-phpstorm-on-mac/20170401149103954380798.png)


`Preferences/Editor/Inspections/PHP/PHP Mess Detector validation`

![20170401149103936778520.png](phpmd-in-phpstorm-on-mac/20170401149103936778520.png)
勾选中`PHP Mess Detector validation`,并选择右侧建议的`Options`规则，规则的说明参考：[https://phpmd.org/rules/index.html](https://phpmd.org/rules/index.html)：
![20170401149103968164148.png](phpmd-in-phpstorm-on-mac/20170401149103968164148.png)

## 使用phpmd
![20170401149103926528991.png](phpmd-in-phpstorm-on-mac/20170401149103926528991.png)
