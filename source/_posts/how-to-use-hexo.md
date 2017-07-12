---
title: 在搭建hexo时碰到的问题
date: 2016-07-05 17:14:59
category: 
tags: website
toc: true
---
>通过github和hexo搭建博客

# 解决在同一台电脑上使用github与gitlab的问题
参考这篇博文:https://github.com/xirong/my-git/blob/master/use-gitlab-github-together.md

方法是一个仓库使用git的全局配置，一个仓库使用git的本地配置


生成公钥的时候指定生成的文件名就可以分别生成github和gitlab的公钥了

``` shell
ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "sample@126.com"
```

# 安装node.js
最快捷的方式还是用brew来安装

``` shell
brew install node.js
```

# 安装hexo

``` shell
npm install -a hexo
```

# 常用hexo命令
输入`hexo`可获取所有常用命令

```
  clean     Removed generated files and cache.
  config    Get or set configurations.
  d(eploy)    Deploy your website.
  g(enerate)  Generate static files.
  help      Get help on a command.
  init      Create a new Hexo folder.
  list      List the information of the site
  migrate   Migrate your site from other system to Hexo.
  new       Create a new post.
  publish   Moves a draft post from _drafts to _posts folder.
  render    Render files with renderer plugins.
  server    Start the server.
  version   Display version information.
```



# 生成博客后快速用`Mou`打开博客的方法

``` shell
open test.md
```

> 注：open命令会用默认的方式打开指定的文件，相当于双击打开该文件。配置文件默认打开方式的方法：选中.md文件,`command+I`显示简介，选择`打开方式`为`Mou`，点击`全部更改`，如下图所示

![](http://upload-images.jianshu.io/upload_images/1903856-9c3a5ec1253f70b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 安装完成后写一篇博客的过程


``` shell
hexo new 'test.md'    //新建博客
open source/_posts/test.md    //用mou打开，编辑
hexo g    //更新本地库
hexo d    //提交本地修改
```

--- 
update: 2017年7月11日17:11

# 切换主题

以[yilia](https://github.com/litten/hexo-theme-yilia)主题为例

- 将主题clone到本地

```
cd path-to-hexo
cd themes
git clone https://github.com/litten/hexo-theme-yilia
```

- 修改站点配置文件`_config.yml`,启用新的主题

```
theme: hexo-theme-yilia
```

- 清缓存和老的数据

```
cd path-to-hexo
hexo clean
```

- 重新generate

```
hexo g -d
```

