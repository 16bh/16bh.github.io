---
title: 解决hexo的landscape-plus主题标签和归档无法分页的bug
toc: false
date: 2016-07-06 15:23:12
cagetory: Hexo
tags: hexo
---

>主题自带的bug导致的


修改文件`hexo/themes/landscape-plus/layout/_partial/archive.ejs`，在倒数第二行加入如下内容：

``` js
<nav id="page-nav"> <%- paginator({ prev_text: "<< Prev", next_text: "Next >>" }) %> </nav>
```

其中，上一页和下一页的样式可自行修改

修改后的效果见：https://16bh.github.io/archives/