---
title: go学习笔记 - 语法
toc: true
comment: true
date: 2017-07-31 18:16:25
categories:
tags: go
---



<img src="/images/20170802150164469935152.png" width="492" height="297"/>


<!--more-->

# 特点

- 语法简易
- 自动格式化代码，保证所有人代码风格一致
- 并发处理
- 垃圾回收
- 函数多返回值，返回错误


# 代码规范

- 要有main包和main函数
- 变量必须要使用，引入的包必须要使用
- 表达式可以省略括号，不能省略花括号，左花括号必须在行尾

``` go
package main

import (
	"fmt"
)

func main() {
	a := 3
	if a > 1 {
		fmt.Printf("%T,%v", a, a)
	}
}
```

# 包

引入多个包

```
package main

import (
	"fmt"
	"math"
)
```
不可以import未被使用的包

# 变量


``` go
var a int8 = 4
var a = 4
a := 8    //:=只能用在函数内
```

byte: unit8

rune: int32


# 自增

不能前置，不能用作表达式

```
a++;  //√
++a;  //×
if (a++) {  //×
```

# 数组及遍历

``` go
package main

func main() {
	a := [3]int{1, 2, 3}
	for i, s := range a {
		println(i, s)
	}
}
```


# 指针
指针不能运算

``` go
package main

func main() {
	a := 3
	var p *int = &a
	print(*p)
}
```
# switch

对比下php和go的swithc语句

``` php
<?php
$a = 1
switch ($a) {
    case 1:
    case 2:
        echo 1;
        break;
    case 3:
        echo 3;
        break;
    default:
        echo 'default';
        break;
}
```

输出为1

``` go
package main

func main() {
	a := 1
	switch a {
	case 1:
	case 2:
		println(1)
		break
	case 3:
		println(3)
	default:
		break
	}
}
```

输出为空

go会自动在语句为空的case后面补上break，相当于没有执行任何操作

要实现php中的多个case执行相同的语句，应该使用下面的写法：

``` go
case 1,2:
	println(1)
	break
```

# for
初始语句和结束语句可以省略

```
for sum < 1000 {
	sum += sum
}
```

# 函数
需指定入参和出参的类型，可以返回多个值

```
//x后面的int可省略，根据王垠的博客说的最好保留
func add(x int, y int) int {
	return x + y
}
```

# defer

```
package main

import "fmt"

func main() {
	defer fmt.Println("world")

	fmt.Println("hello")
}
```

>输出结果：

>hello
>
>world

# struct
用点号`.`访问结构体中的字段

```
type Vertex struct {
	X int
	Y int
}
```

# slice

```
s := []int{2, 3, 5, 7, 11, 13}

//slice长度
len(s)

//slice转string,第二个参数是分隔符
strings.Join(s,'_')

//打印slice
fmt.Printf("%v", s)
```

# map

# 函数

函数可以作为函数的入参

闭包

>Go 函数可以是一个闭包。闭包是一个函数值，它引用了函数体之外的变量。 这个函数可以对这个引用的变量进行访问和赋值；换句话说这个函数被“绑定”在这个变量上。

# 并发
goroutine
channel

```
ch <- v    // 将 v 送入 channel ch
v := <-ch  // 从 ch 接收，并且赋值给 v
```

# 错误处理

# gc


# 参考

- [官网tutorial](https://tour.go-zh.org/list)
- [《Go语言学习笔记》，雨痕著](https://github.com/qyuhen/book)
- [王垠：对Go语言的综合评价](http://www.yinwang.org/blog-cn/2014/04/18/golang)
