---
title: sublime插件 - markdown编辑和预览
toc: true
date: 2016-07-11 18:49:38
categories:
tags: [sublime,markdown]
---


>sublime支持markdwon的编辑和预览
>通过分别安装Markdown Preview和MarkdownEditing插件来实现
>跟其他markdown编辑器比较，sublime编写环境更加美观

<!--more-->

# MarkDownEditing

如本文的编辑效果如图所示：
![](/images/images/1468241270431.png)


# MarkDown Preview

安装插件完成后，设置快捷键：

打开`Sublime Text`>`Perferences`>`Key Bindings - User`,添加如下：

```
{"keys": ["alt+m"], "command": "markdown_preview", "args": { "target": "browser"}}
```

然后，就可以用`Option`+`M`快捷键通过默认浏览器查看`markdown`文件的预览
