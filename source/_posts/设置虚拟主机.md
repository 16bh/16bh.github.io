---
title: mac下nginx服务器设置虚拟主机
toc: true
date: 2016-07-07 12:48:38
category: [IT,php]
tags: [php,nginx]
---

>搭建好了php的开发环境之后,用`localhost`就可以访问`nginx`或`apache`的文件根目录了,如果想用域名来访问的话，就需要设置虚拟主机了

# 前提
 已经搭建了`nginx+mysql+php+php-fpm`的开发环境

# 编辑hosts
mac电脑上`hosts`文件位于`/etc/hosts`
终端打开hosts文件

``` shell
vim /etc/hosts
```

<!--more-->

编辑如下

```
127.0.0.1   localhost
127.0.0.1   myblog.com      //设置你想要用的域名
255.255.255.255 broadcasthost
::1             localhost
```

设置的域名甚至可以是线上已有的域名，如`baidu.com`，不过这样子设置之后就不能访问线上的真实网站了

# 启动nginx端口监听
1. 进入`nginx`目录，如果你使用`homebrew`安装的`nginx`的话，那么目录是`/usr/local/etc/nginx`

``` shell
cd /usr/local/etc/nginx
```

2. 查看配置文件`nginx.conf`
确认最后一行有下面这句，没有的话就手动添加

``` conf
include servers/*;
```

3. 打开`nginx`目录下的文件夹`servers`(如无，手动添加),新建一个`server`,命名为`blog`

``` shell
cd servers
vim blog
```
编辑如下内容：
```
server {
    listen 8080;    //此处修改端口号
    server_name myblog.com; //此处添加hosts中设置的域名
    
    root /Users/jim/blog;    //此处设置项目根目录

    location ~ \.php$ { ## Execute PHP scripts
        expires        off; ## Do not cache dynamic content
        
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params; ## See /etc/nginx/fastcgi_params
    }

    location / {
        index index.html index.php; ## Allow a static html file to be shown first
            try_files $uri $uri/ @handler; ## If missing pass the URI to Magento's front handler
            expires 30d; ## Assume all files are cachable
            if ($request_uri ~* "\.(png|gif|jpg|jpeg|css|js|swf|ico|txt|xml|bmp|pdf|doc|docx|ppt|pptx|zip)$") {
                expires max;
            }

        # set fastcgi settings, not allowed in the "if" block
        include /usr/local/etc/nginx/fastcgi_params;
        fastcgi_split_path_info ^(.+\.php)(/.+)$; #this line
        fastcgi_param SCRIPT_FILENAME $document_root/index.php;
        fastcgi_param SCRIPT_NAME /index.php;
        fastcgi_param  MAGE_RUN_CODE default;
        fastcgi_param  MAGE_RUN_TYPE store;

        # rewrite - if file not found, pass it to the backend
        if (!-f $request_filename) {
            fastcgi_pass 127.0.0.1:9000;
            break;
        }
    }
}
```

然后就可以用你设置的域名和端口号(此处为`jim.practise.com:8080`)来访问你的项目了
若监听的是80端口那么域名后面的端口号可以省略

以后如果要使用别的域名，只需要在`servers`文件夹下面继续新增就可以了

