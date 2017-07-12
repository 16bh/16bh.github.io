---
title: 将Hexo网站托管到Coding.net
toc: true
comment: true
date: 2017-07-12 16:37:04
categories:
tags: website
---



使用Coding提供的pages服务，将网站的代码备份一份在Coding.net
修改域名解析，访问网站时国内用户访问github pages，国内用户访问coding pages

<!--more-->

# 新建Coding的pages仓库

只需要注册[coding.net](https://coding.net/register?key=d59a5269-0dd0-4a51-b48a-0bba7c611a1b),然后建立一个名为`用户名+coding.me`的仓库即可，需要注意的是 coding.net的pages仓库只能有一个master分支

[开始使用 Coding Pages官方帮助文档](https://coding.net/help/doc/pages/getting-started.html)

> Coding Pages 分为「用户 Pages」与「项目 Pages」两种类型。查看详细介绍
> 
> 如果您希望创建「用户 Pages」（直接访问 {user_name}.coding.me 即可抵达您网站），只需要新建一个名为 {user_name}.coding.me 的项目即可。{user_name} 指代您本人的个性后缀，使用其他人的个性后缀不会被归为「用户 Pages」类型。
> 
> 除 {user_name}.coding.me 项目外，每一个项目都可以创建「项目 Pages」，无需额外操作。
> 
> Coding Pages 设置选项在每个项目的「代码 -> Pages 服务」中。
> 


# 设置hexo deploy的时候提交到coding.net

修改站点配置文件`_config.yml`

```
repository:
    coding: git@git.coding.net:{user_name}/{user_name}.coding.me.git,master
    github: git@github.com:16bh/{user_name}.github.io.git,master
```


# 设置DNSPod域名解析
![20170712149985102430955.png](http://o9xbyqajf.bkt.clouddn.com/20170712149985102430955.png)


最后，为了看是否生效，可以[使用mtr检测域名的网络状态](http://jimxu.me/2017/07/12/use-mtr-detect-network-status/)

