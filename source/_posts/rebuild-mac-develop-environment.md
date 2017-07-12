---
title: 从零搭建mac开发环境
categories: 
tags: mac
toc: false
comment: true
date: 2017-05-10 21:48:02
---



从零安装开发环境


<!--more-->

# 系统设置
- 登录apple账号
- 将不常用的app折叠到文件夹中
![20170628149862006734533.png](http://o9xbyqajf.bkt.clouddn.com/20170628149862006734533.png)
-  设置快捷键
- 设置触摸板（三指拖拽功能在`辅助功能`中设置）
- 设置触发角
![20170624149830172871625.png](http://o9xbyqajf.bkt.clouddn.com/20170624149830172871625.png)
- 下载已购项目
- 设置dock

![201706261498466531224.png](http://o9xbyqajf.bkt.clouddn.com/201706261498466531224.png)
置于左侧
将窗口最小化为应用程序图标

# 环境搭建
## 安装homebrew

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
## 通过homebrew安装homebrew-cask

```
brew tap caskroom/cask
```
> 正常的软件通过appstore多dmg安装文件安装，正常渠道无法安装的采用brew cask

## shadowsocksx和chrome

```
brew cask install shadowsocksx
```

- 开启shadowsocksx,登录chrome浏览器，同步书签和插件
- 安装alfred并安装chrome书签的workflow

## git
- 安装xcode
- 安装git
> 安装了xcode后，在终端输入git命令即可安装git

[怎样在一台电脑上同时使用公司 GitLab 和 Github 的服务](https://github.com/xirong/my-git/blob/master/use-gitlab-github-together.md)


## iterm2和oh my zsh

 下载安装iterm2

[https://www.iterm2.com/downloads.html](https://www.iterm2.com/downloads.html)


- 安装oh my zsh

```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

- 安装wd和zsh-wakatime插件
- 设置主题为powerline并安装powerline等宽字体

```
git clone https://github.com/powerline/fonts.git
cd fonts
./install.sh
cd .. && rm -rf fonts
```

设置等宽字体
Profiles - Text - Font

- iterm2也可以使用`robbyrussell`主题和`Arthur`配色方案
（Laravel作者推荐）

- 使用zsh

```
chsh -s /bin/zsh
```

## 编译安装vim

## 安装nginx

	```brew install nginx```
	
	- 配置servers文件
	- 设置pid和log路径

## 安装php

	```brew install php70```
	
	- 设置环境变量
	- 设置pid和log路径
	- 安装扩展

	编译安装
	
## 安装phpstorm
	- 下载安装
	- 导入配置（安装前导出备份） 
	- 安装必要的插件

## 安装redis

	- `brew install redis`
	- 查看启动命令 `brew info redis`
	- 设置pid和log路径
	- 关闭持久化

## 建议pid和log目录

pid: /usr/local/var/run
log: /usr/local/var/log


## 安装mysql
- 下载

[下载安装：http://www.cnblogs.com/macro-cheng/archive/2011/10/25/mysql-001.html](http://www.cnblogs.com/macro-cheng/archive/2011/10/25/mysql-001.html)

> 注意：安装的某一步中会给出mysql的密码，要记录一下，用户后面登录cli并修改密码

- 安装
[配置：http://www.jianshu.com/p/fd3aae701db9
](http://www.jianshu.com/p/fd3aae701db9
)

- 修改mysql密码

## tree
- 安装tree

`brew install tree`

## node
- 安装node

`brew install node`

- 用淘宝的源
`npm install -g cnpm --registry=https://registry.npm.taobao.org`
然后就可以用cnpm代替npm安装包了


# 重要软件
- 安装reeder，登录inoreader账号
- 安装quiver、paste、yonik、bartender、moom、dash等常用软件
![20170626149846649474604.png](http://o9xbyqajf.bkt.clouddn.com/20170626149846649474604.png)


# 设置开启启动app
![20170626149846660040418.png](http://o9xbyqajf.bkt.clouddn.com/20170626149846660040418.png)


# 其他
- 安装hexo
> 前提是安装了node

[迁移hexo](https://www.zhihu.com/question/21193762)



