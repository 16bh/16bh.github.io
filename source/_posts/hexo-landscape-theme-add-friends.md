---
title: hexo侧边栏增加链接小物件
date: 2016-07-06 10:27:09
category:
tags: hexo
---

***1. 新建widget***

  `themes/landscape/layout/_widget`目录下新建文件`links.ejs`,并写入一下内容

``` js
<% if (site.posts.length){ %>
  <div class="widget-wrap">
    <h3 class="widget-title">友情链接</h3>
    <div class="widget">
      <ul>
        <% for (var i in (config.links || theme.links)){ %>
          <li>
            <a href="<%- theme.links[i] %>" target="_blank"><%= i %></a>
          </li>
        <% } %>
      </ul>
    </div>
  </div>
<% } %>
```

***2. 修改配置文件***


  `themes/landscape/_config.yml`
这里是要展示的链接的内容

``` yml
# Links
links:
   谷歌: g.cn
```

这里在侧边栏启动widget

``` yml
# Sidebar
sidebar: right
widgets:
- links      //上面新建的文件是links.ejs,这里用links，保持一致
```