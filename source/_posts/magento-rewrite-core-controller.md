---
title: magento复写core中的controller
toc: false
date: 2016-07-07 18:20:00
category:
tags: magento
---

>我们想要对`core`中的一些模块的`controller`里的一些方法进行修改，自然不能直接在`controller`中修改，要通过复写(`rewrite`)的方法在`local`中操作
>复写的原理是同名的模块会按优先级覆盖，优先级为：`local` > `community` > `core`

以复写`Customer/AccountController.php`为例
![](http://o9xbyqajf.bkt.clouddn.com/images/1468163108242.png)


<!--more-->

先在`controllers`目录下新建`Customer`文件夹,建立`Nano_App_AccountController`类文件，继承原有的`Mage_Customer_AccountController`类

``` php app/code/local/Nano/App/controllers/Customer/AccountController.php
<?php
require_once Mage::getModuleDir('controllers', "Mage_Customer").DS."AccountController.php";
class Nano_App_AccountController extends Mage_Customer_AccountController
{
    /**
     * Login post action
     */
    public function loginPostAction()
    {
        echo 'login post has been rewritten';
    }
} 
```

再修改`app`模块的配置文件`config.xml`，在`global`标签下对`AccountContoller`进行复写

``` xml app/code/local/Nano/App/etc/config.xml
<global>
    <!-......-->
     <rewrite>
         <Nano_App>
              <from><![CDATA[#^/customer/account/loginPost/#]]></from>
              <to>/app/customer/account/loginPost/</to>
          </Nano_App>
      </rewrite>
      <!-......-->
</global>
```

