---
title: yaf学习笔记 - MVC模式
categories:
tags: [php,yaf]
toc: false
comment: true
date: 2017-06-12 18:59:00
---






当我们访问demo项目的时候，在页面上展示了`Hello World! I am Stranger`，其实是通过MVC模式实现的


运行流程如下图所示（摘自鸟哥文档）：


<img src="http://o9xbyqajf.bkt.clouddn.com/20170613149732111245337.png" width="492" height="297"/>
Yaf运行流程(摘自鸟哥文档)

<!--more-->


当我们访问`yaf.com`网站的时候，先走到入口文件`index.php`，然后经过`bootstrap`初始化，`router`路由，因为没有指定controller，会使用默认控制器IndexController的默认方法IndexAction，即下面的几种访问方式都是可以的：

```
yaf.com
yaf.com/index
yaf.com/index/index
yaf.com/index/index/index
```
最后一种访问方式里：第一个index是Module模块名，第二个index是Controller控制器名，第三个index是Action方法名

> 模块的用法见下一节

访问结果如下：

![20170613149732160779459.png](http://o9xbyqajf.bkt.clouddn.com/20170613149732160779459.png)

IndexController的indexAction的代码如下：

``` php ~/test/application/controllers/Index.php
	public function indexAction($name = "Stranger") {
		//1. fetch query
		$get = $this->getRequest()->getQuery("get", "default value");

		//2. fetch model
		$model = new SampleModel();

		//3. assign
		$this->getView()->assign("content", $model->selectSample());
		$this->getView()->assign("name", $name);

		//4. render by Yaf, 如果这里返回FALSE, Yaf将不会调用自动视图引擎Render模板
    return TRUE;
	}
```

注意：

* $name默认值是Stranger，我们可以通过下面的方式指定$name的值

```
yaf.com/index/index/index/name/jimxu
```

![2017061314973219814429.png](http://o9xbyqajf.bkt.clouddn.com/2017061314973219814429.png)

* 申明SampleModel类的一个对象，通过selectSample方法获取$content的值

``` php ~/test/application/models/Sample.php
 public function selectSample() {
        return 'Hello World!';
    }
```

* 将`$name`和`$content`传到view

```
$this->getView()->assign("content", $model->selectSample());
$this->getView()->assign("name", $name);
```

* 在view对应的phtml中可以使用`$name`和`$content`变量的值

``` php ~/test/application/views/index/index.phtml
echo $content, " I am ", $name;
```


* 通过MVC设计模式，以控制器为中介，在模型文件中进行复杂的业务逻辑处理，在视图文件中渲染效果，实现了模型和视图的低耦合
