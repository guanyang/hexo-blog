---
title: Apache Geode使用教程
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-01-21 19:58:18
subtitle: Geode可在广泛分布的云架构中提供对数据密集型应用程序的实时，一致的访问
tags:
- Apache Geode
- 分布式缓存
categories:
- Java
---

### 简介
- 可在广泛分布的云架构中提供对数据密集型应用程序的实时，一致的访问
- Geode还是一个内存数据管理系统，可提供可靠的异步事件通知和有保证的消息传递

### 相关文档
- 官方文档：https://geode.apache.org/docs/guide/114/about_geode.html

### geode下载及环境配置
- 下载地址：https://dlcdn.apache.org/geode/1.14.2/apache-geode-1.14.2.tgz

#### 下载解压
```bash
> cd /usr/local/src
##下载解压
> wget https://dlcdn.apache.org/geode/1.14.2/apache-geode-1.14.2.tgz
> tar -zxvf apache-geode-1.14.2.tgz
> mv apache-geode-1.14.2 /usr/local/geode
```
#### 配置环境

```bash
> vim /etc/profile

#编辑配置，并保存退出
> export GEODE_HOME=/usr/local/geode
> export PATH=$PATH:$GEODE_HOME/bin  

#立即生效
> source /etc/profile  

#查看gfsh版本
> gfsh version

```

### gfsh常用命令
- 启动服务并配置区域
```bash
#启用gfsh命令行
> gfsh

#启动locator
> start locator --name=locator1

#启动pulse，web应用，提供了图形化的监控界面，自动连接到locator的JMX管理器，地址：http://localhost:7070/pulse 默认账户：admin  密码：admin
> start pulse

# 启动缓存服务器，可以参考此命令启动多个，修改name和server-port
> start server --name=server1 --server-port=40404
> start server --name=server2 --server-port=40405

#创建一个复制持久区域
> create region --name=region1 --type=REPLICATE_PERSISTENT

#停止缓存服务器
> stop server --name=server1

#在第二个终端窗口中，运行以下命令以连接到集群
> connect --locator=localhost[10334]

#在当前gfsh会话中，停止集群
> shutdown --include-locators=true

```


- 其他常用命令

```bash

#用gfsh命令来查看集群中的区域
> list regions

#列出集群上的成员
> list members

#查看区域说明
> describe region --name=region1

#运行如下的put命令来将数据添加到区域中
> put --region=region1 --key=3 --value=three

#运行如下命令查询数据
> query --query="select * from /region1"

```

- 启用REST API
>API war路径：{install-dir}/tools/Extensions/geode-web-api-n.n.n.war
>API war可以单独启动，也可以基于cache server启动，将单独开启Jetty server进程

```bash

#基于cache server启动
> start server --name=server3 --server-port=40406 --start-rest-api=true --http-service-port=18080 --http-service-bind-address=localhost


#验证api是否部署成功，注意根据自己配置的host和port进行调整
> curl i http://localhost:18080/geode/v1
```

>swagger文档地址：http://localhost:18080/geode/docs/index.html

- 如何卸载
>关掉所有运行的Geode进程然后移除整个文件目录，没有额外的系统更改，也没有窗体注册需要修改
