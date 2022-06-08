---
title: Spring工具包-sign
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-06-08 11:13:31
subtitle: Spring工具包签名组件，基于注解实现方法参数签名
tags:
- SpringBoot
- Spring
- 签名
- 验签
categories:
- Java
---

### 概览
- 接口签名、验签组件，方便接口添加验签特性、访问接口生成签名

### 使用指南
- Github源码：https://github.com/guanyang/spring-base-parent
- 最新Maven坐标

```
<dependency>
    <groupId>org.gy.framework</groupId>
    <artifactId>spring-base-sign</artifactId>
    <version>1.0.1-SNAPSHOT</version>
</dependency>
```

### 验签
- 添加配置
```
sign:
  client:
    apps:
      -
        appId: 1    // 分配给客户端的appId
        appKey: test1    // 分配给客户端的appSecret
      -
        appId: 2
        appKey: test2
```

- 定义请求参数类，该类实现`SignedReq`接口
- 在请求参数中需要参与签名的字段上添加`@SignParam`注解
```
@SignParam注解name属性用于该字段在生成签名时的健值，不指定则默认使用字段名
```
- 在需要验签的`Controller`方法加上`@SignCheck`注解
- 验签失败会抛出`SignInvalidException`异常，可以针对此异常定义返回调用方的信息

### 签名
- 使用`ParamSignUtils.sign(req, key)`生成签名
```
req类上使用@SignParam注解标识参与签名的字段，@SignParam注解name属性用于该字段在生成签名时的健值，不指定则默认使用字段名
```

### 签名规则
- 把请求参数键值对按字典序排序，然后进行拼接，例如：`key1=value1&key2=value2`
- 再拼接上appKey键值对`key=${appKey}`，例如：`key1=value1&key2=value2&key=${appKey}`
- 将上述拼接之后的字符串进行md5签名即可