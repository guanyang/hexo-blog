---
title: Spring工具包-xss
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-06-08 11:13:44
subtitle: Spring工具包XSS组件，防止XSS注入风险
tags:
- SpringBoot
- Spring
- xss
categories:
- Java
---

### 概览
- 针对请求对象的所有String字段自动进行trim、checkXss
- 如果监测有xss风险，将抛出`XssException`，可针对此异常定制全局异常处理

### 使用指南
- Github源码：https://github.com/guanyang/spring-base-parent
- 最新Maven坐标

```
<dependency>
    <groupId>org.gy.framework</groupId>
    <artifactId>spring-base-xss</artifactId>
    <version>1.0.1-SNAPSHOT</version>
</dependency>
```

### 配置说明
- 应用入口类添加`@EnableXss`注解，启动Xss检查
- 当前组件只针对`RestController`或者`Controller`标注的类进行xss校验
- 请求对象需要添加`@Valid`或者`@Validated`注解才会进行校验
- 如果某些特殊场景需要跳过Xss检查，可以在对应字段上添加如下注解
```
//check设置false，跳过xss检查，trim设置true，进行去空格处理
@XssCheck(check = false, trim = true)
private String name;
```
