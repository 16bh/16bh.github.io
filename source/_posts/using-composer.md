---
title: 使用composer
toc: true
comment: true
date: 2017-08-04 15:27:25
categories:
tags: php
---



<img src="http://o9xbyqajf.bkt.clouddn.com/20170804150183174467257.png" width="492" height="297"/>


<!--more-->

# 安装composer

```
brew install composer
```

# 修改源

方法一： 修改 composer 的全局配置文件（推荐方式）
打开命令行窗口（windows用户）或控制台（Linux、Mac 用户）并执行如下命令：

```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

方法二： 修改当前项目的 composer.json 配置文件：
打开命令行窗口（windows用户）或控制台（Linux、Mac 用户），进入你的项目的根目录（也就是 composer.json 文件所在目录），执行如下命令：

```
composer config repo.packagist composer https://packagist.phpcomposer.com
```

上述命令将会在当前项目中的 composer.json 文件的末尾自动添加镜像的配置信息（你也可以自己手工添加）：
```
"repositories": {
    "packagist": {
        "type": "composer",
        "url": "https://packagist.phpcomposer.com"
    }
}
```


# composer使用


