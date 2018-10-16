---
title: hexo菜单栏创建留言板
date: 2016-07-06 13:34:33
category:
tags: hexo
---



在命令行里面输入：

``` shell
hexo new page "message"
```
然后你会发现source里面多了个目录message，里面有个index.md


再编辑`themes/landscape-plus/_config.yml`，加入`留言板: /message`,如下所示：

``` yml
# Header
menu:
  本站首页: /
  所有文章: /archives
  留言板: /message
rss: /atom.xml
```

最后，将改动提交

``` shell
hexo g -d
```

