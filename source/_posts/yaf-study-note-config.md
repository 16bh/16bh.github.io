---
title: yaf学习笔记 - 配置
categories:
tags: [php,yaf]
toc: false
comment: true
date: 2017-06-09 18:59:00
---








yaf的配置有两种，

- 一是Yaf自身的配置
- 二是生成的项目自己的配置，如项目所用的数据库、缓存配置等

## 修改yaf设置
在路径`/usr/local/etc/php/7.0/conf.d`下存放了各个扩展的配置文件
![20170612149726524849464.png](/images/20170612149726524849464.png)

<!--more-->

`ex-yaf.ini`文件即为yaf模块的配置文件，用vim命令打开该文件，内容如下所示

```
[yaf]
extension="/usr/local/opt/php70-yaf/yaf.so"  //扩展位置
```
我们直接在后面添加配置内容，修改后如下

```
[yaf]
extension="/usr/local/opt/php70-yaf/yaf.so"	//扩展位置
yaf.use_namespace = 1	//启用名字空间
yaf.environ = "dev"	   //设置环境为本地开发环境
```

修改后重启php-fpm

打印phpinfo(),`yaf.use_namespace`的值已经变成ON了，说明修改成功
![20170612149726543885457.png](/images/20170612149726543885457.png)

## yaf的配置项一览
![20170612149726554799450.png](/images/20170612149726554799450.png)


## 项目配置
项目的配置文件为`./conf/application.ini`
默认配置如下：

```
[common]
application.directory = APPLICATION_PATH  "/application"
application.dispatcher.catchException = TRUE

[dev : common]
database.type = mysql
database.read_host = 127.0.0.1
database.read_port =  3306
database.read_user = root
database.read_pwd = root
database.name = yaf
database.db_prefix = tbl_

[test : common]

[product : common]

```

注意，配置是分组的，common为通用配置，dev表示本地环境，test表示测试环境，product表示生产环境，后面的`：common`表示继承了common分组。我们之前已经修改了`yaf.environ`的值为dev，表示使用`[dev : common]`分组下的设置

我们在dev分组下对mysql数据库进行了配置

## 获取配置文件中的值

如要获取上述配置文件中`application.directory`的值，可以通过下面的方式获取

```
$config = Yaf_Application::app()->getConfig()
echo $config->application->directory;
```


