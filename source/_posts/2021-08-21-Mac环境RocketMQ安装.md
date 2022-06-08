---
title: Mac环境RocketMQ安装
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2021-07-21 16:21:43
subtitle: Mac环境自己搭建RocketMQ服务，实现本地调试验证MQ相关功能
tags:
- RocketMQ
categories:
- MQ
---

### 下载
官网地址：http://rocketmq.apache.org/docs/quick-start/

### 运维管理
https://github.com/apache/rocketmq/blob/master/docs/cn/operation.md

### rocketMq 安装
#### 解压与编译

```bash
unzip rocketmq-all-4.9.0-source-release.zip
cd rocketmq-all-4.9.0/
mvn -Prelease-all -DskipTests clean install -U
cd distribution/target/rocketmq-4.9.0/rocketmq-4.9.0
```

#### 启动Name Server服务

```bash
# 1.启动NameServer
nohup sh bin/mqnamesrv &
# 2.查看启动日志
tail -f ~/logs/rocketmqlogs/namesrv.log

```

#### 修改内存大小
RocketMq默认内存较大，启动Borker如果因为内存不足启动失败，需要修改如下配置文件，修改JVM内存大小
- runborker.sh
- runserver.sh

改为： JAVA_OPT="${JAVA_OPT} -server -Xms256m -Xmx256m -Xmn128m"

#### 启动borker

```bash
# 1.启动Broker
nohup sh bin/mqbroker -n 127.0.0.1:9876 &

# 自定义配置文件
# nohup sh bin/mqbroker -n 192.168.0.5:9876 -c conf/broker.conf autoCreateTopicEnable=true &

# 2.查看启动日志
tail -f ~/logs/rocketmqlogs/broker.log 

```

#### 关闭rocketMq

```bash
# 关闭NameServer
sh bin/mqshutdown namesrv
# 关闭Borker
sh bin/mqshutdown broker
```
