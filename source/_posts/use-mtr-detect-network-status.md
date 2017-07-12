---
title: 使用mtr工具检测网络w
toc: true
comment: true
date: 2017-07-12 17:21:07
categories:
tags: tools
---



mtr集成了traceroute、ping、nslookup功能


<!--more-->


# 安装mtr

```
brew install mtr
```

# 使用mtr

```
mtr ip/host_name
```

 >mtr -h  #提供帮助命令
 >mtr -v  #显示mtr的版本信息
 >mtr -r  #已报告模式显示
 >mtr -s  #用来指定ping数据包的大小
 >mtr --no-dns  #不对IP地址做域名解析
 >mtr -a  #来设置发送数据包的IP地址 这个对一个主机由多个IP地址是有用的
 >mtr -i  #使用这个参数来设置ICMP返回之间的要求默认是1秒
 >mtr -4  #IPv4
 >mtr -6  #IPv6


# 使用mtr检测域名
 jimxu.me这个域名通过DNSPod分别解析到了16bh.github.io(国外)和jimxu.coding.me(国内)

 对比下托管在国内外的两个Pages服务的网络状态
 ![20170712149986203271598.png](http://o9xbyqajf.bkt.clouddn.com/20170712149986203271598.png)

可见国内网络时托管在coding.net的网站比托管在github的网站有了大幅的提速