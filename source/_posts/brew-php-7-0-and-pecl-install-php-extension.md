---
title: 使用pecl终端命令安装php扩展
toc: true
comment: true
date: 2018-04-27 14:28:17
categories: php
tags: pecl
---



brew不支持php70扩展的安装了，改用pecl

``` shell
➜  conf.d brew search php70
==> Searching local taps...
==> Searching taps on GitHub...
==> Searching blacklisted, migrated and deleted formulae...
It was migrated from josegonzalez/php to homebrew/core.
```


<!--more-->

## 安装PHP@7.0

```shell
brew install php@7.0
```

安装完要配置环境变量,加入`.zshrc`文件

```shell
export PATH="$(brew --prefix php@7.0)/sbin:$PATH"
export PATH="/usr/local/bin:/usr/local/sbin:$PATH"
```
启动关闭的命令也变了

```shell
//启动php-fpm
sudo php-fpm

//关闭php-fpm
sudo pkill php-fpm
```

## 安装pear

参考一下的教程，安装pear，安装完之后就可以使用pecl命令安装管理php扩展了

[在Mac上安装pecl](https://www.jianshu.com/p/598c0fd84719)

## pecl命令

- pecl search xxxx 查找扩展
- pecl install xxxx 安装扩展
- pecl list xxxx  查看已安装扩展列表

## 扩展的配置

以前brew安装php70的扩展都是放在conf.d文件夹下的，而现在php@7.0的扩展安装完之后之前会自动在`php.ini`文件中开启

以protobuf扩展为例，我们通过`pecl install protobuf`安装完成之后,在终端日志最后可以看到以下内容

```shell
Build process completed successfully
Installing '/usr/local/Cellar/php@7.0/7.0.29_1/pecl/20151012/protobuf.so'
install ok: channel://pecl.php.net/protobuf-3.5.1.1
Extension protobuf enabled in php.ini
```
`/usr/local/Cellar/php@7.0/7.0.29_1/pecl/20151012/protobuf.so`是扩展所在的目录

打开`php.ini`文件,
第一行新增了

```ini
extension="protobuf.so"
```
将其注释掉

在conf.d目录下新建文件`ext-protobuf.ini`，编辑如下：

```ini
[protobuf]
extension="/usr/local/Cellar/php@7.0/7.0.29_1/pecl/20151012/protobuf.so"
```

## php的配置

brew安装的php70时，php.ini文件是不生效的
但是brew安装php@7.0，php.ini文件是生效的

### obcache
默认打开了obcache，影响本地测试，需要关闭

修改php.ini

```ini
[opcache]
; Determines if Zend OPCache is enabled
opcache.enable=0
```
