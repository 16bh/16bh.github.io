---
title: '[译]Magento中的12种设计模式'
toc: true
comment: true
date: 2017-03-30 17:18:15
categories: [php]
tags: [magento,设计模式]
---


发现一篇介绍magento的设计模式的英文文章，有空的时候翻译了一下

> 原文地址:
> http://magenticians.com/12-design-patterns-magento

<!--more-->

Magento中的架构通常被认为是过度设计了。如果从架构的角度去看Magento的代码，很容易发现它至少使用了下面介绍的的十二种设计模式。
>Magento its architecture is sometimes deemed overly engineered. If we look at it from a helicopter view, commonly used design patterns are easily spotted. Here are 12 of them.

## 介绍
给出一个需求，解决的方案有很多，设计模式便是其中的最佳方法，可以解决特定环境下的同类问题。设计模式的代码是可重复利用的，对于提高工作效率大有裨益，那从长远角度考虑，是不是应当在代码中尽可能多的使用设计模式呢？明显不是，一名优秀的软件开发者知道何时使用设计模式，并不会无的放矢。早期Magento框架中的比较出色的一点是，其中的绝大部分（甚至所有）使用的设计模式的方式都有其用意所在（画外音：说明Magento的开发者是一名优秀的软件开发者，不然本文也就没有意义了）。

本文是根据@Ryan Street的系列博文整理而得的。

>Introduction
>
A software design pattern is a reusable solution to an often occurring problem. This doesn’t mean that software is better if it has more design patterns. Instead, a good software engineer should be able to spot the problem and implement the pattern instead of introducing implementations without purpose. The earlier behavior is leadingly noticeable in Magento, where most if not all design pattern-implementations have a purpose.
This is a compilation of an article-series which originally appeared on Ryan Street’s blog (@ryanstreet).

## 模式1：MVC
简易程度：
使用场景：

Model-View-Controller,即模型-视图-控制器,简称MVC，应该是最广为人知的一种设计模式（大多数使用者甚至都不会将它视为设计模式）。

这是一种将业务逻辑、页面展示、逻辑分离开来的设计模式。Mageno中使用了大量的xml文件作为逻辑模板，使用pthml（混合了HTML和PHP）文件作为它的视图，剩下的模型依赖Varien的ORM。大多数的业务逻辑发生在模型中，而控制器将模型数据映射到视图，Magento的视图包含了太多的逻辑而显示很笨重，不得不通过一个专门的php类（Block类）进行渲染。
>Model View Controller Pattern
>
Model View Controller, MVC for short, is a design pattern where business, presentation and coupling logic are separated. Magento heavily utilizes XML as templating-logic and HTML mixed with PHP files for its views. Models are backed by ORM. Most business logic happens in the models whereas the controllers map the model-data to the views.
Because Magento its views are “fat” – they often contain a lot of logic – its not rare that views have an additional PHP class (the Block system) which will help with rendering

## 模式2： 前端控制器模式
简易程度：
使用场景：

前端控制器模式确保有且只有一个入口。所有的请求都会先从前端控制器那里走一遭，被识别后路由分发到指定的controller，进行特定的处理。
在Magento唯一一个入口文件`index.php`就起到了前端控制器的作用，它通过`Mage::app()`方法实现应用环境的初始化并将请求路由到正确的controller中。
>Front Controller Pattern
>
The front controller pattern makes sure that there is one and only one point of entry. All requests are investigated, routed to the designated controller and then processed accordingly to the specification. The front controller is responsible of initializing the environment and routing requests to designated controllers.
Magento has only one point of entry (index.php) which will initialize the application environment (Mage::app()) and route the request to the correct controller.

## 模式3：工厂模式
简易程度：
使用场景：
工厂模式的“工厂”二字已经充分表露了它的功能————如工厂的流水线一般统一进行类的实例化。

它被广泛应用在Magento的代码库中，负责自动加载系统。在`config.xml`文件中定义一个`module`的别名后，工厂就悄咪咪的记录了别名对应的类及类所在的位置。

`Mage`核心类中有很多辅助实现工厂的方法，其中的`Mage::getModel()`方法可以接收一个类的别名返回类的实例，如`Mage::getModel('catalog/product')`返回产品类`Mage_Catalog_Model_Product`的实例。

区别于传统的在代码中直接引入类所在文件并调用类，工厂模式以统一的方式对类进行初始化。

