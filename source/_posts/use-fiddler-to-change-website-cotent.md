---
title: 通过Fiddler工具进行接口代理-改变线上网页的显示结果
toc: false
category:
date: 2016-01-18 22:16:53
tags: [php,tools]
---


>Fiddler是抓取请求的工具的一种，类似的还有Charles等，使用Fidder之前应先关闭其他的代理工具

>需求如下：

>网站前端和服务端配合开发了一个页面，会调取接口A的数据并在页面上呈现，现在由于业务要求需要开发新的接口B，在原有的前端逻辑下正常展示。那么，在开发的过程中，在没有前端配合的情况下，服务端如何让这个页面调取B的接口并呈现呢？

解决方案是这样：

以去哪儿的某款产品为例：http://szgq1.package.qunar.com/user/id=187688454&abt=a#tf=tejiaqunar

用chrome打开该链接，打开开发者工具，依次选择`Network -XHR`可以看到页面调用的服务端的接口列表

<!--more-->

<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901134036.png" width="513"/>

以`getBottomRecommend`接口为例，

<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901156887.png" width="162"/>

右击该接口地址并在新的页面中打开，会显示该接口的出入参。

接口的请求地址：`http://szgq1.package.qunar.com/user/recommend/getBottomRecommend.json?pId=187688454`

入参是产品id`pId=187688454`

出参是推荐的产品的list数组：
<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901371905.png" width="938"/>


出参的显示结果如下图所示：
<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901384409.png" width="387"/>
假设，我们本地开发了一个新的产品推荐接口，接口地址为`user/recommend/newGetBottomRecommend.json`

在网站前端修改接口地址并上线之前（有时候，情况更加复杂，我们进行的app服务端的开发，为app的某个页面提供接口，在app修改接口地址并打包给我们之前，我们只能通过观察数据的结构来想象展示的效果，而一般情况下pc或M站上是有这样的页面提供给我们测试使用的），我们本地开发的时候需要在原有的界面显示新接口返回的数据

 

打开`Fiddler`软件，刷新刚才的产品详情页，此时在fiddler窗口中会抓取所有的请求

<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901413278.png" width="510"/>
A区域中显示了页面在刷新后发起的所有的请求，我们在其中找到我们要修改的请求

1、在右侧的区域里选择AutoResponder添加代理

2、勾选这三项

3、Add rule添加代理

4、在4中输入原有的接口地址　　http://szgq1.package.qunar.com/user/recommend/getBottomRecommend.json?pId=187688454

5、在5中输入现在代理的接口地址，我们先选择自带的404_Plain.dat试一试，理论上调用这一接口会报404错误（查找不到文件）

6、保存操作，刷新接口请求发现接口返回值是
<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901456863.png" width="453"/>


此时，页面中产品推荐模块的展示结果为：

<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901448188.png" width="401"/>

可见，此时，该模块对应的线上接口调的是我们代理的404的新接口。

7、我们也可以用json文件来代替接口的请求，比如我们将原有的json文件复制下来，进行修改

``` json
{"ret":true,"data":{"group":[{"min_price":0,"count":1024,"short_arr":"我家+","arr":"日本,大阪,京都","departure":"博客园","takeoff_date":"今天","url":"/search/group-a-a-%E4%B8%8A%E6%B5%B7-----%E6%97%A5%E6%9C%AC-4812----20160127-10758"}]}}
```

保存为`newReturn.json`,并在新接口请求的位置选择这个文件

<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901518516.png" width="329"/>

此时，接口的请求结果为我们输入的内容：
<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901532561.png" width="806"/>
页面的显示结果为：
<img src="http://o9xbyqajf.bkt.clouddn.com/images/1467901544378.png" width="385"/>

