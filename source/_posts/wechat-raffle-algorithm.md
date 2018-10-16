---
title: 微信领红包问题
categories:
tags: [php,算法]
toc: false
comment: true
date: 2017-06-08 14:54:33
---

> 参考：https://www.zhihu.com/question/22625187

需求：每个人领到的红包大小相近，每次点击领取红包时计算

微信红包原理是每次领取红包在（0.01，剩下的钱/剩下的人*2）之间随机


<!--more-->

``` php
<?php
//随机小数
function randomFloat($min = 0, $max = 1) {
    return $min + mt_rand() / mt_getrandmax() * ($max - $min);
}


function raffle()
{
    $total = 100;
    $num = 10;
    $leftTotal = 100;
    $leftNum = 10;
    $minLimit = 0.01;

    for($i=0;$i<$num;$i++)
    {
        if (1 == $leftNum) {
            $money = $leftTotal;
            echo $money."\n";
            break;
        }
        $money = randomFloat($minLimit,$leftTotal/$leftNum*2);
        echo $money."\n";
        $leftTotal -= $money;
        $leftNum --;
    }
    
}

raffle();


```