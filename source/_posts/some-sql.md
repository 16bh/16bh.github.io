---
title: 常用sql操作
toc: false
date: 2016-10-28 12:08:42
categories: [IT,mysql]
tags: mysql
---



常用sql操作


<!--more-->

1. 统计查询结果的数量
    
    ```
    select count(*) from 
    ```
2. 查询时间时加8小时
    ```
    select * from table where date_add(time,interval 8 hour)> '2016-10-01 10:00:00'
    ```
3. 修改字段属性
    ```
    alter table `{$installer->getTable('memebox_auth/device')}`
           modify `device_id` varchar(256);
    ```