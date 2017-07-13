---
title: package安装mysql
toc: true
comment: true
date: 2017-04-13 18:46:08
categories:
tags: mysql
---


通过brew安装mysql是很简单的，但是在使用的时候经常出现奇怪的错误
，比如这样的`The server quit without updating PID file`,或者这样的

改用package安装



<!--more-->


## 下载安装包

  访问MySQL的官网[http://www.mysql.com/downloads/](http://www.mysql.com/downloads/) 然后在页面中会看到“MySQL Community Server”下方有一个“download”点击



## 设置新密码

```
set PASSWORD = PASSWORD('new_password');
```