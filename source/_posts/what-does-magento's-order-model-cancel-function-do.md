---
title: '[magento]Order对象的cancel方法会执行哪些操作？'
toc: false
date: 2017-03-29 16:53:49
categories: IT
tags: magento
---

用户下单未付款，用户付款后申请取消，...，这些场景时我们需要取消magento中生成的订单，取消的方式如下：


```php
$order->cancel();//取消普通订单
$order->cancelPaidOrder();//取消已付款订单
```

这种对象的方法实现的具体方式是怎样的呢？


<!--more-->
以cancel方法为例，cancelPaidOrder方法类似：

### 取消订单
``` php
$order->cancel();
```

### cancel方法
``` php app/code/core/Mage/Sales/Model/Order.php
 public function cancel()
    {
        if ($this->canCancel()) { //判断订单是否可以取消
            $this->getPayment()->cancel();//取消订单
            $this->registerCancellation();//修改订单表数据，取消item

            Mage::dispatchEvent('order_cancel_after', array('order' => $this));//抛出order_cancel_after事件
        }

        return $this;
    }
```


### registerCancellation方法处理order表和item表的数据
``` php app/code/core/Mage/Sales/Model/Order.php
public function registerCancellation($comment = '', $graceful = true)
    {
        if ($this->canCancel() || $this->isPaymentReview()) {
            $cancelState = self::STATE_CANCELED;
            foreach ($this->getAllItems() as $item) {
                if ($cancelState != self::STATE_PROCESSING && $item->getQtyToRefund()) {
                    if ($item->getQtyToShip() > $item->getQtyToCancel()) {
                        $cancelState = self::STATE_PROCESSING;
                    } else {
                        $cancelState = self::STATE_COMPLETE;
                    }
                }
                $item->cancel(); //订单中的每件商品都要通过item对象的cancel方法处理一遍
            }
            $this->setSubtotalCanceled($this->getSubtotal() - $this->getSubtotalInvoiced());//以下是给order表中跟取消订单相关的字段赋值
            ... ...
            $this->setBaseTotalCanceled($this->getBaseGrandTotal() - $this->getBaseTotalPaid());

            $this->_setState($cancelState, true, $comment);//设置订单的状态
        } elseif (!$graceful) {
            Mage::throwException(Mage::helper('sales')->__('Order does not allow to be canceled.'));
        }
        return $this;
    }
```

### item对象的cancel方法
``` php app/code/core/Mage/Sales/Model/Order/Item.php
 public function cancel()
    {
        if ($this->getStatusId() !== self::STATUS_CANCELED) {
            Mage::dispatchEvent('sales_order_item_cancel', array('item'=>$this));//抛出sales_order_item_cancel事件,事件的参数是item对象
            $this->setQtyCanceled($this->getQtyToCancel());//以下是给item表中跟取消item相关的字段赋值
            $this->setTaxCanceled(
                $this->getTaxCanceled() +
                $this->getBaseTaxAmount() * $this->getQtyCanceled() / $this->getQtyOrdered()
            );
            $this->setHiddenTaxCanceled(
                $this->getHiddenTaxCanceled() +
                $this->getHiddenTaxAmount() * $this->getQtyCanceled() / $this->getQtyOrdered()
            );
        }
        return $this;
    }
```

### 监控sales_order_item_cancel事件，触发商品还库存操作
``` xml app/code/core/Mage/CatalogInventory/etc/config.xml
<sales_order_item_cancel>
                <observers>
                    <inventory>
                        <class>cataloginventory/observer</class>
                        <method>cancelOrderItem</method>
                    </inventory>
                </observers>
            </sales_order_item_cancel>
```

####  Mage_CatalogInventory_Model_Observer类的refundOrderInventory方法还item库存：
``` php app/code/core/Mage/CatalogInventory/Model/Observer.php
/**
     * Return creditmemo items qty to stock
     *
     * @param Varien_Event_Observer $observer
     */
    public function refundOrderInventory($observer)
    {
        /* @var $creditmemo Mage_Sales_Model_Order_Creditmemo */
        $creditmemo = $observer->getEvent()->getCreditmemo();
        $items = array();
        foreach ($creditmemo->getAllItems() as $item) {
            /* @var $item Mage_Sales_Model_Order_Creditmemo_Item */
            $return = false;
            if ($item->hasBackToStock()) {
                if ($item->getBackToStock() && $item->getQty()) {
                    $return = true;
                }
            } elseif (Mage::helper('cataloginventory')->isAutoReturnEnabled()) {
                $return = true;
            }
            if ($return) {
                $parentOrderId = $item->getOrderItem()->getParentItemId();
                /* @var $parentItem Mage_Sales_Model_Order_Creditmemo_Item */
                $parentItem = $parentOrderId ? $creditmemo->getItemByOrderId($parentOrderId) : false;
                $qty = $parentItem ? ($parentItem->getQty() * $item->getQty()) : $item->getQty();
                if (isset($items[$item->getProductId()])) {
                    $items[$item->getProductId()]['qty'] += $qty;
                } else {
                    $items[$item->getProductId()] = array(
                        'qty'  => $qty,
                        'item' => null,
                    );
                }
            }
        }
        Mage::getSingleton('cataloginventory/stock')->revertProductsSale($items);
    }
```

####  Mage_CatalogInventory_Model_Stock类的revertProductsSale方法
``` php app/code/core/Mage/CatalogInventory/Model/Stock.php
public function revertProductsSale($items)
    {
        $qtys = $this->_prepareProductQtys($items);
        $this->_getResource()->correctItemsQty($this, $qtys, '+');
        return $this;
    }
```

#### Mage_CatalogInventory_Model_Resource_Stock类的correctItemsQty方法
``` php app/code/core/Mage/CatalogInventory/Model/Resource/Stock.php
 public function correctItemsQty($stock, $productQtys, $operator = '-')
    {
        if (empty($productQtys)) {
            return $this;
        }

        $adapter = $this->_getWriteAdapter();
        $conditions = array();
        foreach ($productQtys as $productId => $qty) {
            $case = $adapter->quoteInto('?', $productId);
            $result = $adapter->quoteInto("qty{$operator}?", $qty);
            $conditions[$case] = $result;
        }

        $value = $adapter->getCaseSql('product_id', $conditions, 'qty');

        $where = array(
            'product_id IN (?)' => array_keys($productQtys),
            'stock_id = ?'      => $stock->getId()
        );

        $adapter->beginTransaction();//用事物的方法批量修改  cataloginventory_stock_item库存表中的库存数量
        $adapter->update($this->getTable('cataloginventory/stock_item'), array('qty' => $value), $where);
        $adapter->commit();

        return $this;
    }
```

ps:此处还库存有个坑，当并发量高的时候，会出现多次还库存的情况，建议通过redis的方式在此处加锁

###     监控order_cancel_after事件

无，默认代码不会触发任何事件，可以自定义事件

比如订单取消后记录日志等



最后，珍爱生命，远离magento


