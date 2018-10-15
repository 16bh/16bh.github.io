---
title: go学习笔记：安装并运行hello world
categories:
tags: [go]
toc: false
comment: true
date: 2017-04-11 11:53:15
---

<img src="/images/20170411149188484167726.png" width="492" height="297"/>

- homebrew安装go
- 配置环境变量
- 在终端运行go程序


<!--more-->

# 通过homebrew安装go

```
brew update
brew install go
```

查看安装的路径：

<img src="/images/20170727150113573556935.png" />

# 添加环境变量

编辑`~/.zshrc`

```
export GOROOT=/usr/local/opt/go/libexec
export GOPATH=$HOME/go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```
保存后执行

```
source ~/.zshrc
```


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

## go run
在终端执行
```
cd ~/code/go/src/hello.go
go run hello.go
```
<img src="/images/20170727150113791458287.png"/>


## go build
也可以先用`build`命令编译，再执行

```
go build hello.go  //生成可执行文件hello
./hello
```

<img src="/images/20170727150114608372047.png" />


## go tool objdump 查看执行过程

>[https://golang.org/cmd/objdump/](https://golang.org/cmd/objdump/)
> Objdump prints a disassembly of all text symbols (code) in the binary. If the -s option is present, objdump only disassembles symbols with names matching the regular expression.

```
go build hello.go
go tool objdump -s "main\.main" hello
```

<img src="/images/20170727150114621467973.png" />

# 参考
>https://golang.org/doc/install?download=go1.8.1.darwin-amd64.pkg

