---
title: 访问模块中的controller
date: 2016-06-30 18:27:55
category:
tags: magento
toc: true
---

>magento与别的框架的不同之处之一：路由规则通过xml文件进行配置
参考：《深入理解magento 第二章》

#controller文件
之前我们新成立的Nano公司建了如下的模块，
![](http://o9xbyqajf.bkt.clouddn.com/images/1468037922718.png)

完善一下HelloWorldController

``` php magento-practise.local/app/code/local/Nano/App/controllers/HelloWorldController.php
<?php
//自己定义的前台的控制器都应继承Mage_Core_Controller_Front_Action
//类名称的格式为：模块名字空间_模块名称_controller名称
class Nano_App_HelloWorldController extends Mage_Core_Controller_Front_Action
{
    //默认控制器
    public function indexAction()
    {
        echo '默认的action，如果没有指定action的话就会访问它';
    }

    public function sayAction()
    {
        echo "Hello World!";
    }
}
```

如何访问`controllers`下的`HelloWorldController.php`呢?

#修改模块配置文件的路由规则
编辑`app\etc\config.xml`

``` xml magento-practise.local/app/code/local/Nano/App/etc/config.xml
<?xml version="1.0"?>
<config>
    <modules>
        <Nano_App>
            <version>0.0.1</version>
        </Nano_App>
    </modules>

    <frontend><!--frontend是网站前台，admin是网站后台，install是magento的安装程序-->
        <routers>
            <Nano_App><!--路由的标识，要唯一 -->
                <use>standard</use>
                <args>
                    <module>Nano_App</module><!--模块-->
                    <frontName>app</frontName><!--在url中通过app就可以访问到Nano_App-->
                 </args>
            </Nano_App>
        </routers>
    </frontend>

</config>

```

同样，清除magento的缓存使得配置文件生效之后，我们在浏览器上请求
[jim.practise.com/index.php/app/helloWorld/say](locahost/index.php/magento/app/helloWorld/say)
那么就会访问到`HelloWorldController`下的`sayAction`了
而请求

[jim.practise.com/index.php/app/helloWorld](localost/index.php/magento/app/helloWorld)
或
[jim.practise.com/index.php/app/helloWorld/index](localhost/index.php/magento/app/helloWorld/index)
就会访问到`HelloWorldController`下的`indexAction`


>注：本地域名需要根据本地电脑的配置进行替换,`jim.practise.com`是我本地配置的域名，指向项目文件的根目录
