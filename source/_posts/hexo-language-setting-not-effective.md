---
title: hexo语言设置未生效解决办法
categories: Blog
toc: false
comment: true
date: 2017-03-30 19:11:45
tags: hexo
---



![20170330149087276742023.png](hexo-language-setting-not-effective/20170330149087276742023.png)

修改了hexo的language没有生效，可能是你没有执行`hexo clean`！

<!--more-->

在Hexo的`站点配置文件`中设置如下
```
language: zh-Hans
```

如下图所示
网站中显示如下，很明显不是简体中文

![20170330149087244657592.png](hexo-language-setting-not-effective/20170330149087244657592.png)

解决方法：

1. 先将language设置为空
2. 执行`hexo g`
3. 执行`hexo clean`
4. 将language设置为想要的语言
5. 执行`hexo g`


执行上述操作后如下：

![20170330149087302021084.png](hexo-language-setting-not-effective/20170330149087302021084.png)


>注：
其他语言代码如下：
![20170330149087240941015.png](hexo-language-setting-not-effective/20170330149087240941015.png)
