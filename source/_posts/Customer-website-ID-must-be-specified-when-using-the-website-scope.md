---
title: magento报错:Customer website ID must be specified when using the website scope
toc: false
date: 2016-07-21 10:58:20
categories: [IT]
tags: magento
---


根据邮件用户名获取顾客对象时，可以用`Customer`模块自带的`loadByEmail方法`。

``` php app/code/core/Mage/Customer/Model/Customer.php
public function loadByEmail($customerEmail)
    {
        $this->_getResource()->loadByEmail($this, $customerEmail);
        return $this;
    }
```

<!--more-->

但是直接使用下面的方法

``` php
$customer = Mage::getModel('customer/customer')
                ->loadByEmail($email);
```
会报错，错误信息如下：

> Customer website ID must be specified when using the website

事实上，创建`customer`对象时需要指定`websitId`

正确的使用方法如下：

``` php
$customer = Mage::getModel('customer/customer')
                ->setWebsiteId(Mage::app()->getStore()->getWebsiteId())
                ->loadByEmail($email);
```
