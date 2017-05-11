---
title: hexo的yelee主题设置
toc: true
date: 2016-07-27 12:13:56
categories: Hexo
tags: hexo
---


>yeele主题是个比较成熟的主题，基本上不需要修改源代码，安装各种插件。只修改配置文件就可以得到很好的展示效果



<!--more-->

# 主题配置

``` yml hexo/themes/yelee/_config.yml
menu:	 #主页左侧的菜单栏
  主页: /
  所有文章: /archives/
  Hexo: /tags/hexo	#在菜单栏中展示一个标签
  #标签云: /tags/	#这个会报404，关闭了
  关于我: /about/
  
subnav:	#主页左侧展示的社交账号，如果是网址的话要加上`https://`或`http://`
  Email: "mailto:email_address"
  GitHub: "https://github.com/16bh"
  
duoshuo: 
  on: true
  domain: jimxu #这里填入的是多说账号的shortname
  
friends: # 友情链接功能
  stackoverflow的magento版块: http://magento.stackexchange.com
  程序员技能树: http://skill.phodal.com/#_a2b2c2dekm2_1_Name
```

# 文章置顶功能修复

> 参考了`Netcan`的这篇文章[解决Hexo置顶问题](http://www.netcan666.com/2015/11/22/%E8%A7%A3%E5%86%B3Hexo%E7%BD%AE%E9%A1%B6%E9%97%AE%E9%A2%98/)



