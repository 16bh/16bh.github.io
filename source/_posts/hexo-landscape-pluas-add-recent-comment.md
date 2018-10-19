---
title: hexo侧边栏安装最近评论小物件
date: 2016-07-06 14:10:06
categories: [Blog]
tags: hexo
---

> 前提：你的hexo已经配置了多说

多说已经倒闭很多年了

---



先`themes/landscape-plus/layout/_widget`目录下新建小物件`duoshuo_recent_comments.ejs`，编辑如下：


``` js
<% if (theme.duoshuo_shortname){ %>
<div class="widget-wrap">
  <h3 class="widget-title">最近评论</h3>
<div class="widget">
<ul class="ds-recent-comments" data-num-items="5" data-show-avatars="1" data-show-time="1" data-show-title="1" data-show-admin="1" data-excerpt-length="70"></ul>
</div>
  </div>
<% } %>
```

再修改主题的配置`themes/landscape-plus/_config.yml`


``` yml
# Sidebar
sidebar: right
widgets:
- recent_posts
- category
- tag
- tagcloud
- archive
- links
- duoshuo_recent_comments    //与小物件的名称保持一致
```
