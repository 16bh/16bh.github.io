---
title: 从零搭建mac开发环境
categories: Mac
tags: []
toc: false
comment: true
date: 2017-05-10 21:48:02
---






<!--more-->

- 登录apple账号
- 设置快捷键
- 设置触摸板（三指拖拽功能在`辅助功能`中设置）
- 设置触发角
- 下载已购项目
- 设置dock
置于左侧
将窗口最小化为应用程序图标
- 安装homebrew

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
- 通过homebrew安装homebrew-cask

```
brew tap caskroom/cask
```

- 通过homebrew-cask安装shadowsocksx

```
brew cask install shadowsocksx
```

- 开启shadowsocksx,登录chrome浏览器，同步书签和插件
- 安装alfred并安装chrome书签的workflow
- 安装git

[怎样在一台电脑上同时使用公司 GitLab 和 Github 的服务](https://github.com/xirong/my-git/blob/master/use-gitlab-github-together.md)

> 终端输入git

- 安装iterm2

```
https://www.iterm2.com/downloads.html
```

- 安装oh my zsh

```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
安装wd和zsh-wakatime插件

设置主题为powerline

安装powerline等宽字体

```
git clone https://github.com/powerline/fonts.git
cd fonts
./install.sh
cd .. && rm -rf fonts
```

设置等宽字体
Profiles - Text - Font

- 使用zsh

```
chsh -s /bin/zsh
```

- 安装nginx
brew install nginx
配置servers文件
设置log路径

- 安装php
brew install php70
设置环境变量
设置log路径
安装扩展

- 安装redis
brew install redis
设置log路径
关闭持久化

- 安装mysql

[下载安装：http://www.cnblogs.com/macro-cheng/archive/2011/10/25/mysql-001.html](http://www.cnblogs.com/macro-cheng/archive/2011/10/25/mysql-001.html)

[配置：http://www.jianshu.com/p/fd3aae701db9
](http://www.jianshu.com/p/fd3aae701db9
)

- 安装reeder，登录inoreader账号
- 安装quiver、paste、yonik、bartender、moom、dash等常用软件
- 安装hexo
- 设置开启启动app

