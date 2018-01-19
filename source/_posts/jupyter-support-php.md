---
title: jupyter support php
toc: true
comment: true
date: 2017-11-20 16:28:48
categories:
tags: [jupyter,php]
---



As we know, jupyter support python originally. It can also support other language like php.U need to install specific kenerl.


<!--more-->

## envirenement

- php7
- zeromq
- php-zmq
- jupyter
- composer

> just run `brew install zeromq` to install zeromq on mac
> 
> php7.0 don't support php-zmq,must upgrade to php7.1,then `brew install php71-zmq`

## install jupyter-PHP

download here https://litipk.github.io/Jupyter-PHP-Installer/


## notice

while installing, if you see error below:

You are running PHP-CLI with xdebug enabled. This will have a major impact on the kernel's performance.

it means that you have't install zeromq





---
any question, contact me by email