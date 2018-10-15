---
title: hexo文章的分类和标签
toc: true
date: 2016-07-19 16:48:04
categories:
tags: hexo
---



给博客文章增加分类和标签


<!--more-->

# 如何增加分类和标签
在`markdwon`文件头部的一对`---`标记之间添加 `category: 分类名`和`tags:标签名`

如本文的文件头部如下：
![](/images/images/1468918218644.png)

# 多标签

`tags: [标签1,标签2,标签3]`


# 多级目录

`categories: [一级目录,二级目录]`

# 在侧边栏添加标签和目录

修改主题配置文件：

``` yml hexo/themes/landscape-plus/_config.yml
# Sidebar
sidebar: right
widgets:
- category
- tag
```
