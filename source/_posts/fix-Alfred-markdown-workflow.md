---
title: markdown图片链接生成的Alfred脚本微调整
toc: false
date: 2016-07-08 12:04:14
categories: [Software]
tags: [markdown,afred]
---

> 注意：这是一篇过时的文章，博客的图片上传有更好的实践方式，见[此文](https://16bh.github.io/2018/10/15/a-cool-way-to-blog-by-hexo-and-typora/)

github上有个天才作者，开发了一个方便的[图片上传实用工具](https://github.com/tiann/markdown-img-upload)，可以方便、快速地在截图之后通过脚本把图片上传到七牛云然后得到一个图片链接



作者加入的这样的设定：markdwon里面的图片链接不是标准的markdown格式，而是html的img标签；这是因为在retina屏幕下截图的话，如果不做任何处理，在非retina屏幕下面，这个图片会直接扩大两倍，非常粗糙难看；因此，需要保存图片显示大小的信息，保证截图大小和显示大小一致；这里使用mac系统自带的sips工具拿到截图大小，然后直接把宽度放在img标签里面。这样在显示的时候，可以保证是和截图时大小一致。

然而我在使用的时候发现截图带上了尺寸，生成的如下所示的链接之后

```
<img src="/images/images/1467908925897.png" width="120"/>
```

在网页上显示的效果不是很好，图片不点开的话经常看不清楚




<!--more-->

看了一下作者写的`python`脚本，做了一些微小的调整：
1. 去掉了图片的尺寸
2. 将图片的链接改为标准的markdown格式

再次截图并粘贴之后得到的链接就是这样的了：

```
![](/images/images/1467950738418.png)
```

修改之后的脚本代码如下：

``` python
# coding: utf-8
from clipboard import get_paste_img_file
from upload import upload_qiniu
import util
import os
import subprocess
import sys
import time

if not os.path.exists(util.CONFIG_FILE):
    util.generate_config_file()

config = util.read_config()
if not config:
    util.notice('请先设置你的七牛图床信息')
    util.open_with_editor(util.CONFIG_FILE)
    sys.exit(0)

url = '%s/%s' % (config['url'], config['prefix'])

img_file, need_format, format = get_paste_img_file()
if img_file:
    # has image

    # use time to generate a unique upload_file name, we can not use the tmp file name
    upload_name = "%s.%s" % (int(time.time() * 1000), format)
    if need_format:
        #size_str = subprocess.check_output('sips -g pixelWidth %s | tail -n1 | cut -d" " -f4' % img_file.name, shell=True)
        #size = int(size_str.strip()) / 2
         #markdown_url = '<img src="%s/%s"/>' % (url, upload_name)
         markdown_url = '![](%s/%s)' % (url, upload_name)
    else:
        markdown_url = '%s/%s' % (url, upload_name)

    # make it to clipboard
    os.system("echo '%s' | pbcopy" % markdown_url)
    os.system('osascript -e \'tell application "System Events" to keystroke "v" using command down\'')
    upload_file = util.try_compress_png(img_file, format!='gif')
    if not upload_qiniu(upload_file.name, upload_name): util.notice("上传图片到图床失败，请检查网络后重试")
else:
    util.notice("剪切版里没有图片！")
```
