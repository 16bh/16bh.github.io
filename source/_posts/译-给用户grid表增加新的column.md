---
title: '[译]给用户grid表增加新的column'
toc: true
date: 2016-08-29 16:19:31
categories: Magento
tags: magento
---


> 来源：http://magento.stackexchange.com/questions/5973/adding-columns-to-customer-grid-using-observer-or-overriding-the-customer-grid



<!--more-->

为了给用户grid新增一个column，需要重写block：`Mage_Adminhtml_Block_Customer_Grid`，并覆写block里的两个方法：
	- _prepareCollection：添加你的属性到collection中
	- _prepareColumns：添加column到grid中	
# 新建模块并配置

先新建一个模块`Easylife_Customer`,修改	
``` xml app/etc/module/Easylife_Customer.xml
<?xml version="1.0"?>
<config>
    <modules>
        <Easylife_Customer>
            <active>true</active>
            <codePool>local</codePool>
            <depends>
                <Mage_Customer /><!-- 添加的模块依赖该核心模块 -->
                <Mage_Adminhtml /><!-- 添加的模块依赖该核心模块 -->
            </depends>
        </Easylife_Customer>
    </modules>
</config>
	```
	
# 修改配置文件

``` xml app/code/local/Easylife/Customer/etc/config.xml
<?xml version="1.0"?>
<config>
    <modules>
        <Easylife_Customer>
            <version>0.0.1</version>
        </Easylife_Customer>
    </modules>
    <global>
        <blocks>
            <adminhtml>
                <rewrite>
                    <customer_grid>Easylife_Customer_Block_Adminhtml_Customer_Grid</customer_grid><!-- 用我们自己建立的Easylife_Customer_Block_Adminhtml_Customer_Grid覆写原有的用户block -->
                </rewrite>
            </adminhtml>
        </blocks>
    </global>
</config>
```


# 编辑block文件

``` php app/code/local/Easylife/Customer/Block/Adminhtml/Customer/Grid.php
<?php
class Easylife_Customer_Block_Adminhtml_Customer_Grid extends Mage_Adminhtml_Block_Customer_Grid{
    /**
     * 覆写_prepareCollection方法新增一个属性到collection中
     * @return $this
     */
    protected function _prepareCollection(){
        $collection = Mage::getResourceModel('customer/customer_collection')
            ->addNameToSelect()
            ->addAttributeToSelect('email')
            ->addAttributeToSelect('created_at')
            ->addAttributeToSelect('group_id')
            //如果你要添加的属性是用户自身的属性，那么用下面的语句
            ->addAttributeToSelect('mobile')
            //如果你要添加的属性是用户地址表中的，参考下面的语句
            //->joinAttribute('mobile', 'customer_address/mobile', 'default_billing', null, 'left')
            ->joinAttribute('billing_postcode', 'customer_address/postcode', 'default_billing', null, 'left')
            ->joinAttribute('billing_city', 'customer_address/city', 'default_billing', null, 'left')
            ->joinAttribute('billing_telephone', 'customer_address/telephone', 'default_billing', null, 'left')
            ->joinAttribute('billing_region', 'customer_address/region', 'default_billing', null, 'left')
            ->joinAttribute('billing_country_id', 'customer_address/country_id', 'default_billing', null, 'left');

        $this->setCollection($collection);
        //下面是替换了原有的parent::_prepareCollection的代码，原有的代码是调用了Mage_Adminhtml_Block_Customer_Grid的父类即Mage_Adminhtml_Block_Widget_Grid中的代码        
        //直接调用 parent::_prepareCollection 会使得上面的代码失效。
        //而你又不能用这种语法来调用父类的父类的方法 parent::parent::_prepareCollection()，所以就只能将代码整个copy到此处
        if ($this->getCollection()) {

            $this->_preparePage();

            $columnId = $this->getParam($this->getVarNameSort(), $this->_defaultSort);
            $dir      = $this->getParam($this->getVarNameDir(), $this->_defaultDir);
            $filter   = $this->getParam($this->getVarNameFilter(), null);

            if (is_null($filter)) {
                $filter = $this->_defaultFilter;
            }

            if (is_string($filter)) {
                $data = $this->helper('adminhtml')->prepareFilterString($filter);
                $this->_setFilterValues($data);
            }
            else if ($filter && is_array($filter)) {
                $this->_setFilterValues($filter);
            }
            else if(0 !== sizeof($this->_defaultFilter)) {
                $this->_setFilterValues($this->_defaultFilter);
            }

            if (isset($this->_columns[$columnId]) && $this->_columns[$columnId]->getIndex()) {
                $dir = (strtolower($dir)=='desc') ? 'desc' : 'asc';
                $this->_columns[$columnId]->setDir($dir);
                $this->_setCollectionOrder($this->_columns[$columnId]);
            }

            if (!$this->_isExport) {
                $this->getCollection()->load();
                $this->_afterLoadCollection();
            }
        }

        return $this;
    }

    /**
     * 覆写_prepareColumns方法在email列后面新增一列    
     * 如果你想要改变新增列的位置，那么直接修改addColumnAfter方法的第三个参数就好了     
     */
    protected function _prepareColumns(){
        $this->addColumnAfter('mobile', array(
            'header'    => Mage::helper('customer')->__('Mobile'),
            'index'     => 'mobile'
        ),'email');
        return parent::_prepareColumns();
    }
}
```


