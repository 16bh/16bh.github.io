---
title: 运行hexo报错解决方案
date: 2016-07-06 12:30:02
catogory: Hexo
tags: hexo
toc: true
---

（1）FATAL Permission denied (publickey)

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

 (2)  ssh: connect to host github.com port 22: Operation timed out
fatal: Could not read from remote repository.

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