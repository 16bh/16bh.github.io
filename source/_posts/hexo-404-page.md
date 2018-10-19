---
title: 设置hexo404页面
toc: false
date: 2016-07-13 11:36:35
categories: [Blog]
tags: hexo
---

不爽默认的404页面，那么就换一个吧

在主题的`source`目录下新建`404.html`，编辑如下，注意修改第10行`homePageUrl`的值。


<!--more-->


``` html /hexo/themes/landscape-plus/source/404.html
<!DOCTYPE HTML>
<html>
<head>
  <meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="robots" content="all" />
  <meta name="robots" content="index,follow"/>
</head>
<body
<script type="text/javascript" src="http://www.qq.com/404/search_children.js" charset="utf-8" homePageUrl="http:/16bh.github.io" homePageName="回到我的主页"></script>
</body>
</html>
```
