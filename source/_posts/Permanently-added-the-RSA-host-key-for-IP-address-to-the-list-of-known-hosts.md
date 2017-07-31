---
title: Permanently added the RSA host key for IP address to the list of known hosts
toc: true
comment: true
date: 2017-07-26 18:27:02
categories:
tags: [hexo,git,ssh,error]
---

<img src="http://o9xbyqajf.bkt.clouddn.com/20170726150106524593664.png" width="492" height="297"/>

将Hexo项目托管到Coding.net后，使用`hexo g -d`提交代码后报下面的Warning

> Permanently added the RSA host key for IP address '123.59.85.105' to the list of known hosts.


<!--more-->

`123.59.85.105`为域名`coding.net`的ip地址

猜测可能的原因是hexo命令deploy时不会检查`~/.ssh/known_hosts`文件

编辑config文件 `~/.ssh/config`:


```
Host coding.net
      HostName 123.59.85.105
      IdentityFile {path_to_private_key}
      User {user_name}
```

此时提交就没有warning了