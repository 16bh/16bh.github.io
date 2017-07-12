---
title: MarkDown插入图片技巧
categories:
tags: [markdown]
toc: false
comment: true
date: 2017-04-07 11:39:01
---


![20170407149158020754096.png](http://o9xbyqajf.bkt.clouddn.com/20170407149158020754096.png)

将图片上传到七牛云，获取图片的链接，粘贴到md文件中：
- 通过Alfred的Workflow实现
- 通过U图床或iPic工具实现
- AutoHotkey

<!--more-->
## Alfred
使用方法：截图或复制图片到剪切板后，按workflow的快捷键，workflow自动上传图片并将图片链接保存在剪贴板中
![20170408149162737051667.png](http://o9xbyqajf.bkt.clouddn.com/20170408149162737051667.png)

workflow开发者下载页面：[https://github.com/tiann/markdown-img-upload](https://github.com/tiann/markdown-img-upload)

## U图床/iPic（推荐）
优点：

- 剪切板自动上传
- 拖拽上传，支持gif文件

![20170407149157029132684.gif](http://o9xbyqajf.bkt.clouddn.com/20170407149157029132684.gif)




## AutoHotkey
参考下面的文章

- [AutoHotkey&qshell 实现图片自动上传七牛并返回markdown引用](http://jverson.com/2016/08/30/autohotkey-markdown-uploadImage/)