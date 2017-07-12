---
title: 安装redis后清除magento缓存失效解决方案
date: 2016-06-30 18:30:57
category:
tags: [magento,redis]
---

>在[《如何清除magento缓存》](https://16bh.github.io/2016/07/05/%E5%A6%82%E4%BD%95%E6%B8%85%E9%99%A4magento%E7%BC%93%E5%AD%98/)一文中介绍了清除magento缓存的三种方法

6月27日

---
前几天给mac安装了redis服务器之后，今天在开发的过程中，先修改了一些配置文件，然后像往常一样用删除var下的cache目录的方法清除缓存后，发现配置文件未生效

---

原因：magento缓存和redis缓存
解决方法：清除所有redis的缓存

``` shell
redis-cli  //打开redis服务器的客户端
flushall  //清除所有redis服务内容
```