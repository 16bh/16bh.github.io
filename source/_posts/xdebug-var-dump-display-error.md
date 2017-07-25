---
title: 安装xdebug后var_dump显示问题
toc: true
comment: true
date: 2017-07-24 17:08:19
categories:
tags: [xdebug,phpstorm]
---

<img src="http://o9xbyqajf.bkt.clouddn.com/20170724150088775879.png" width="492" height="297"/>
(图片来源：[pixabay](https://pixabay.com/zh/))

 安装了xdebug之后，使用var_dump打印输出时显示错误
 
<!--more-->

 错误如下：
 
 <img src="http://o9xbyqajf.bkt.clouddn.com/20170724150088734626603.jpg"/>



在网上查询了一下，有人说先检查一下php的配置中`html_errors`这项是否是开启的，如果是Off的就把它设置为On

php手册中关于html_errors的介绍：
>html_errors boolean
在错误信息中关闭HTML标签。这种新的HTML格式的错误信息是可以点击，它引导用户前往描述该错误或者导致该错误发生的函数的参考信息页面。 这些参考与 docref_root 和 docref_ext 的设置有关。

检查的方法是在终端输入以下命令

```
php -i | grep html_errors
```

好了，先检查一下


<img src="http://o9xbyqajf.bkt.clouddn.com/20170724150088750041484.jpg"/>

果然是关闭的，去`php.ini`里开启它吧

<img src="http://o9xbyqajf.bkt.clouddn.com/20170724150088738770125.jpg"/>

若还未生效
查看php设置的`xdebug.overload_var_dump`这一项，将其设置为0

<img src="http://o9xbyqajf.bkt.clouddn.com/20170725150097075965208.png"/>

改好了重启php-fpm服务




## 参考

> http://www.cnblogs.com/huangye-dream/p/4182803.html


