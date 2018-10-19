---
title: 常用sql操作
toc: false
date: 2016-10-28 12:08:42
categories: IT
tags: mysql
---



几个sql操作


<!--more-->

1. 统计查询结果的数量

    ```sql
    select count(*) from  table
    ```
2. 查询时间时加8小时
    ```sql
    select * from table where date_add(time,interval 8 hour)> '2016-10-01 10:00:00'
    ```
3. 修改字段属性
    ```sql
    alter table `{$installer->getTable('memebox_auth/device')}`
           modify `device_id` varchar(256);
    ```

4. 联合查询join

	```sql
	select * from A left join B on A.id=B.id where A.ctime>'2016-01-01' and B.status=0
	```

5. 分组group by

	``` sql
	select status,count(*) from order group by status
	```
