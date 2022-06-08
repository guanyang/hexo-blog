---
title: Spring工具包-util
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-06-08 11:13:38
subtitle: Spring工具包常用工具类合集
tags:
- SpringBoot
- Spring
- file
- http
- net
- regex
categories:
- Java
---

### 概览
- 常用工具类定义，避免重复造轮子，提升效率
  - AES加密
  - 枚举定义
  - 数据加载，避免深度分页
  - 版本号比较
  - 图片过滤清洗，防止违规内容
  - 图片添加水印
  - IP/Cookie工具类
  - 常用正则合集
  - 参数校验注解，支持集合和枚举校验

### 使用指南
- Github源码：https://github.com/guanyang/spring-base-parent
- 最新Maven坐标
```
<dependency>
  <groupId>org.gy.framework</groupId>
  <artifactId>spring-base-util</artifactId>
  <version>1.0.1-SNAPSHOT</version>
</dependency>
```

### 工程结构解读
```
├── README.md
├── pom.xml
├── src
│   ├── main
│       ├── java
│           └── org
│               └── gy
│                   └── framework
│                       └── util
│                           ├── code            //常用编码合集，例如AES加密
│                           ├── data            //数据加载，避免深度分页；版本号比较
│                           ├── file            //图片过滤清洗，防止违规内容；图片添加水印
│                           ├── http            //IP/Cookie工具类
│                           ├── net             //网络相关工具类
│                           ├── regex           //常用正则合集
│                           ├── response        //json/jsonp内容输出
│                           └── validation      //参数校验注解，支持集合和枚举校验
```