---
title: magento地址不带index.php无法访问？
toc: false
date: 2016-07-12 18:37:06
categories: Magento开发
tags: magento
---



有时候，如果`url`不带`index.php`会报403nginx错误
如果你的`nginx`或`apache`的配置无误
则需要修改`magento`的后台配置


<!--more-->

`System`>`Configuration`>`Web`>`Search Engines Optimization`>`Use Web Server Rewrites`修改为`Yes`
![](http://o9xbyqajf.bkt.clouddn.com/images/1468319924766.png)
