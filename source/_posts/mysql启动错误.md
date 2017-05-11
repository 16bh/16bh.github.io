---
title: mysql启动错误:The server quit without updating PID file
toc: false
date: 2016-07-12 17:13:44
categories: [IT,mysql]
tags: [mysql,error]
---


安装mysql后，启动失败，错误提示为


> mysql Starting MySQL..The server quit without updating PID file

<!--more-->

查看mysql错误日志

``` shell
var /usr/local/var/mysql
vim jims-MacBook-Air.local.err    //电脑名.err文件
```

mysql报错如下：

> Can't start server: Bind on TCP/IP port: Address already in use

mysql默认的端口号是3306,查看3306端口号占用情况:

``` shell
lsof -i TCP:3306
```
将占用端口的软件或服务关闭后重试