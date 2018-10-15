---
title: yaf学习笔记 - request类和respose类
toc: true
comment: true
date: 2017-07-26 16:48:53
categories:
tags: yaf
---


<img src="/images/20170726150106236928086.png" width="492" height="297"/>



<!--more-->

## Yaf-Request-Abstract

```
/* Methods */
public void getActionName ( void )
public void getBaseUri ( void )
public void getControllerName ( void )
public void getEnv ( string $name [, string $default ] )
public void getException ( void )
public void getLanguage ( void )
public void getMethod ( void )
public void getModuleName ( void )
public void getParam ( string $name [, string $default ] )
public void getParams ( void )
public void getRequestUri ( void )
public void getServer ( string $name [, string $default ] )
public void isCli ( void )
public void isDispatched ( void )
public void isGet ( void )
public void isHead ( void )
public void isOptions ( void )
public void isPost ( void )
public void isPut ( void )
public void isRouted ( void )
public void isXmlHttpRequest ( void )
public void setActionName ( string $action )
public bool setBaseUri ( string $uir )
public void setControllerName ( string $controller )
public void setDispatched ( void )
public void setModuleName ( string $module )
public void setParam ( string $name [, string $value ] )
public void setRequestUri ( string $uir )
public void setRouted ([ string $flag ] )
```

## Yaf-Response-Abstract

```
/* Methods */
public bool appendBody ( string $content [, string $key ] )
public bool clearBody ([ string $key ] )
public void clearHeaders ( void )
private void __clone ( void )
public __construct ( void )
public void __destruct ( void )
public mixed getBody ([ string $key ] )
public void getHeader ( void )
public bool prependBody ( string $content [, string $key ] )
public void response ( void )
protected void setAllHeaders ( void )
public bool setBody ( string $content [, string $key ] )
public void setHeader ( void )
public void setRedirect ( void )
private void __toString ( void )
```

## 引用

 - [Yaf-Response-Abstract](http://php.net/manual/en/class.yaf-response-abstract.php)

 - [Yaf-Request-Abstract](http://php.net/manual/en/class.yaf-request-abstract.php)
