---
title: homebrew、homebrew-cask及cakebrew
date: 2016-06-16 18:19:59
catory:
tags: homebrew
toc: true
---


## 一 用homebrew安装常用包

``` shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

在终端运行`brew`命令可得到常用命令

>Example usage:
  查询包是否存在：brew search [TEXT|/REGEX/]  
  查询包信息及可用安装命令：brew (info|home|options) [FORMULA...]
  安装包：brew install FORMULA... 
  更新homebrew：brew update  
  更新包：brew upgrade [FORMULA...]  
  卸载包：brew uninstall FORMULA...  
  查看已安装包：brew list [FORMULA...]  

>Troubleshooting:
  brew config
  检查homebrew状况：brew doctor  
  brew install -vd FORMULA

>Brewing:
  brew create [URL [--no-fetch]]
  brew edit [FORMULA...]
  https://github.com/Homebrew/brew/blob/master/share/doc/homebrew/Formula-Cookbook.md

>Further help:
  man brew
  brew help [COMMAND]
  brew home

如：
        
      brew search brew-cask
      brew install nginx
      brew search php
      brew uninstall mysql
 

      

## 二 用homebrew-cask安装常用软件
比在网上下载安装文件安装的优势在于：
（1）节省下载安装包的过程，一行命令即可安装
（2）一些在网上搜不到安装文件的软件也可以通过这种方法安装

``` shell
brew tap phinze/homebrew-cask
brew install brew-cask
```

使用方法：将上面的brew换成brew-cask即可，如

       brew-cask install qq

## 三 用cakebrew可视化你的homebrew
如果你不熟悉终端命令，可以下载cakebrew，它是homebrew的客户端，可以实现常用的搜索、安装、卸载操作
官网下载安装

> https://www.cakebrew.com

或执行以下命令

``` shell
brew cask install cakebrew
```
效果图：
![](https://www.cakebrew.com/assets/img/app-bg.png)
