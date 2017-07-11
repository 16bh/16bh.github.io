---
title: python安装requests库
toc: false
date: 2016-07-07 20:37:15
category: [IT,python]
tags: python
---

> 墙裂推荐史上最简单的`markdown`图片使用方法：[markdown图片实用工具](https://github.com/tiann/markdown-img-upload)。通过`Alfred`的工作流和七牛云存储相结合的方法，复制图片粘贴到编辑器自动生成图片链接
> 
>其中，`Alfred`用到的`python`脚本依赖`requests`库,而网上很多人的`pip`安装方法不成功，其实因为你电脑安装了不同版本的`python`
> 
> 

安装python的requests，网上推荐的大部分是`pip`方法

``` shell
sudo easy_install pip   //安装pip
sudo pip install requests   //安装requests
```

执行后在python控制台查看所有已安装的模块：

``` shell
>>> help('modules')
```

未发现requests

<!--more-->

先执行

``` shell
python
```

查看当前python的版本
<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467904179678.png" width="292"/>

如图，正运行的版本是2.7

再去`python`的根目录查看当前安装了几个版本

```
cd /Library/python
ll
```

<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467904516625.png" width="281"/>

不出意外，电脑里有2.6和2.7两个版本，pip默认安装到了2.6版本

``` shell
curl -OL https://github.com/kennethreitz/requests/zipball/master
mv ./master ./master.tar.gz    //下载下来的文件没有后缀，手动加上`.tar`
tar -xf ./master.tar.gz
cd kennethreitz-requests-7700eca
python2.7 setup.py install    //不要运行python命令，加上你的python版本号
```

这样，就为正在运行的`python`安装好`requests`库了