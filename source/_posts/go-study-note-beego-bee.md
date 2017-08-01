---
title: go学习笔记：Beego
toc: true
comment: true
date: 2017-07-27 15:33:17
categories:
tags: go
---



<img src="http://o9xbyqajf.bkt.clouddn.com/20170727150114170158010.png" />

谢大的beego开源项目：

<div class="github-widget" data-repo="astaxie/beego"></div>

<!--more-->

## 安装beego

```
 go get -u github.com/astaxie/beego
```


## 安装bee工具

```
go get github.com/beego/bee
```


## 使用bee工具

### 工具命令一览

```
new         create an application base on beego framework
run         run the app which can hot compile
pack        compress an beego project
api         create an api application base on beego framework
bale        packs non-Go files to Go source files
version     show the bee & beego version
generate    source code generator
migrate     run database migrations

```

### 生成一个项目

```
cd src
bee new {project_name}
```
<img src="http://o9xbyqajf.bkt.clouddn.com/2017072715011416163291.png"/>

然后在src目录下生成一个项目，结构入下：

<img src="http://o9xbyqajf.bkt.clouddn.com/20170727150114096074080.png"/>


### 创建api

```
cd src
bee api {project_name}
```

<img src="http://o9xbyqajf.bkt.clouddn.com/20170727150114112858689.png"/>

结构如下：

<img src="http://o9xbyqajf.bkt.clouddn.com/20170727150114117882110.png"/>

对比之前的结构可以发现在controllers和models目录分别生成了object.go和user.go文件

### 运行项目

```
cd src
bee run {project_name}
```

<img src="http://o9xbyqajf.bkt.clouddn.com/20170727150114201058758.png" />

在浏览器中访问`http://localhost:8080`,结果如下图所示：
<img src="http://o9xbyqajf.bkt.clouddn.com/20170727150114189785456.png" width="492" height="297"/>

官网文档是这么介绍的
> 这样我们的应用已经在 8080 端口(beego 的默认端口)跑起来了.你是不是觉得很神奇，为什么没有 nginx 和 apache 居然可以自己干这个事情？是的，Go 其实已经做了网络层的东西，beego 只是封装了一下，所以可以做到不需要 nginx 和 apache


我本人在使用的时候发现如果打开了nginx有时会报404的错误，所以最好先关闭nginx服务


