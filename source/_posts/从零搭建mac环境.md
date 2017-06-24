---
title: 从零搭建mac开发环境
categories: Mac
tags: mac
toc: false
comment: true
date: 2017-05-10 21:48:02
---



从零安装开发环境


<!--more-->

- 登录apple账号
- 设置快捷键
- 设置触摸板（三指拖拽功能在`辅助功能`中设置）
- 设置触发角
![20170624149830172871625.png](http://o9xbyqajf.bkt.clouddn.com/20170624149830172871625.png)
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

> 终端输入git命令即可安装git

- 下载安装iterm2

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

- 使用zsh

```
chsh -s /bin/zsh
```

- 安装nginx

	```brew install nginx```
	
	- 配置servers文件
	- 设置log路径

- 安装php！

	```brew install php70```
	
	- 设置环境变量
	- 设置log路径
	- 安装扩展
	
- 安装phpstorm
	- 下载安装
	- 导入配置（安装前导出备份） 
	- 安装必要的插件

- 安装redis

	```brew install redis```
	
	- 设置log路径
	- 关闭持久化

> 建议将php,redis,nginx等错误日志放在一个文件夹中

- 安装mysql

[下载安装：http://www.cnblogs.com/macro-cheng/archive/2011/10/25/mysql-001.html](http://www.cnblogs.com/macro-cheng/archive/2011/10/25/mysql-001.html)

[配置：http://www.jianshu.com/p/fd3aae701db9
](http://www.jianshu.com/p/fd3aae701db9
)

- 安装reeder，登录inoreader账号
- 安装quiver、paste、yonik、bartender、moom、dash等常用软件
- 安装hexo

[迁移hexo](https://www.zhihu.com/question/21193762)

- 设置开启启动app
- 安装tree

```
brew install tree
```

