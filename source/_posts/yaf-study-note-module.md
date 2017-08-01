---
title: yaf学习笔记 - 模块
categories: 
tags: [php,yaf]
toc: false
comment: true
date: 2017-06-13 10:12:59
---









## 模块是什么？

设计模式的一条准则是“高内聚，低耦合”。
模块是高内聚的一种实现手段


## 建立模块

当我们访问application/controllers/IndexController的时候，相当于访问了默认的Index模块，这是由配置决定的

``` ini application.ini
application.dispatcher.defaultModule = Index
```

我们要实现一个博客网站，文章可以作为一个模块
在application目录下新建modules目录，建立Post文件夹，在Post下面依次建立models,views,controllers,在Post/controllers下建立List.php文件，内容如下：

``` php
<?php
    class ListController extends Yaf_Controller_Abstract
    {
        public function viewAction()
        {
              
        }
    }
```

<!--more-->

Post/views下面建立list文件夹，新建view.phtml文件

```
<?php
echo 2333;
```
Post模块的结构如下所示：
![20170613149732391375464.png](http://o9xbyqajf.bkt.clouddn.com/20170613149732391375464.png)

## 模块的配置

这时候我们访问

```
yaf.com/post/list/view
```
看到下面的报错信息：
![20170613149732400095678.png](http://o9xbyqajf.bkt.clouddn.com/20170613149732400095678.png)

报错的原因是因为我们没有将新建的模块加到配置文件中
编辑conf/application.ini文件，将下面两句代码加入common分组下面

```
application.modules = "Index,Post"	//模块
application.dispatcher.defaultModule = Index	//默认模块
```

再次访问，就可以了
![20170613149732414586476.png](http://o9xbyqajf.bkt.clouddn.com/20170613149732414586476.png)