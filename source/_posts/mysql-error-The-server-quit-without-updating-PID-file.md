---
title: '[mysql error]The server quit without updating PID file '
categories:
tags: [mysql,error]
toc: false
comment: true
date: 2017-04-12 19:06:00
---



mysql是通过homebrew安装的,重启电脑后启动mysql报错


<!--more-->

update: 2017年7月11日17:42

终极解决方案：
用brew安装mysql经常会碰到这些问题，直接用安装包安装后，从未复现


debug前须知：
mysql配置文件依次读取：
```
/etc/my.cnf
/etc/mysql/my.cnf
~/my.cnf
```


![2017041214919952361252.png](http://o9xbyqajf.bkt.clouddn.com/2017041214919952361252.png)

网上提供的解决方法：

## 查看报错信息，有两处报错
err文件位于`/usr/local/var/mysql/data`
![20170412149199540435226.png](http://o9xbyqajf.bkt.clouddn.com/20170412149199540435226.png)

    - Can't open the mysql.plugin table. Please run mysql_upgrade to create it.
    按照提示运行`mysql_upgrade`报错
    ![20170412149199546335602.png](http://o9xbyqajf.bkt.clouddn.com/20170412149199546335602.png)
    >mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
    
    - Fatal error: Can't open and lock privilege tables: Table 'mysql.user' doesn't exist

## 检查是否有实例正在运行
```
ps -ef | grep mysql
```
![20170412149199567567857.png](http://o9xbyqajf.bkt.clouddn.com/20170412149199567567857.png)
结果：没有

## 删除.err文件
![20170412149199529841695.png](http://o9xbyqajf.bkt.clouddn.com/20170412149199529841695.png)
结果：无效

## 改变权限
```
sudo chown -R _mysql:mysql /usr/local/var/mysql
```
结果：无效

## 重新初始化
```
unset TMPDIR
mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql/data --tmpdir=/tmp
```
![20170412149199560432948.png](http://o9xbyqajf.bkt.clouddn.com/20170412149199560432948.png)

因为/usr/local/var/mysql/data目录不为空，所以没法初始化，那么先清空目录，再初始化

```
unset TMPDIR
cd /usr/local/var/mysql/data
sudo rm *
mysql_install_db
```
再运行`sudo mysql.server start`命令启动，依然报错，查看目录文件权限，原来初始化的时候又改变权限了

```
sudo chown -R _mysql:mysql /usr/local/var/mysql
```
![2017041214919969007399.png](http://o9xbyqajf.bkt.clouddn.com/2017041214919969007399.png)

DONE！

 brew services start mysql与mysql.server start

2017-04-12T12:00:55.701485Z 1 [Note] A temporary password is generated for root@localhost: ZCBp1r-K0RlE

If you lose this password, please consult the section How to Reset the Root Password in the MySQL reference manual.