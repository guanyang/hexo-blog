---
title: Spring工具包-csrf
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-06-08 11:01:18
subtitle: Spring工具包安全组件，支持csrf防护
tags:
- SpringBoot
- Spring
- csrf
categories:
- Java
---

### 概览
- csrf防护组件，支持referer验证、双重cookie验证，支持多种验证方式

### 使用指南
- Github源码：https://github.com/guanyang/spring-base-parent
- 最新Maven坐标

```
<dependency>
    <groupId>org.gy.framework</groupId>
    <artifactId>spring-base-csrf</artifactId>
    <version>1.0.1-SNAPSHOT</version>
</dependency>
```

### 配置说明

```
csrf:
  ## 验证方式(referer/token)(多种使用";"分隔)
  types: token
  ## referer验证方式下的url(多种使用";"分隔，使用token方式可以不配置)
  #referers: http://www.xxx.com
  ## token验证方式下的token参数名(使用referer方式可以不配置)
  paramName: csrf_token
  ## token验证方式下的cookie名(使用referer方式可以不配置)
  tokenName: csrf_token_cookie
  ## token验证方式下的token生成地址(使用referer方式可以不配置)
  tokenUrl: /api/token
  ## token验证方式下的cookie有效期(单位:s)(使用referer方式可以不配置)
  tokenMaxAge: 7200

```

- 在需要csrf验证的Controller方法加上@CsrfCheck注解
```
@GetMapping("/api")
@CsrfCheck
public Response test(@Valid TestRequestDTO dto) {
    return testService.test(dto);
}
```