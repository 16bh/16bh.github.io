---
title: phpstorm可编辑的Rest客户端
toc: true
comment: true
date: 2018-05-07 17:51:59
categories:
tags:
---


看了一篇文章[快速测试 API 接口的新技能](https://toutiao.io/k/6tokkp),说的是IDEA自带了Rest客户端
我就看看phpstorm能不能用的上

<!--more-->

## 版本支持

新建了个.http文件，发现根本识别不了

丫的，原来我的正版phpstorm还是2017.3的版本，速度升级到最新版，然后就支持了，bingo!

## post请求


## 能不能支持xdebug呢？

google的app版本的Postman刚开始也支持不了xdebug，后来在同事的指点下，发现在cookie里加入以下内容就可以了

> XDEBUG_SESSION=PHPSTORM;


在这里应该也可以，编辑以下请求：

```
### test
GET {{host}}/api/ticket/test
Accept : application/json
Content-Type: application/json;charset=UTF-8
Authorization:
Cookie: XDEBUG_SESSION=PHPSTORM
```
开启phpstorm的xdebug功能，果然成功了！