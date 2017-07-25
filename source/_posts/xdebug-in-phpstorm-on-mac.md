---
title: mac下phpstorm配置xdebug
toc: true
date: 2016-07-08 14:28:10
categories:
tags: [phpstorm,xdebug]
---

# 给php安装xdebug扩展
安装扩展(前提是你的`php`也是用`brew`安装的)

``` shell
brew install php55-xdebug --build-from-source
```

进入下面的目录打开`xdebug`配置文件：
``` shell
cd /usr/local/etc/php/5.5/conf.d
vim ext-xdebug.ini
```

编辑如下：


``` ini
[xdebug]
zend_extension="/usr/local/opt/php55-xdebug/xdebug.so"

xdebug.remote_enable=on
xdebug.remote_handler=dbgp
xdebug.remote_host=localhost
xdebug.remote_port=9010
xdebug.remote_log=/tmp/xdebug.log
xdebug.profiler_enable=0
xdebug.profiler_output_name=xdebug.cachegrind-out.%s.%p
xdebug.idekey="PHPSTORM"
```

配置完成后要重启`php-fpm`:

<!--more-->

``` shell
sudo php55-fpm restart
```
在`index.php`中加入`phpinfo();die;`并执行
若能在php的配置页面中看到`xdebug`的模块说明配置成功

![](http://o9xbyqajf.bkt.clouddn.com/images/1467959560969.png)


# chrome或firefox浏览器安装扩展
![](http://o9xbyqajf.bkt.clouddn.com/images/1467962586560.png)

安装[xdebug-helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?hl=zh-CN)扩展并开启，直到在浏览器工具栏可以看到激活状态的图标
![](http://o9xbyqajf.bkt.clouddn.com/images/1467962624678.png)

# phpstorm设置
进入`phpstorm`的偏好设置:

（1）`Languages & Frameworks` > `PHP` > `Servers`
![](http://o9xbyqajf.bkt.clouddn.com/images/1467962809444.png)

（2）`Languages & Frameworks` > `PHP` > `Debug` > `DBGp Proxy`

![](http://o9xbyqajf.bkt.clouddn.com/images/1467962870171.png)

 (3) `Languages & Frameworks` > `PHP` > `Debug`
 ![](http://o9xbyqajf.bkt.clouddn.com/images/1467962941842.png)


# xdebug使用

1. 在`chrome`上启用`xdebug-helper`扩展，输入网址或请求的接口地址
2. 在`phpstorm`上开启`xdeubg`监听![](http://o9xbyqajf.bkt.clouddn.com/images/1467963645152.png)

3. 刷新`chrome`,在`phpstorm`中弹出xdebug窗口

4. 单步调试
![20170621149801911655649.png](http://o9xbyqajf.bkt.clouddn.com/20170621149801911655649.png)

5. 跳入，进入调用的方法体
![20170621149801924516403.png](http://o9xbyqajf.bkt.clouddn.com/20170621149801924516403.png)

6. 跳出，离开方法体，返回原来执行的代码
![20170621149801925964706.png](http://o9xbyqajf.bkt.clouddn.com/20170621149801925964706.png)


# 报错
如果报下面的错误，说明端口号错误，确保设置的端口号与之前在`ext-xdebug.ini`中配置的是一致的。如果一致的还出现这种错误，那么换一个端口号试试

![](http://o9xbyqajf.bkt.clouddn.com/images/1467960299385.png)
