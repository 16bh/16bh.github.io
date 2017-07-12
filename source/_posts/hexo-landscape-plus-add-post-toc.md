---
title: 'landscape-plus主题增加hexo文章目录功能'
toc: false
date: 2016-07-06 14:59:23
category:
tags: website
---

第一步，编辑`themes\landscape-plus\layout\_partial\article.ejs`文件，在`<%- post.content %>`这一行之前加入如下代码:

``` js
<!-- Table of Contents -->
<% if (!index && post.toc){ %>
  <div id="toc" class="toc-article">
    <strong class="toc-title">文章目录</strong>
    <%- toc(post.content) %>
  </div>
<% } %>
```

<!--more-->

插入后为：

``` js
 <% } else { %>
      <!-- Table of Contents -->
<% if (!index && post.toc){ %>
  <div id="toc" class="toc-article">
    <strong class="toc-title">文章目录</strong>
    <%- toc(post.content) %>
  </div>
<% } %>
        <%- post.content %>
```

第二步，编辑文件`themes\landscape-plus\source\css\_partial\article.styl`，在最后添加如下代码：

``` styl
/*toc*/
.toc-article
  background #eee
  border 1px solid #bbb
  border-radius 10px
  margin 1.5em 0 0.3em 1.5em
  padding 1.2em 1em 0 1em
  max-width 28%
.toc-title
  font-size 120%
#toc
  line-height 1em
  font-size 0.9em
  float right
  .toc
    padding 0
    margin 1em
    line-height 1.8em
    li
      list-style-type none
  .toc-child 
    margin-left 1em
```