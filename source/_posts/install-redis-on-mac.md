---
title: mac下安装redis
date: 2016-06-20 18:12:38
category:
tags: [redis]
toc: true
---


## 一 准备工作
安装了homebrew
安装了php、nginx（或apache）或集成环境

## 二 安装redis服务器
1. 通过homebrew安装

  ```
brew install redis
```

2. 直接下载安装
本人是用这种方法安装的，安装完后才发现可以用homebrew安装

```
curl -O http://redis.googlecode.com/files/redis-2.8.7.tar.gz
sudo tar -zxf redis-2.8.7.tar.gz
mv redis-2.8.7 /usr/local/redis
cd redis
sudo make
sudo make test
sudo make install
mv redis.conf /etc/reds.conf
```
安装成功
## 三 redis服务器的启动、使用和退出
*** 1 启动redis服务*** 
执行以下命令
```
/usr/local/bin/redis-server /etc/redis.conf
```
出现下面的界面说明redis服务器安装成功
![](http://o9xbyqajf.bkt.clouddn.com/images/1469498761643.png)


进入`/usr/local/bin`目录可以看到以下文件
> dump.rdb  用于将缓存以文件的形式存储在硬盘中，需要设置权限，见文末
> redis-cli    用于启动redis客户端

***2 查看redis服务是否启动***
```
ps aux | grep redis
```
***3 使用redis服务***
>注：启动redis服务器后终端所在的窗口就不能输入别的命令了(如下图所示)，需要在终端打开新的窗口才能使用客户端功能
> 
![](http://o9xbyqajf.bkt.clouddn.com/images/1469498796319.png)





通过redis-cli命令可以启动redis客户端

```
redis-cli
```
常用命令
> keys * 查看所有键值
> set (key) (value) 设置键key的值为value
> append (key) (value2) 在键key的值后面加上value2
> get (key) 查看键key的值

redis客户端使用举例：
![](http://o9xbyqajf.bkt.clouddn.com/images/1469498811208.png)


6.23补充：如何设置和查看缓存时间
>set a 123;//设置缓存：a=>123
>EXPIRE a 3600;//设置缓存时间（秒）
>TTL a；//查看缓存剩余时间

6.24补充：如何清空所有缓存
>flushall  //执行该命令后会清空redis服务器的所有缓存，一般用于应急处理，不应该作为常用命令

***4 退出redis服务***
（1）客户端退出
执行
```
redis-cli shutdown
```
（2）关闭pid
先运行
```
ps -u jim(替换成你的用户名) -o pid,rss,command | grep redis-server
```
查看所有redis服务的pid号

![](http://o9xbyqajf.bkt.clouddn.com/images/1469498829072.png)


16.6.24日补充：还可以通过mac自带的活动监视器查看pid
如下图所示
通过Spotlight或alfred搜索`activity monitor`打开活动监视器
在活动监视器中搜索`redis-server`，即可得到pid号
![](http://o9xbyqajf.bkt.clouddn.com/images/1469498837473.png)


补充：如果你的电脑安装了oh my zsh
那么只需要在终端输入
```
kill redis
```
按tab，会自动替换成对应的pid（喜大普奔啊，各位）

再运行
```
kill -9 27355
```
关闭redis服务对应的pid号，即可关闭redis服务
## 四 配置php使用redis服务
1. 安装php的redis扩展
```
  brew install php55-redis --build-from-source
```
`php55`是本机安装的php的版本（5.5）,`--build-from-source`是让安装的扩展与php的版本保持一致

  查看phpinfo()，出现redis选项说明redis配置成功
![](http://o9xbyqajf.bkt.clouddn.com/images/1469498850108.png)

2. 在php代码中使用redis服务

``` php
$redis = new Redis();
$redis->connect('127.0.0.1','host');//redis服务器ip及端口号
$redis->set($key,$value,$timeout);//设置缓存:键-值-缓存时间
$redis->get($key);//查找缓存
$redis->del($key);//删除缓存
$redis->delete($key);//删除缓存
```

##五 常见问题
（1）Redis: Failed opening .rdb for saving: Permission denied
redis服务器会生成`dump.rdb`文件存储缓存，如果文件权限不够则无法读写该文件
```
cd /usr/loal/bin
```
在`/usr/local/bin/`（默认文件目录）下执行命令
```
chmod 777 dump.rdb
```

