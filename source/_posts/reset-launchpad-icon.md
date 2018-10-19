---
title: 重新排序Launchpad图标
date: 2016-06-16 22:51:31
categories: Software
tags: launchpad
---



在终端执行：

``` shell
defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock
```

复原：

```shell
defaults write com.apple.dock ResetLaunchPad -bool false; killall Dock
```

