---
title: magento常用方法
toc: true
date: 2016-07-12 15:41:35
categories: Magento
tags: magento
---



记录常用的Magento方法


<!--more-->

# 调用助手类

``` php
Mage::helper()->functionInHelper();
```

# 获取数据库对象

``` php
$object = Mage::Model();
```
        
以及可用的方法：

``` php
$object -> getData();//取数据
$object -> setData();//写入数据
```
# 日志

``` php
Mage::log();
Mage::logException();
```

      
# 获取入参,可以设置默认值

``` php
$id = $this->getRequest()->getParam('id',null);
```

# 获取用户session对象

``` php
$session = Mage::getSingleton('customer/session');
```

以及可以使用方法

``` php
$session->login($user,$pass);  //登录
$session->logout();              //登出
$session->isLoggedIn();        //判断是否登录
$customer = $session->getCustomer();
```
    

# 获取系统session对象

``` php
$session = Mage::getSingleton('core/session');
```

# 获取ip

``` php
$ip = Mage::helper('core/http')->getRemoteAddr()
```
    
# 获取顾客对象
## 根据id获取对象
 
``` php
$customer = Mage::getModel('customer/customer')
				->load($id);
```

## 根据email获取对象

``` php
$customer = Mage::getModel('customer/customer')
                ->setWebsiteId(Mage::app()->getStore()->getWebsiteId())
                ->loadByEmail($email);
```

# 获取产品对象

``` php
$product = Mage::getModel('catalog/product');
```
    
# 获取订单对象

``` php
$order = Mage::getModel('sales/order');
```

# 获取店铺对象
 
``` php
$store = Mage::app()->getStore();
```
    
# 获取商品库存

``` php
$qty = (int)Mage::getModel('cataloginventory/stock_item')->loadByProduct($product)->getQty()；
```

# 获取类名

``` php
get_class()
```

# 输出magento的配置文件

``` php
header('Content-Type: text/plain'); echo $config = Mage::getConfig() ->loadModulesConfiguration('config.xml') ->getNode() ->asXML(); exit;
    }
```

# 获取storeId

``` php
Mage::app()->getStore()
```

# 获取websiteId
``` php
Mage::app()->getStore()->getWebsiteId()
```

