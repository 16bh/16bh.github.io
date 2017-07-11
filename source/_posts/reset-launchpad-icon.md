---
title: 重新排序Launchpad图标
date: 2016-06-16 22:51:31
category: Mac
tags: mac
---


在终端执行：

``` shell
defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock
```
