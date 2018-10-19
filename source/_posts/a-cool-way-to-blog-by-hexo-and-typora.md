---
title: 一种酷炫的博客实践方式：hexo+typora
toc: true
comment: true
date: 2018-10-15 21:14:13
categories: [Blog]
tags: [hexo,typora]
---

博客的图片不能上传到七牛云了，也懒得去折腾那些在线的图床了，还是放在本地最安心

最近发现了mac上超好用又免费的一款markdown工具`Typora`，`Typora`自带的图片工具可以将本地图片直接复制到md文件中，并放在自定义的路径中，例如与当前md文件同名的文件夹中

这种格式以方便可以被编辑器`Typora`识别并预览

另一方面刚好也是`hexo`支持并可以预览的

于是，就产生了一种比较好的博客实践方式，即`hexo+typora`，详情见正文



<!--more-->

## 将博客中的图片从七牛云中下载到本地

[详见本文](https://16bh.github.io/2018/10/15/batch-download-image-from-qiniu/)

## 配置hexo支持本地图片

hexo3的一个新特性，是可以支持本地图片

有两种支持方式，参考[官方文章](https://hexo.io/zh-cn/docs/asset-folders)：

### 方法1

直接把图片放到`source/images`目录下,然后就可以通过`images/图片名称`的方式来使用图片了

1. 也可以放到`source/_posts/images`目录下，两者的区别在于放soure/images目录中_posts和_drafts里的文章都可以用，放在_posts/images目录只有posts可以用了。一般drafts草稿文件夹用不上，所以区别不大
2. 需要注意的是这种方式只支持一级目录，不能在images文件夹中再建立文件夹了。此时typora虽然可以识别，但是hexo渲染的时候会报错



### 方法2

每篇文章都单独建立文件夹存放图片

修改配置文件`*.github.io/_config.yml`

```yml
 post_asset_folder: true
```

这样每次之后，每次新建一篇md博文的时候，都会同时新建一个同名的文件夹用于存储该文章的图片

## 配置typora

上述的两种方式typora都支持



对于第2种方法

按如下方式配置`typora`，这样当你在md文件中插入一张图片的时候，刚好会被`typora`复制到hexo生成的文件文件夹中

![image-20181015213318141](a-cool-way-to-blog-by-hexo-and-typora/image-20181015213318141.png)

如上图，我截图并复制到markdown文件中后，就会被自动替换成下面的路径

```
![image-20181015213318141](a-cool-way-to-blog-by-hexo-and-typora/image-20181015213318141.png)
```

其中,`a-cool-way-to-blog-by-hexo-and-typora`是本文的标题



对于第1种方法

把上面的自定义路径修改为`./images`即可

## tips

有一篇文章指出的一点我觉得很好

图片能省则省，不要滥用图片，占用空间

其他关于hexo的使用，请参考以下文章：[hexo系列](https://16bh.github.io/tags/hexo)
