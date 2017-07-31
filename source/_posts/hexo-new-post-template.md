---
title: hexo默认文章的模板修改
date: 2016-07-06 14:41:14
category:
tags: hexo
---

> 新增了文章目录功能后，每次新建文章时都需要加上`toc: true`，修改默认的文章模板，下次新建时就不用手动输入了

直接修改`/scaffolds/post.md`,加入`toc: true`即可

```
---
title: {{ title }}
date: {{ date }}
tags:
toc: true
---

```
