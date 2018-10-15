---
title: magento设置后台配置的默认值
toc: false
date: 2016-07-20 14:19:02
categories:
tags: magento
---


在[《magento新建模块的后台配置》](http://16bh.github.io/2016/07/10/magento%E6%96%B0%E5%BB%BA%E6%A8%A1%E5%9D%97%E7%9A%84%E5%90%8E%E5%8F%B0%E9%85%8D%E7%BD%AE/)
中设置了系统的后台配置选项后，可以在`config.xml`中设置后台配置的默认值



<!--more-->


# 设置配置项的默认值

``` xml magento-practise.local/app/code/local/Nano/App/etc/config.xml
    <default>
        <app_options>
            <app_setting>
                <user_name>老王</user_name>
                <pass_word>laowang</pass_word>
            </app_setting>
        </app_options>
    </default>
```

其中，`app_options`、`app_setting`、`user_name`、`pass_word`均为你在同一目录下的`system.xml`中配置的唯一标识符

打开后台，结果如下：
![](/images/images/1468984141679.png)

# 默认值不生效解决方法
>**配置默认值的优先级：数据库 > `xml`配置文件**

设置后台配置文件的默认值，需要将`config.xml`与`systeml.xml`同时提交后才会生效

---


若先提交了`system.xml`，并在后台查看配置已经生效了，此时系统会将配置存入`core_config_data`表中，存入的默认值为`NULL`,如下图所示，再提交`config.xml`的时候，由于数据库中已经存入默认值且为空，导致设置的默认值不生效

![](/images/images/1468996708948.png)

如果要让`config.xml`中设置的默认值生效，可以将数据库中配置的值对应的记录删除，清除`magento`缓存后重新进入后台查看，默认值生效
此时查看表`core_config_data`中配置项的值，跟设置的默认值一样了

![](/images/images/1468996558123.png)
