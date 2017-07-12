---
title: phpstorm修改php文件头模板
toc: false
comment: true
date: 2017-06-21 16:32:39
categories: 
tags: [phpstorm]
---



phpstorm设置新建php文件时的头文件，一个帅气的头文件是不是让你码字的心情都更好了呢

![20170712149985488177380.png](http://o9xbyqajf.bkt.clouddn.com/20170712149985488177380.png)


<!--more-->

`Editor/ File and Code Templates / includes / PHP File Header`

![20170621149803412611540.png](http://o9xbyqajf.bkt.clouddn.com/20170621149803412611540.png)

可以在模板中使用一下变量：

* ${FILE_NAME}:current file name
* ${USER}:current user system login name
* ${DATE}:current system date
* ${TIME}:current system time
* ${YEAR}:current year
* ${MONTH}:current month
* ${DAY}:current day of the month
* ${HOUR}:current hour
* ${MINUTE}:current minute
* ${PRODUCT_NAME}:current IDE name
* ${PROJECT_NAME}:current project name

你也可以自定义变量

```
#set( $MAIL = "xxx@test.com" )
```
然后就可以在模板中使用${MAIL}变量了