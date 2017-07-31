---
title: landscape-plus主题代码高亮测试
toc: true
date: 2016-07-07 10:50:25
category:
tags: hexo
---

>IT博客怎么能没有代码高亮的功能呢
>hexo支持代码块的高亮，使用方式是在第一个\`\`\`后面接空格+语言名称,还可以在语言名称后面加上代码块的标题

## C语言
>\`\`\` c
>int main(){
> return main();
>}
>\`\`\`


``` c
int main(){
  return main();
}
```

<!--more-->

---

## php

>\`\`\` php 1.php
>array_values();
>for($a=0;$a<10;$a++){
>    break;
>}
>\`\`\`

``` php 1.php
array_values();
for($a=0;$a<10;$a++){
    break;
}
```

---

>\`\`\`
>array_values();
>for($a=0;$a<10;$a++){
>    break;
}
>\`\`\`

```
array_values();
for($a=0;$a<10;$a++){
    break;
}
```
注意：去掉语言名称就不会高亮了

---
## html

>\`\`\` html
><span>test</span>
>\`\`\`


``` html
<span>test</span>
```

---

## css
>\`\`\` css
>.id:{
>    border:1px solid red;
>}
>\`\`\`


``` css
.id:{
    border:1px solid red;
}
```

---

## yml

>\`\`\` yml
>\# Archives
>\# 2: Enable pagination
>\# 1: Disable pagination
>\# 0: Fully Disable
>archive: 1
>category: 1
>tag: 1
>\`\``

``` yml
# Archives
# 2: Enable pagination
# 1: Disable pagination
# 0: Fully Disable
archive: 1
category: 1
tag: 1
```
---
## xml

>\`\`\` xml
> <FirstElement>
>        Some Text
>    </FirstElement>
>\`\`\``


``` xml
<FirstElement>
        Some Text
</FirstElement>
```
