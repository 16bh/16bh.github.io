---
title: 回收饮料瓶问题
categories: IT
tags: [php,算法]
toc: false
comment: true
date: 2017-06-08 14:43:54
---


x瓶饮料，喝完了每y个空瓶可以兑换一瓶新的饮料（y<x）,求总共可以喝多少瓶饮料？

<!--more-->

如x=10,y=2时，

- 第一次喝10瓶，得到10个空瓶，换5瓶
- 第二次喝5瓶，得到5个空瓶，换2瓶，剩1个空瓶
- 第三次喝2瓶，得到2个空瓶，加上之前剩的共3个空瓶，换1瓶，剩1个空瓶
- 第四次喝1瓶，得到1个空瓶，加上之前剩的共2个空瓶，换1瓶
- 第五次喝1瓶，得到1个空瓶，没的换


``` php
<?php

function getTotalNum($num,$step)
{
    $total = $num;
    $left = 0;
    while ($num >= $step) {
        $left = $num % $step;  //记录没有兑换的空瓶
        $num = floor($num/$step);
        $total += $num;
        $num += $left;  //将没有兑换的空瓶放到喝剩下的空瓶一起
    }
    return $total;
}

echo getTotalNum(10,2);//19
echo getTotalNum(20,3);//29
```
