---
title: hexo如何安装主题
toc: true
date: 2016-07-05 11:43:41
categories: [Blog]
tags: hexo
---

>以`landscape-plus`主题为例,该主题是在默认主题`landscape`结合国人的使用习惯改进的

# 主题安装

终端执行命令
``` shell
cd hexo;    //进入你的hexo博客的根目录
git clone https://github.com/xiangming/landscape-plus.git themes/landscape-plus
```

<!--more-->

# 主题使用

修改配置文件 `hexo/_config.yml`

``` yml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape-plus
```


# 网站生效

切换主题后，网站不会立刻生效，需要用下面的命令删除缓存

``` shell
hexo clean;
```

然后就可以

```
hexo g -d
```