>  Factory Pattern
>
As implied by the name, the factory pattern is responsible of factorizing (instantiating) classes. It’s widely used through the Magento code base and leverages the autoloading system in Magento. By defining an alias in a module its config.xml you are letting the factory know where it can find classes.
There are various factory-helper methods in the Mage core class and one of them is getModel(). It accepts an alias for a class and will then return an instance of it. Instead of having include calls scattered through the code base, the factory pattern will instantiate classes in an uniform way.

## 模式4：单例模式
简易程度：
使用场景：

另一种获取类的实例的方法是`Mage::getSingleton()`，它跟`Mage::getModel()`方法一样接收一个类的别名，不同之处在于`getSingleton `在返回实例之前，会先去注册表里瞄一眼，看看这个类是否已经实例化过了，如果实例化过了，那这个实例就可以被共享了。

例如，Magento中的session对象，（如customer session或checkout session）,被储存在注册表中，可以在代码不同地方重复使用，而不要每次都重新创建
>Singleton Pattern
>
Another way to retrieve an instance of a class, is to call Mage::getSingleton(). It accepts a class alias and before returning an instance, it checks the internal registry whether this class has already been instantiated before – this results in a shared instance. An example of where this is mandatory, is the session storage which should be shared through the code base instead of creating it anew every time.

## 模式5：注册模式
简易程度：
使用场景：
（进程级别的）

所有的单例都存储在内部注册表中,这是全局的存储数据的地方,而且不仅限于内部使用。下面列举的注册相关的方法可以分别实现从注册表中存储，查询，删除数据。

``` php
Mage::register($key,$value)     //存储
Mage::registry()    //查询
Mage::unregister()  //删除
```

这种注册表的方法通常应用于数据不能传递时的场景下，进行数据的传输。并且数据格式是`key-value`的格式

比如订单生成的时候`register`一个key，然后在`sales_order_save_after`事件的`observer`方法中通过`registry`读取之前`register`的key

>Registry Pattern
>
All the singletons are stored in the internal registry: a global scoped Container for storing data. It is not only for internal use. The Mage::register($key, $value),::registry($key) and ::unregister($key) methods can be respectively used for storing, retrieving and removing data from the registry. The registry is often used for transferring data between scopes when they cannot be passed on, otherwise.

## 模式6：原型模式
简易程度：
使用场景：

原型模式是对工厂模式功能的补充,它定义类的实例可以根据其父类（原型）检索其它类的实例。

举个栗子，`Mage_Catalog_Model_Product`类有一个`getTypeInstance`方法来获取特定的类`Mage_Catalog_Model_Product_Type`的对象，后者包含了不适用于其它产品的一系列的方法和属性。
而`Mage_Downloadable_Model_Product_Type`这个Downloadable产品的类又最终继承了`Mage_Catalog_Model_Product_Type`类。如果您正在下单并想要调用Downloadable类型产品的特定方法，则需要首先使用原始的产品类的getTypeInstance方法对其进行实例化。

