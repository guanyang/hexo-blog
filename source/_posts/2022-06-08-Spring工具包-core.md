---
title: Spring工具包-core
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-06-08 10:39:41
subtitle: Spring工具包核心，定义基础DTO、异常及错误码
tags:
- SpringBoot
- Spring
- Exception
- Filter
- StateMachine
categories:
- Java
---

### 概览
- 定义DTO，规范输入输出格式，参考`Response`
- 定义错误码、异常，参考`CommonException`
- 定义事件接口契约，参考`EventI`
- 添加`Filter`和`FilterChain`支持，方便自由定制
- 定义TraceId生成工具，参考`TraceUtils`
- 添加`StateMachine`状态机，支持`Fluent API`调用
- 定义枚举类标准，统一格式，参考`IStdEnum`

### 使用指南
- Github源码：https://github.com/guanyang/spring-base-parent
- 最新Maven坐标
```
<dependency>
  <groupId>org.gy.framework</groupId>
  <artifactId>spring-base-core</artifactId>
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
│                       └── core
│                           ├── dto             //统一DTO定义，规范格式
│                           ├── event           //定义事件接口契约
│                           ├── exception       //定义异常及错误码
│                           ├── filter          //定义Filter和FilterChain
│                           ├── statemachine    //状态机定义
│                           ├── support         //常用支持类定义，例如枚举标准格式定义
│                           ├── trace           //定义TraceId生成工具
│                           └── util            //常用工具类，例如JSON工具
```
