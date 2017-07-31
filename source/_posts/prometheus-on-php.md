---
title: 使用php对接prometheus监控系统
toc: true
comment: true
date: 2017-07-25 15:55:13
categories:
tags: php
---


<img src="http://o9xbyqajf.bkt.clouddn.com/20170725150097148897159.png" width="492" height="297"/>

<!--more-->

## 什么是prometheus

- 监控系统
- 报警机制
- 时间序列数据
- 支持Java,Go，PHP等

## prometheus_client_php

A prometheus client library written in PHP

<div class="github-widget" data-repo="Jimdo/ prometheus_client_php"></div>

## 对接prometheus系统

第一步 将监控数据写入适配器，如redis、apc
第二步 提供接口供prometheus系统调用


## 四种数据类型

- counter 计时器

只能增加value值，适合记录持续增长的，如接接口调用次数、请求总数、页面访问次数等

- gauge 尺度盘

可以任意修改value值,适合记录瞬时数据，如CPU使用率、内存使用情况、磁盘空间等

- histogram 直方图

用来度量数据中值的分布情况，如程序执行时间：0-100ms、100-200ms、200-300ms、>300ms 的分布情况

- summary

## adapter 存储介质

三种adapter

- apc
- redis
- in-memory

``` php
if ($adapter === 'redis') {
    Redis::setDefaultOptions(array('host' => isset($_SERVER['REDIS_HOST']) ? $_SERVER['REDIS_HOST'] : '127.0.0.1'));
    $adapter = new Prometheus\Storage\Redis();
} elseif ($adapter === 'apc') {
    $adapter = new Prometheus\Storage\APC();
} elseif ($adapter === 'in-memory') {
    $adapter = new Prometheus\Storage\InMemory();
}
```


## register 注册器

方法列表：

- registerCounter
- getCounter 
- getOrRegisterCounter
- registerGauge
- getGauge
- getOrRegisterGauge
- registerHistogram
- getHistogram 
- getOrRegisterHistogram

```
$registry = new CollectorRegistry($adapter);

//或者，获取默认的registry
$registry = \Prometheus\CollectorRegistry::getDefault();
```

## 供prometheus调用的接口

```
$registry = new CollectorRegistry($adapter);
$renderer = new RenderTextFormat();
$result = $renderer->render($registry->getMetricFamilySamples());

header('Content-type: ' . RenderTextFormat::MIME_TYPE);
echo $result;
```

## 清除测试数据

测试的时候想要清除在apc中存储的prometheus数据，可以调用下面的方法

```
$adapter = new Prometheus\Storage\APC();
$adapter->flushAPC();
```



同理，清除redis和memory

```
$adapter = new Prometheus\Storage\Redis();
$adapter->flushRedis();

$adapter = new Prometheus\Storage\InMemory();
$adapter->flushMemory();
```

## counter用法
 
 

```
 $counter = $registry->getOrRegisterCounter('aaa', 'bbb', 'ccc', ['color']);
 $counter->incBy(1, ['red']);
```
 
 结果为：
 
```
# HELP aaa_bbb ccc
# TYPE aaa_bbb counter
aaa_bbb{color="red"} 1
```


当然也可以同时设置两个label


```
 $counter = $registry->getOrRegisterCounter('aaa', 'bbb', 'ccc', ['color', 'size']);
 $counter->incBy(1, ['red', 10]);
```

 结果为：
 
```
# HELP aaa_bbb ccc
# TYPE aaa_bbb counter
aaa_bbb{color="red",size=10} 1
```

## gauge

```
$gauge = $registry->getOrRegisterGauge('test', 'some_gauge', 'it sets', ['type']);
$gauge->set(2.5, ['blue']);
```

## histogram

```
$histogram = $registry->getOrRegisterHistogram('test', 'some_histogram', 'it observes', ['type'], [0.1, 1, 2, 3.5, 4, 5, 6, 7, 8, 9]);
$histogram->observe(3.5, ['blue']);
```

