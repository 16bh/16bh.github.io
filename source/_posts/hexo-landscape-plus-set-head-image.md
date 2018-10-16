---
title: hexo菜单栏背景图片设置
toc: false
date: 2016-07-08 23:15:35
categories:
tags: hexo
---

landscape-plus主题默认关闭了顶部的大图，如需开启，取消`header.styl`第33行的注释即可。

```styl themes/landscape-plus/source/css/_partial/header.styl
background: url(banner-url) center #000 
```

如需修改高度：
``` styl hexo\themes\landscape-plus\source\css\_variables.styl
banner-height = 280px   //修改menu图片高度
```

随机切换背景图片效果设置：
``` styl hexo\themes\landscape-plus\source\css\_variables.styl
//banner-url = "images/banner.jpg"
banner-url = "https://unsplash.it/1920/280/?random"
```
