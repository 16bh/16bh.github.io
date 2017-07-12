---
title: 在Finder中查看隐藏文件
date: 2016-07-05 22:48:16
category: 
tags: mac
---

##方法1：
在终端中执行：

``` shell
defaults write com.apple.Finder AppleShowAllFiles YES
```

再按住`Option`键，单击`Finder`的图标不放，选择`重新开启`,即可看到隐藏文件



要取消的话，执行：

``` shell
defaults write com.apple.Finder AppleShowAllFiles NO
```

再重启`Finder`即可

## 方法2

使用快捷键：
`command+shif+.`