>Prototype Pattern
>
Where the factory pattern (#3 on our list) stops, is where the prototype pattern continues. It defines that instances of classes can retrieve a specific other class instance depending on its parent class (the prototype). A notable example is the Mage_Catalog_Model_Product class which has a getTypeInstance method to retrieve the specificMage_Catalog_Model_Product_Type with a specific subset of methods and properties not applicable to all products.
For example, the Mage_Downloadable_Model_Product_Type ultimately extends the Mage_Catalog_Model_Product_Type. If you are iterating over an order and want to call a specific method of a downloadable product, you will need to factorize it first with the getTypeInstance method of the original product.

## 模式7：对象池模式
简易程度：
使用场景：
对象池模式只是一个包含对象的集合，防止它们一次又一次被分配和销毁。

在Magento中，对象池模式并不常见，只会在处理严重影响服务器性能的重任务时被使用，例如批量导入产品的时候。

可以使用`Mage::objects（）`方法访问对象池（由`Varien_Object_Cache`类管理）

>Object Pool Pattern
>
The object pool pattern is simply a box with objects so that they do not have to be allocated and destroyed over and over again. It’s not used a lot in Magento other than for heavy tasks where resources can get limited soon, like importing products. The object pool (managed by Varien_Object_Cache) can be accessed with Mage::objects().

## 模式8 迭代器模式
简易程度：
使用场景：
迭代器模式定义了一个公共方法来遍历具有对象的结合。

在Magento中，这是由`Varien_Data_Collection`类实现的，它依次使用各种baked-in的PHP类（如`ArrayIterator`）来为数组提供更多的OO接口。这样可以确保模型集合始终具有一个通用的API来遍历，而不依赖于实际的模型。
>Iterator Pattern
>
The iterator pattern defines that there is a shared way to iterate over a container with objects. In Magento, this is handled by the Varien_Data_Collection which on its turn uses various baked-in PHP classes (like ArrayIterator) for having a more OO-interface to arrays. This ensures that model-collections will always have a common API to iterate over without being dependent of the actual models.

## 模式9：延迟加载模式
简易程度：
使用场景：

延迟加载确保加载数据被延迟到实际需要的时间点,这导致更少的资源利用。 Magento的延迟加载行为之一就是collection集合。如果使用`Mage::getModel（'catalog/product')->getCollection()`获取产品collection时，并没有操作数据库。只有当load之后，遍历collection中的product对象或者查询collection的数量时，才会对数据库进行读写操作。
>Lazy Loading Pattern
>
Lazy loading ensures that loading data is delayed until the point when it is actually needed. This results in less resources being used. One of the lazy loading behaviors of Magento is that of collections. If you were to retrieve a collection of products with Mage::getModel('catalog/product')->getCollection(), the database will only be touched when you actually access the collection by, for example, iterating over it or retrieving the count of models found.


## 模式10：服务定位器模式
简易程度：
使用场景：

服务定位器模式抽取某个服务的检索。它遵守其抽象基础，可以在不破坏任何东西的情况下改变服务，而且可以看到适合其目的的服务。
例如，Ryan的数据库连接。

另一个例子是Magento的缓存机制，通过`Mage::getCache()`存储缓存，`Mage::getCache()`是由Zend或其他供应商提供的缓存存储的代理服务定位器。

再如，队列的实现

>Service Locator Pattern
>
The service locator pattern abstracts away the retrieval of a certain service. This allows for changing the service without breaking anything (as it adheres to its abstract foundation) but also fetching the service as seen fit for its purpose.
Ryan exemplifies this with database connections. Another example is that of Magento its caching mechanism where Mage::getCache() is a service locator by-proxy for the cache storage supplied by Zend or other vendors.

## 模式11：模块模式
简易程度：
使用场景：

任何熟悉Magento开发的人都会很自然的接触模块模式。它基本上定义了不同的功能被分组成独立的模块，它们彼此独立，并且可以根据需要插入到Magento主系统中。在理想情况下，模块模式的实现将确保每个元素都可以被删除或交换。 PHP中模块模式的主角之一是Composer软件包管理器。
虽然Magento严重依赖于模块化架构，但它并不是模块化的。某些功能与核心密切相关，不能轻易改变。还大量使用超全局的`Mage`核心类，引入了各种不受监管的系统级依赖关系。
>Module Pattern
>
Anyone familiar with Magento development has stumbled upon the module pattern. It basically defines that different domains are grouped into separate modules which function independent of each other and can be plugged-in to the main system as deemed appropriate. In an ideal situation, an implementation of the module pattern would make sure that each element can be removed or swapped. One of the protagonists of the module pattern in PHP is the Composer package manager.
Though Magento heavily relies on a modular architecture, its not modular to the bone. Certain functionality is heavily tied to the core and can not be easily changed. There is also the heavy usage of the super-global Mage core-class which introduces all sorts of system-wide dependencies not easily overseen.

## 模式12：观察者模式
简易程度：
使用场景：

Magento的事件驱动架构是实现观察者模式的结果。通过定义观察者（或监听者），可以挂接额外的代码，随着观察到的事件触发，这些代码将被调用。

Magento使用`config.xml`存储并定义观察者。使用`Mage::dispatchEvent（$eventName，$data）`触发事件，eventName是事件名，data是参数。事件触发后会将查询数据存储，并触发相应的`$event`观察者。
除了使用模块之外，还可以使用事件来定制现有的逻辑，而不用接触现有的代码。

举个栗子，下单完成后发送邮件通知用户，不需要将写邮件的代码跟下单的代码写在一起，只要下单完成后触发事件`sales_order_save_after`,在`config.xml`中定义`sales_order_save_after`事件的观察者，然后在观察者方法中写相应的发送邮件的代码

>Observer Pattern
>
Magento its event-driven architecture is a result of an implementation of the observer pattern. By defining observers (or listeners), extra code can be hooked which will be called upon as the observed event fires. Magento uses its XML-data storage to define observers. If an event is fired with Mage::dispatchEvent($eventName, $data), the data storage will be consulted and the appropriate observers for $event will be fired.
In addition to using modules, events can be used to customize existing logic without touching the existing code.
