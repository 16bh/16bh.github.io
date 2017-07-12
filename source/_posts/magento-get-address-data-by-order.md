---
title: Magento根据订单获取地址信息
categories:
tags: [magento]
toc: false
comment: true
date: 2017-04-06 14:35:24
---

![20170406149146130740929.png](http://o9xbyqajf.bkt.clouddn.com/20170406149146130740929.png)

根据orderid获取address信息


<!--more-->
代码实现：

``` php
$orderModel = Mage::getModel('sales/order')->loadByIncrementId($orderId);
$address = $orderModel->getShippingAddress();
$street = $address->getStreet();
$address_data = array(
    'name' => $address->getData('lastname').$address->getData('firstname'),//姓名
    'phone' => $address->getData('telephone'),//手机号
    'province' => $address->getData('region'),//省
    'city' => $address->getData('city'),//市
    'district' => $street[0],//区
    'street' => $street[1],//街道
);
```


原理：

``` php app/code/core/Mage/Sales/Model/Order.php
public function getShippingAddress()
{
foreach ($this->getAddressesCollection() as $address) {
    if ($address->getAddressType()=='shipping' && !$address->isDeleted()) {
        return $address;
    }
}
return false;
}

 public function getAddressesCollection()
{
    if (is_null($this->_addresses)) {
        $this->_addresses = Mage::getResourceModel('sales/order_address_collection')
            ->setOrderFilter($this);

        if ($this->getId()) {
            foreach ($this->_addresses as $address) {
                $address->setOrder($this);
            }
        }
    }

    return $this->_addresses;
}
```


``` php app/code/core/Mage/Customer/Model/Address/Abstract.php
/**
 * get address street
 *
 * @param   int $line address line index
 * @return  string
 */
public function getStreet($line=0)
{
    $street = parent::getData('street');
    if (-1 === $line) {
        return $street;
    } else {
        $arr = is_array($street) ? $street : explode("\n", $street);
        if (0 === $line || $line === null) {
            return $arr;
        } elseif (isset($arr[$line-1])) {
            return $arr[$line-1];
        } else {
            return '';
        }
    }
}
```