---
title: 禁用magento模块
date: 2016-06-30 18:27:32
category: Magento
tags: magento
---


> 有时候，我们需要禁用一些不用的模块，如magento核心模块中的Authorizenet模块是国外支付用的一个模块，国内商城是用不上的，可以禁用，让magento更轻便

访问magento后台`localhost/magento/admin`
选择`System/Configuration`
在左侧选择`ADVANED/Advanced`，
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1903856-cb84f511b6388b7e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在右侧展示的是所有已激活的模块列表

![](http://upload-images.jianshu.io/upload_images/1903856-a8e371b2a6b41166.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

找到你要禁用的模块，将模块右侧的状态从‘Enable’改成‘Disable’就可以禁用该模块了，如图所示

![](http://upload-images.jianshu.io/upload_images/1903856-d528da826076ded9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)