---
title: sublime搭建js编译环境及自动根据文件后缀选择对应的编译环境
toc: true
date: 2016-07-21 18:50:05
categories: [Editor,sublime]
tags: [sublime,js]
---

开始学习`js`,先在`sublime`上搭建`js`的编译环境

<!--more--> 

# 搭建js编译环境

> 确保你的电脑已经安装了`node.js`

编译环境的搭建同之前搭建`php`的编译环境

菜单栏`Tools` > `Build System` > `New Build System`

在新建的文件中编辑如下内容（删除自动生成的内容）：

```
{
"cmd": ["/usr/local/bin/node", "$file"],
"selector": "source.js"
}
```

保存并命名为`js.sublime-build`，此时`sublime`的所有编译环境列表在`Tools` > `Build System` 中已经有`js`这一项了，选择它即可
![](http://o9xbyqajf.bkt.clouddn.com/images/1469098626551.png)
当你打开`javascript`文件时，按`Command`+`B`就可以编译程序了：
![](http://o9xbyqajf.bkt.clouddn.com/images/1469098738991.png)

# sublime中编译js时执行alert命令报错解决方法

`sublime`中无法执行浏览器的弹窗命令，代码中有`alert`的话会报如下错误：

> eferenceError: alert is not defined

`stackoverflow`提供了[解决方法](http://stackoverflow.com/questions/28999738/simulating-alerts-in-sublime-text),在`sublime`的`js`文件开头加入一下代码:

``` js
if((typeof alert) === 'undefined') {
    global.alert = function(message) {
        console.log(message);
    }
}
```
其实就是用`console.log`命令替换了`alert`命令，将要再弹窗中展示的问题直接打印输出

效果如下：
![](http://o9xbyqajf.bkt.clouddn.com/images/1469158250092.png)


# 让sublime自动选择编译环境

我们可以在`sublime`中对不同的语言搭建不同的编译环境

当搭建了多个编译环境的时候，选择 `Tools` > `Build System` > `Automatic`可以根据文件的后缀名自动选择对应的编译环境。




