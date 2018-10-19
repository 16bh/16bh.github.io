---
title: 在php中使用json
date: 2016-06-23 18:14:55
categories: [IT]
tags: [php,json]
toc: true
---



# 关于json
1. 为什么要使用json
json字符串容易存储，尤其是要将一个数组存入数据库或缓存或记录日志的时候

2. json_encode

``` php
$str = json_encode($arr);
```

3. json_decode
在`Dash`中的函数格式如下

```
mixed json_decode ( string $json [, bool $assoc = false [, int $depth = 512 [, int $options = 0 ]]] )
```

注意第二个参数，当`json_decode()`的第二个参数不填的时候，json解析的到的结果是个object对象，只有当第二个参数是true的时候，json解析的结果才是list数组
即

``` php
$object = json_decode($str);
$array = json_decode($str,true);
```

***如果是做API接口开发，经常和客户端联调的筒子们肯定就知道，object类型和list类型对于安卓来说相差甚远，直接关系到接口是否能够解析***


# 关于json工具

1. 在线json解析
（1）Json Parser Online:http://json.parser.online.fr/
  优势：界面简洁美观,json解析框够大，适用于解析很长的json字符串

  ![](how-to-use-json/1240-20181016234745433.png)

  （2） Be Json

  ![](how-to-use-json/1240-20181016234749326.png)
  优势：***json解析出错时会给出错误提示***

2. Chrome的json解析扩展 - `JSONVIEW`
安装完成后调用接口直接在页面上显示json解析后的内容

下载链接：
https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc

效果图：
![](how-to-use-json/1240-20181016234752107.png)
