---
title: 解决重启后私钥失效的问题
toc: false
comment: true
date: 2017-07-07 16:26:09
categories:
tags: git
---


通过ssh-add的方式添加私钥后，重启后会导致私钥无效，需要重新添加

原因是ssh-add的方法是将private key加入到ssh-agent中，而ssh-agent是用来临时存储私钥的session服务

整理了一下解决方法



<!--more-->


## 设置脚本自动添加私钥

现在解决之前遇到的重启后私钥失效的问题

使用mac自带的`Automator`工具

新建一个应用程序
![20170707149941570858169.png](http://o9xbyqajf.bkt.clouddn.com/20170707149941570858169.png)


选择`运行shell脚本`

![20170707149941566797740.png](http://o9xbyqajf.bkt.clouddn.com/20170707149941566797740.png)

在脚本中添加如下命令

```
ssh-add id_rsa.gitlab
ssh-add id_rsa.github
```

保存，命名为`ssh-add private keys`，会生成一个app，设置开机启动该app即可


## 永久添加私钥

> 原文见 [Mac 上 ssh-add 永久将私钥添加到 Keychain](http://www.icodeyou.com/2016/01/17/ssh-add-mac/)

如果不想使用下面的脚本,可以用下面的命令添加私钥

ssh-agent 是一个用于存储私钥的临时性的 session 服务
将私钥存储在Keychain中就可以永久使用了

```
ssh -add -K id_rsa.github
```


>github关于ssh的说明：https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/