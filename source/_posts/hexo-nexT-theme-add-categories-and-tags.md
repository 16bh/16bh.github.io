---
title: hexo nexT主题新增分类页和标签页
categories:
toc: false
comment: true
date: 2017-03-30 19:35:59
tags: hexo
---




切换到nexT主题后，默认是没有分类页和标签页的，要自己新建。

<!--more-->

## 新增菜单
编辑`主题配置文件`

``` yml hexo/themes/next/_config.yml
menu:
  home: /
  categories: /categories
  #about: /about
  archives: /archives
  tags: /tags
  #sitemap: /sitemap.xml
  #commonweal: /404.html
```

## 新建页面
在终端执行

``` shell
hexo new page tags
hexo new page categories
```

## 编辑分类页标签页
在分类页和标签页的md文件头部加上types指明页面的类型就行了

``` hexo/source/categories/index.md
---
title: categories
date: 2017-03-30 19:32:41
type: "categories"
---

```

``` md hexo/source/tags/index.md
---
title: tags
date: 2016-07-28 17:00:34
type: "tags"
---

```
