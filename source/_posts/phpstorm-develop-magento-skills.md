---
title: 用phpStorm进行magento开发的几个Tips
categories: [Editor,phpStorm]
top: 6
toc: false
comment: true
date: 2017-04-01 16:41:58
tags: [magento,phpstorm,php]
---

![20170401149103658911016.png](http://o9xbyqajf.bkt.clouddn.com/20170401149103658911016.png)

- 安装phpcs
- 安装phpmd
- 安装magicento插件
- 只索引有用的文件夹
- 常用magento代码片段


<!--more-->

> 参考：
> https://mirasvit.com/blog/guide-for-setting-up-phpstorm-for-magento-2-developments.html

# 安装phpcs

phpcs可以统一编码的规范，常用的是psr2

[怎么在phpStorm中配置使用phpcs？](http://jimxu.me/2017/04/01/mac%E4%B8%8BphpStorm%E9%85%8D%E7%BD%AE%E4%BD%BF%E7%94%A8phpcs/)



# 安装phpmd

php代码纠错

[怎么在phpStorm中配置使用phpmd？](http://jimxu.me/2017/04/01/mac%E4%B8%8BphpStorm%E9%85%8D%E7%BD%AE%E4%BD%BF%E7%94%A8phpmd/)

# 安装[magicento](http://magicento.com/ )插件
![20170401149103633058337.png](http://o9xbyqajf.bkt.clouddn.com/20170401149103633058337.png)

# 只对用的到的文件夹进行索引
```
/bin/
/dev/
/pub/
/setup/
/var/cache/
/var/log/
/var/page_cache
/var/view_processed
```
建议将以上的文件夹标记为`Excluded`，这样就不会浪费phpStorm的性能对它们进行索引了

![20170401149103630080427.png](http://o9xbyqajf.bkt.clouddn.com/20170401149103630080427.png)

# 设置常用代码片段

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