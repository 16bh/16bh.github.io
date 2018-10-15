---
title: '[magento]Order对象的save方法执行哪些操作？'
toc: false
comment: true
date: 2017-03-30 14:31:19
categories:
tags: magento
---

![20170330149085600641699.png](/images/20170330149085600641699.png)
保存订单对象时除了更新sales_flat_order表，还会：

 >
 - _beforeSave方法
 - _afterSave方法
 - order_save_after事件




<!--more-->

## before save
 - 检查state
 - 设置店名
 - 设置订单号

 > magento自带的通过对象的方式生成订单号的做法影响下单时的性能，可以通过redis的方式自动生成订单号

 - 设置item数量
 - 设置用户id
 - 设置账单地址
 - 设置物流地址

``` php app/code/core/Mage/Sales/Model/Order.php
 protected function _beforeSave()
    {
        parent::_beforeSave();//触发model_save_before和core_abstract_save_before事件
        $this->_checkState();//检查state，注1
        if (!$this->getId()) {//新建订单设置store名称
            $store = $this->getStore();
            $name = array($store->getWebsite()->getName(),$store->getGroup()->getName(),$store->getName());
            $this->setStoreName(implode("\n", $name));
        }

        if (!$this->getIncrementId()) {//没有订单号
            $incrementId = Mage::getSingleton('eav/config')
                ->getEntityType('order')
                ->fetchNewIncrementId($this->getStoreId());//生成订单号，注2
            $this->setIncrementId($incrementId);//设置订单号
        }

        /**
         * Process items dependency for new order
         */
        if (!$this->getId()) {
            $itemsCount = 0;
            foreach ($this->getAllItems() as $item) {
                $parent = $item->getQuoteParentItemId();
                if ($parent && !$item->getParentItem()) {
                    $item->setParentItem($this->getItemByQuoteItemId($parent));
                } elseif (!$parent) {
                    $itemsCount++;
                }
            }
            // Set items count
            $this->setTotalItemCount($itemsCount);
        }
        if ($this->getCustomer()) {
            $this->setCustomerId($this->getCustomer()->getId());
        }

        if ($this->hasBillingAddressId() && $this->getBillingAddressId() === null) {
            $this->unsBillingAddressId();
        }

        if ($this->hasShippingAddressId() && $this->getShippingAddressId() === null) {
            $this->unsShippingAddressId();
        }

        $this->setData('protect_code', substr(md5(uniqid(mt_rand(), true) . ':' . microtime(true)), 5, 6));
        return $this;
    }
```

其中，checkState方法有一个注意事项：
如果订单实付金额为0（使用了优惠券等情况下），订单的state不是canceled，也不是complete，那么就会被置为closed

``` php app/code/core/Mage/Sales/Model/Order.php
protected function _checkState()
    {
        if (!$this->getId()) {//新建的订单下面的代码不会生效
            return $this;
        }

        $userNotification = $this->hasCustomerNoteNotify() ? $this->getCustomerNoteNotify() : null;//通知顾客

        if (!$this->isCanceled()
            && !$this->canUnhold()
            && !$this->canInvoice()
            && !$this->canShip()) {
            if (0 == $this->getBaseGrandTotal() || $this->canCreditmemo()) {
                if ($this->getState() !== self::STATE_COMPLETE) {
                    $this->_setState(self::STATE_COMPLETE, true, '', $userNotification);
                }
            }
            /**
             * Order can be closed just in case when we have refunded amount.
             * In case of "0" grand total order checking ForcedCanCreditmemo flag
             */
            elseif (floatval($this->getTotalRefunded()) || (!$this->getTotalRefunded()
                && $this->hasForcedCanCreditmemo())
            ) {
                if ($this->getState() !== self::STATE_CLOSED) {
                    $this->_setState(self::STATE_CLOSED, true, '', $userNotification);
                }
            }
        }

        if ($this->getState() == self::STATE_NEW && $this->getIsInProcess()) {
            $this->setState(self::STATE_PROCESSING, true, '', $userNotification);
        }
        return $this;
    }
```

## after save

``` php app/code/core/Mage/Sales/Model/Order.php
protected function _afterSave()
    {
        if (null !== $this->_addresses) {
            $this->_addresses->save();
            $billingAddress = $this->getBillingAddress();
            $attributesForSave = array();
            if ($billingAddress && $this->getBillingAddressId() != $billingAddress->getId()) {
                $this->setBillingAddressId($billingAddress->getId());
                $attributesForSave[] = 'billing_address_id';
            }

            $shippingAddress = $this->getShippingAddress();
            if ($shippingAddress && $this->getShippigAddressId() != $shippingAddress->getId()) {
                $this->setShippingAddressId($shippingAddress->getId());
                $attributesForSave[] = 'shipping_address_id';
            }

            if (!empty($attributesForSave)) {
                $this->_getResource()->saveAttribute($this, $attributesForSave);
            }

        }
        if (null !== $this->_items) {
            $this->_items->save();
        }
        if (null !== $this->_payments) {
            $this->_payments->save();
        }
        if (null !== $this->_statusHistory) {
            $this->_statusHistory->save();
        }
        foreach ($this->getRelatedObjects() as $object) {
            $object->save();
        }
        return parent::_afterSave(); //触发model_save_after和core_abstract_save_after事件
    }
```

## 监控sales_order_save_after事件
![2017033014908558291593.png](/images/2017033014908558291593.png)
