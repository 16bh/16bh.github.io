---
title: magento中查看某一段代码生成的sql
toc: false
date: 2016-10-27 16:25:49
categories:
tags: magento
---




查看一段代码运行期间执行的sql语句
便于查看sql性能


<!--more-->

使用magento自带的读写适配器操纵数据库的时候，会调用`lib/Zend/Db/Adapter/Abstract.php`文件中的`query`方法,在`query`方法中将sql语句记入日志
	
```
public function query($sql, $bind = array())
{
Mage::log($sql,null,'jim.log');//记日志

}
```
同时，在待测试的代码前后都加上标记，同样记入日志中

```
public function test()
{
    Mage::log('----------test sql start--------------',null,'jim.log');
    $a = Mage::helper('test')->testSql(); //待测试代码
    Mage::log('----------test sql end--------------',null,'jim.log');
}
```

最后运行程序后，打开日志文件`jim.log`查看`test sql start`和`test sql end`之间的sql语句，即为测试代码执行的sql语句

