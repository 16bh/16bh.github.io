---
title: app中h5页面传递用户登陆信息 - session与token
toc: false
date: 2016-07-21 11:10:55
categories: 服务端
tags: [php,服务端]
---


>`app`中用`token`存储用户登录信息
>`h5`中用`session`存储用户信息


<!--more-->

# token使用

   后端将用户登录的用户名和密码通过加密生成`token`值并返回给`app`,`app`下次请求接口时带上`token`，直到用户登出为止
   
   当后端需要根据`token`值获取用户信息时，只需要进行相应的解密操作即可
   
 # 在`app`中的`h5`页面判断用户登录
 
 `app`中的`h5`页面
 
 


