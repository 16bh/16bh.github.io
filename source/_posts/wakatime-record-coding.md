---
title: 记录你的编程习惯 - 编辑器通用插件：WakaTime
toc: true
date: 2016-07-11 19:16:05
categories: Software
tags: tools
---

>和`RescueTime`等软件不同，`WakaTime`只专注于记录编程相关的活动，即所有你在编辑器中的操作  

先上效果图：
![](http://o9xbyqajf.bkt.clouddn.com/images/1468241463615.png)


<!--more-->

`WakaTime`的使用非常简单，先在[wakaTime的网站](https://wakatime.com)注册一个账号，再根据编辑器的不同安装对应的插件就可以了

# `phpstorm`安装`wakatime`
 - Inside PhpStorm, select Preferences → Plugins → Browse Repositories....

 - Search for wakatime.

 - Click the green Install Plugin button and confirm the installation.

 - Re-launch PhpStorm.

 - Enter your API key , then click Save.
 

# `sublime`安装`wakatime`
 - Install Package Control.

 - Inside Sublime, select Tools → Command Palette...

 - Type install, then select Package Control: Install Package and press Enter.

 - Type wakatime, then select WakaTime and press Enter.

 - Enter your API key , then press Enter

# `vim`安装`wakatime`

 - Install Vundle for Vim.

 - From terminal run:

echo "Plugin 'wakatime/vim-wakatime'" >> ~/.vimrc && vim +PluginInstall

 - (Re-)start Vim and enter your API key , then press Enter.

 
 # 隐私设置
 
 `wakatime`默认会记录你编辑的项目文件名称，如果不想让它记录的话可以修改配置文件`~/.wakatime.cfg`，加上下面这句话：

 ```
 hidefilenames = true
 ``` 

