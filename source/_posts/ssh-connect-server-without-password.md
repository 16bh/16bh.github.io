---
title: ssh连接服务器更简单一点
comment: true
date: 2017-07-07 15:50:02
categories:
tags: [git,ssh]
---








用ssh连接服务器，通常是下面这样的

```
ssh user@127.0.0.1
```
然后按提示输入密码就连上了

其实，可以更简单一点，我们不需要输入用户名，不需要输入服务器ip地址，甚至不需要输入密码！

<!--more-->

## 简化1：不需要输入用户名和host
那么多的服务器，每个服务器登录的用户名和host还不一样 谁记的住呀

直接修改你本地的`.ssh/config`文件（没有就新建一个）

编辑如下：

```
 Host test
      HostName 172.0.0.1
      User user
```
然后就可以用

```
ssh test
```
来连接服务器了，但是还是要输入密码的


## 简化2： 不需要输入密码

先生成秘钥

```
ssh-keygen -t rsa
```

过程中会提示你输入密语，密语可以为空，按确认就好（安全性降低了，但可以避免以后一直询问你密语）

这样在你的`.ssh`目录下就应该生成了下面两个文件

```
id_rsa  私有秘钥(私钥)
id_rsa.pub  公有秘钥(公钥)
```

用`scp`命令将生成的公钥copy到服务器，为了防止文件名重复改个名字

```
scp ~/.ssh/id_rsa.pub user@172.0.0.1:~/.ssh/unique_id_rsa.pub
```
按提示输入密码（以后就不用输了）

最后，登录服务器,进入`~/.ssh`目录

应该能看到下面两个文件

```
authorized_keys 存储了很多公钥的文件
unique_id_rsa.pub 我们刚才copy过来的
```

执行下面的操作

```
//将我们的公钥加入到文件的末尾
cat unique_id_rsa.pub >> authorized_keys
//然后删除无用的公钥
rm unique_id_rsa.pub
```

退出服务器

执行
```
ssh test
```
就可以直连服务器啦

注意一点:

- 生成的一定要是默认的秘钥名（id_rsa），如果生成秘钥的时候你指定了其他的名字如 `id_rsa.different`,那么连接服务器的时候就要用下面的命令

```
ssh -i id_rsa.different test
```

enjoy it



