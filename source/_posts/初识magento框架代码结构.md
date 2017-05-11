---
title: 初识magento框架代码结构
date: 2016-06-30 18:24:32
category: Magento
tags: magento
---

安装好magento之后，用IDE打开所在文件夹，会看到如下所在的代码结构：

```
/app     –程序根目录
/app/etc –全局配置文件目录
/app/code –所有模块安装其模型和控制器的目录
/app/code/core –核心代码或经过认证得模块，如果要升级不要这里的代码
/app/code/community –社区版的模块目录
/app/code/local –定制代码目录
/app/code/core/Mage –magento默认命名空间
/app/code/core/Mage/{Module} –模块根目录
/app/code/core/Mage/{Module}/etc –模块的配置文件目录
/app/code/core/Mage/{Module}/controllers –模块的控制器
/app/code/core/Mage/{Module}/Block –显示块的逻辑类
/app/code/core/Mage/{Module}/Model –模块的对象模型
/app/code/core/Mage/{Module}/Model/Mysql4 –模块的资源模型
/app/code/core/Mage/{Module}/sql –模块各个版本的安装和升级用sql 
/app/code/core/Mage/{Module}/sql/{resource}/ - 升级是需要的资源模型
/app/code/core/Mage/{Module}/sql/{resource}/{type}-{action}-{versions}.(sql|php) –资源升级文件例如: mysql4-upgrade-0.6.23-0.6.25.sql 
/app/design –设计包目录(layouts, templates, translations) 
/app/design/frontend –前端的设计
/app/design/adminhtml –后台管理设计
/app/design/{area}/{package}/{theme} –定制的主题
/app/design/{area}/{package}/{theme}/layout –定义显示块的 .xml 文件
/app/design/{area}/{package}/{theme}/template – .phtml (html with php tags)模版
/app/design/{area}/{package}/{theme}/locale –Zend_Translate 兼容的主题用的文字翻译
/app/locale –本地化文件
/app/locale/{locale (en_US)} –Zend_Translate 兼容的模块用的文字翻译
/skin/{area}/{package}/{theme}/- css和图像
/lib –公用库
/js – javascripts 
/media –上传文件存放目录
/tests –测试目录
/var –临时文件目录
```


说明：
1. `app/code`目录下分为三部分：`core`、`community`、`local`

 - `core`里的是核心模块，修改了这部分的话magento就没法升级了
 - `commutiy`里的是社区模块，就是别人开发的，有免费的也有收费的
 - ***`local`***里的是我们自己开发的模块，在新建模块之前先建立一个名字空间，一般是公司的名称，如tecent，然后就可以在`app/code/local/tecent/`目录下新建模块了，如何新建模块，参考[]()

2. `media`和`var`文件需要有写入的权限，在安装`magento`的时候如果这两个文件权限不够的话会报错，需要`chmod 777 `修改文件夹的权限