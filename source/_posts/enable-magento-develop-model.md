---
title: 开启开发者模式
date: 2016-06-30 18:26:22
categories: [IT]
tags: magento
---

> 开启了开发者模式后，可以直接在页面上显示错误信息。

1. `项目根目录/errors`下的`local.xml.sample` 修改为`local.xml`

2. 修改index.php

``` php

if (isset($_SERVER['MAGE_IS_DEVELOPER_MODE'])) {
    Mage::setIsDeveloperMode(true);
}

#ini_set('display_errors', 1);
```

改为

``` php
Mage::setIsDeveloperMode(true);
ini_set('display_errors', 1);
```
