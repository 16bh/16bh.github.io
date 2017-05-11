---
title: mac安装go并运行第一个程序
categories: [IT,go]
tags: [go]
toc: false
comment: true
date: 2017-04-11 11:53:15
---

![20170411149188484167726.png](http://o9xbyqajf.bkt.clouddn.com/20170411149188484167726.png)

- homebrew安装go
- 配置环境变量
- 在终端运行go程序


<!--more-->

# 通过homebrew安装go

```
brew update
brew install go
```

# 添加环境变量

```
#编辑~/.zshrc
export GOROOT=/usr/local/opt/go/libexec
export GOPATH=$HOME/.go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```
保存后执行`source ~/.zshrc`


# 在终端环境运行go程序

新建文件`hello.go`，编辑如下并保存
``` go ~/code/go/src/hello.go
// hello.go
package main
import "fmt"

func main() {
  fmt.Printf("Hello, world!")
}
```

在终端执行
```
cd ~/code/go/src/hello.go
go run hello.go
```
![20170411149188473495637.png](http://o9xbyqajf.bkt.clouddn.com/20170411149188473495637.png)


# 参考
>https://golang.org/doc/install?download=go1.8.1.darwin-amd64.pkg

