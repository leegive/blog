---
title: JAXB在java9及以上找不到依赖的问题
date: 2019-03-09 22:24:29
tags:
---
JAXB Api 是java ee 的api， java9以上版本引入了模块的概念，java se中不再包含java ee的jar
<!-- more -->

解决方案在pom.xml增加jaxb依赖

```xml
<dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
    <version>2.3.0</version>
</dependency>
<dependency>
    <groupId>com.sun.xml.bind</groupId>
    <artifactId>jaxb-impl</artifactId>
    <version>2.3.0</version>
</dependency>
<dependency>
    <groupId>com.sun.xml.bind</groupId>
    <artifactId>jaxb-core</artifactId>
    <version>2.3.0</version>
</dependency>
<dependency>
    <groupId>javax.activation</groupId>
    <artifactId>activation</artifactId>
    <version>1.1.1</version>
</dependency>
```