---
title: windows下通过charles和夜神模拟器对安卓app进行抓包
toc: false
date: 2015-12-21 22:28:27
category: software
tags: [charles]
---

>通过charles对手机app进行抓包，应该算是客户端、服务端、测试应该掌握的基本技能了。如果你没有一台安卓手机，又想抓取安卓app的请求的话，可以考虑在电脑上安装安卓模拟器，然后通过charles或fiddler进行抓包


<!--more-->

# 准备工作

1. 安装抓包工具charles（或fiddler）

<img src="how-to-use-charles-on-windows/1467901924100.png" width="39"/>

2. 安装安卓模拟器

开始装的是bluestacks，但不支持安装内核低的安卓包，卸载的时候还费了老大的劲，完全卸载可参考http://www.ptbus.com/view/41755/。

后来选择了夜神安卓模拟器，效果很赞，免费软件

<img src="how-to-use-charles-on-windows/1467901958901.png" width="40"/>

# 设置
夜神模拟器安装完成后 点`设置-wlan`
>注意：这里说的设置不是安卓模拟器软件顶端的这个设置

<img src="how-to-use-charles-on-windows/1467902016305.png" width="236"/>
而是在模拟的安卓系统内的设置
<img src="how-to-use-charles-on-windows/1467902040285.png" width="172"/>
选择设置中的wifi
<img src="images/images/1467902054467.png" width="225"/>
鼠标长按默认的wifi进入修改界面
<img src="how-to-use-charles-on-windows/1467902073787.png" width="204"/>

点修改网络，选择“显示高级选项”，设置网络代理：主机名设置成你电脑的ip，端口填8888，保存
<img src="how-to-use-charles-on-windows/1467902110604.png" width="199"/>
这样，我们就设置好代理了，然后只要启动抓包工具就可以抓包了。

注意：在设置过代理后，只有先打开下面的抓包工具，安卓模拟器才能正常联网。

# 抓包

打开charles，界面如下
<img src="how-to-use-charles-on-windows/1467902137558.png" width="173"/>
A：清空所有请求

B：打开\关闭 获取请求，在不抓包的时候点B关闭获取请求，降低系统负担

C：获取的请求列表



点击选中一个请求后，在右侧可以看到请求的详细数据
<img src="images/images/1467902151768.png" width="238"/>
overview包含请求的链接

request：请求的入参

response：请求的出参

在respons的最下方可以选择展示的出参的类型：
<img src="how-to-use-charles-on-windows/1467902166891.png" width="148"/>