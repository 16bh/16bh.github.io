---
title: Maximum function nesting level of 256 reached
toc: true
comment: true
date: 2017-07-26 17:50:04
categories:
tags: [php,xdebug,error]
---


<img src="/images/20170726150106445031039.png" width="492" height="297"/>

Maximum function nesting level of '256' reached, aborting!函数递归深度超过256

<!--more-->
php本身并没有限制函数递归深度，其实是xdebug扩展报的错

检查php的xdebug配置

<img src="/images/20170726150106262652534.png"/>

修改xdebug配置`
/usr/local/etc/php/7.0/conf.d/ext-xdebug.ini`

```
xdebug.max_nesting_level=512
```


重启 php-fpm,生效

