---
title: Spring工具包-limit
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-06-08 11:09:20
subtitle: Spring工具包限流组件，支持全局限流和SPI扩展
tags:
- SpringBoot
- Spring
- RateLimiter
categories:
- Java
---

### 概览
- 当前组件主要用于应用访问频率限制，添加注解`LimitCheck`即可快速接入使用
- 默认支持基于`redis`实现的频率访问控制，需要应用配置`StringRedisTemplate`实例
- 支持SPI方式扩展实现，接口类：`org.gy.framework.limit.core.ILimitCheckService`

### 使用指南
- Github源码：https://github.com/guanyang/spring-base-parent
- 最新Maven坐标

```
<dependency>
    <groupId>org.gy.framework</groupId>
    <artifactId>spring-base-limit</artifactId>
    <version>1.0.1-SNAPSHOT</version>
</dependency>
```

### 配置说明
1. 需要在启动类添加`@EnableLimitCheck`注解
```
//如果应用配置多个StringRedisTemplate，需要注入指定bean，启动类添加如下注解，注意修改bean名称：
@EnableLimitCheck(redisTemplateName = "stringRedisTemplate")
```

2. 注解调用示例如下，支持Spel表达式
```
//当前示例场景：300秒只能调用1次
@LimitCheck(key = "'GY:LOCK:TEST:' + #user.name", limit = 1, time = 300)
public void test(User user){
    System.out.println("------------>>>>>>>>"+user);
}
```
