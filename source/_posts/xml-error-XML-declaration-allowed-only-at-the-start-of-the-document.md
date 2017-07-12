---
title: 'XML报错:XML declaration allowed only at the start of the document'
toc: false
date: 2016-07-20 11:01:15
categories: 
tags: [xml,error]
---



>错误信息:
>Warning: simplexml_load_string(): Entity: line 1: parser error : XML declaration allowed only at the start of the document


<!--more-->

检查后发现，`xml`文件的头文件开头处出现了多余的空格

```
    <?xml version="1.0"?>
```

修改为：

``` xml
<?xml version="1.0"?>
```

问题解决