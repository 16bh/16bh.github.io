---
title: magento计划任务
toc: false
date: 2016-07-19 17:56:24
categories: IT
tags: [magento,crontab]
---



设置计划任务，定时运行脚本。


<!--more-->

修改模块的配置文件`config.xml`：

``` xml Module_Name/etc/config.xml
 <crontab>
        <jobs>
            <计划任务标识>
                <schedule><cron_expr>0 */1 * * *</cron_expr></schedule>   <!--定时1分钟-->
                <run><model>你想要运行的脚本文件</model></run>
            </计划任务标识>
        </jobs>
  </crontab>
```

所有的计划任务存在`cron_schedule`表中
