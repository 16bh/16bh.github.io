---
title: hexo中添加github组件
toc: true
comment: true
date: 2017-07-27 16:29:00
categories:
tags: [hexo,github]
---


<img src="http://o9xbyqajf.bkt.clouddn.com/20170727150114537274249.png" width="492" height="297"/>

Hexo的yelee支持添加github组件

<!--more-->

## 如何开启

修改主题配置文件 `{path_to_hexo}/themes/yelee/_config.yml`, 开启此功能

```
github_widget: true
```

## 如何使用 

在文章中想要添加github组件的地方添加如下代码:

{user_name} github作者名
{project_name} github项目名称
 
```
<div class="github-widget" data-repo="{user_name}/{project_name}"></div>
```


## 示例

例如：

```
<div class="github-widget" data-repo="hustcc/GitHub-Repo-Widget.js"></div>
```

会显示如下效果：

<div class="github-widget" data-repo="hustcc/GitHub-Repo-Widget.js"></div>