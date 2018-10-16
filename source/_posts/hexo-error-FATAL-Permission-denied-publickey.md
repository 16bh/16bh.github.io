---
title: 运行hexo报错解决方案
date: 2016-07-06 12:30:02
categories:
tags: hexo
toc: true
---



记录几个常见的hexo报错



## FATAL Permission denied (publickey)

其实这是git的错误，与hexo木有关系

原因：未配置git


解决方式：

先运行

``` shell
npm install hexo-deployer-git --save
```

再修改`_config.yml`:

``` yml
type: git
  repository: git@name.github.com:name/name.github.io.git
  branch: master
```





## ssh: connect to host github.com port 22: Operation timed out.fatal: Could not read from remote repository.
原因：ssh连接方式失效

解决方式：换成https连接方式

将`_config.yml`中的


``` yml
repository: git@name.github.com:name/name.github.io.git
```
修改为：

``` yml
https://github.com/name/name.github.io.git
```

> name指的是你github账号


## YAMLException: can not read a block mapping entry; a multiline key may not be an implicit key at line 5

```
categories:
tags: hexo
```
文章头部的`categories`和`tags`后面写内容的时候要有空格
