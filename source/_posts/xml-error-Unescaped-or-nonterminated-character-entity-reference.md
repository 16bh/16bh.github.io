---
title: '[xml error]Unescaped & or nonterminated character/entity reference'
categories: IT
toc: false
comment: true
date: 2017-04-01 15:48:36
tags: [xml]
---



xml的某个标签中的值包含了&，会报下面的错误
`Unescaped & or nonterminated character/entity reference`

<!--more-->

网上流传的解决方法如下：

用`&amp;`代替`&`


但是stackoverflow上有个小哥表示自己不想这么干，就发了个帖子：[《我一定要用`&amp;`替换`&`符号吗》](http://stackoverflow.com/questions/3493405/do-i-really-need-to-encode-as-amp)

下面是大佬的回复：

>
Yes. Just as the error said, in HTML, attributes are #PCDATA meaning they're parsed. This means you can use character entities in the attributes. Using & by itself is wrong and if not for lenient browsers and the fact that this is HTML not XHTML, would break the parsing. Just escape it as &amp; and everything would be fine.

>HTML5 allows you to leave it unescaped, but only when the data that follows does not look like a valid character reference. However, it's better just to escape all instances of this symbol than worry about which ones should be and which ones don't need to be.

>Keep this point in mind; if you're not escaping & to &amp;, it's bad enough for data that you create (where the code could very well be invalid), you might also not be escaping tag delimiters, which is a huge problem for user-submitted data, which could very well lead to HTML and script injection, cookie stealing and other exploits.

>Please just escape your code. It will save you a lot of trouble in the future.
