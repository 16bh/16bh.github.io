---
title: git设置忽略对文件权限进行版本控制
toc: false
date: 2016-07-11 14:08:58
categories: [IT,git]
tags: git
---

`git`有哦时候会记录文件权限的改变，使得权限改变的文件出现在未暂存文件中
这里，只需要修改`git`的配置文件就可以了

进入项目根目录，有个`.git`隐藏文件夹，里面有个`config`文件，即是你这个项目的`git`的配置

``` shell
vim project_root/.git/config
```
打开config文件，编辑如下：

``` config project_root/.git/config
	repositoryformatversion = 0
	filemode = false         //filemode设置为false就不会记录文件权限的变化了
	bare = false
	logallrefupdates = true
	ignorecase = false 
	precomposeunicode = true

```


> 注：git的配置文件共有三处：1)/etc/gitconfig全局配置    2)~/.gitconfig当前用户配置    3）project_root/.git/config当前项目配置