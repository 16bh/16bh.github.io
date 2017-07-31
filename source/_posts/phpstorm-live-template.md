---
title: phpstorm使用代码片段
toc: true
comment: true
date: 2017-04-01 10:22:30
categories:
tags: phpstorm
---



<img src="http://o9xbyqajf.bkt.clouddn.com/20170726150106594122661.png" width="492" height="297"/>


<!--more-->


用过magento的人起码手动输入过上百次以下的代码了
``` php
Mage::log($test,null,'test.log');
$order = Mage::getModel('sales/order')->loadByIncrementId($orderNumber);
$customer = Mage::getModel('customer/customer')->load($customer_id);
```

其实这些常用的代码可以设置成代码片段
路径：`Editor/Live Templates`

![20170407149153181620126.png](http://o9xbyqajf.bkt.clouddn.com/20170407149153181620126.png)
如图，点击右上角的+号可以新增代码片段
`Abbreviation`表示设置的片段的关键字
`Description`是关键字可以不填
`Template text`是片段的内容

我们新建一个片段叫`order`，内容为：

```
$order = Mage::getModel('sales/order')->loadByIncrementId($END$);//$END$是光标最后会停留的位置，可以输入用户自定义的订单编号
```

有两种触发片段的方法

- 按快捷键展开
 ![20170407149153260586416.png](http://o9xbyqajf.bkt.clouddn.com/20170407149153260586416.png)
- 直接输入片段的关键字，`Enter`确认后展开
![http://o9xbyqajf.bkt.clouddn.com/QQ20170407-104052-HD.gif](http://o9xbyqajf.bkt.clouddn.com/QQ20170407-104052-HD.gif)


可以将多个位置设置成同一变量，如下所示
![20170407149155255061216.png](http://o9xbyqajf.bkt.clouddn.com/20170407149155255061216.png)
效果如图：

![20170407149157042959651.gif](http://o9xbyqajf.bkt.clouddn.com/20170407149157042959651.gif)



---
更新：2017年7月21日

看了一篇文章作者的设定,将最常用的符号也设置为代码片段

d  触发 $
a  触发 =>
o  触发 ->
