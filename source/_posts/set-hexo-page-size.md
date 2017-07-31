---
title: 分别设置hexo首页、标签页、归档页文章个数
toc: false
cagegory: 
date: 2016-07-06 19:12:59
tags: hexo
---
# 开启关闭分页功能
修改配置文件`hexo/_config.yml`，找到如下内容：

``` yml
# Pagination
## Set per_page to 0 to disable pagination
per_page: 10 
pagination_dir: page
```

其中，`per_page`即为你想要设置的分页个数，如果不想分页的话，设置`per_page: 0`即可

# 个性化页面分页

>一般希望首页展示文章的个数少一些，归档页等页面的文章数目多一些

<!--more-->

需要安装一下插件：

```
hexo-generator-archive  //归档页
hexo-generator-category     //分类页
hexo-generator-index    //首页
hexo-generator-tag      //标签页
```

安装方法：
hexo3.0版本已安装
手动安装方法：

``` shell
npm install hexo-generator-archive --save
npm install hexo-generator-category --save
npm install hexo-generator-index --save
npm install hexo-generator-tag --save
```


安装完成后，修改配置文件`hexo/_config.yml`,添加如下内容

``` yml
# Plugins
index_generator:
  per_page: 5 ##首页默认5篇文章标题，如果值为0不分页

archive_generator:
  per_page: 20 ##归档页面默认20篇文章标题，如果值为0不分页
  yearly: true ##生成年视图
  monthly: true ##生成月视图

tag_generator:
  per_page: 20 ##标签页面默认20篇文章，如果值为0不分页

category_generator: 
  per_page: 20 ##分类页面默认20篇文章，如果值为0不分页

```