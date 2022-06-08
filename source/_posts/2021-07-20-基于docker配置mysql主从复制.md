---
title: 基于docker配置mysql主从复制
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2021-07-20 16:55:40
subtitle: 基于docker，实现mysql主从复制配置
tags:
- mysql
- docker
categories:
- SQL
---

### 创建容器
- 主节点容器创建

```bash
docker run --name mastermysql  -d -p 3307:3306 -e MYSQL_ROOT_PASSWORD=123456 -v /usr/local/docker/mysql/master/data:/var/lib/mysql -v /usr/local/docker/mysql/master/conf/my.cnf:/etc/mysql/my.cnf  mysql:5.7.19
```

-  主节点配置my.cnf

```bash
[mysqld]
log-bin=mysql-bin
server-id=1
binlog-ignore-db=information_schema
binlog-ignore-db=cluster
binlog-ignore-db=mysql
binlog-do-db=demo
```

- 从节点容器创建

```bash
docker run --name slavemysql  -d -p 3308:3306 -e MYSQL_ROOT_PASSWORD=123456 -v /usr/local/docker/mysql/slave/data:/var/lib/mysql -v /usr/local/docker/mysql/slave/conf/my.cnf:/etc/mysql/my.cnf  mysql:5.7.19
```

- 从节点配置my.cnf

```bash
[mysqld]
log-bin=mysql-bin
server-id=2
binlog-ignore-db=information_schema
binlog-ignore-db=cluster
binlog-ignore-db=mysql
replicate-do-db=demo
replicate-ignore-db=mysql
log-slave-updates
slave-skip-errors=all
slave-net-timeout=60
```

### 进入容器
- 主：docker exec -it mastermysql bash
- 从：docker exec -it slavemysql bash

### 授权复制权限
- 创建用户

```bash
create user 'slave'@'%' identified by '123456';
```
- 授权

```bash
GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'slave'@'%';

flush privileges;
```

### 查询节点状态

```bash
# 主：
show master status;
# 从：
show slave status;
```

### 从节点配置主从连接
```bash
stop slave;

change master to master_host='172.17.0.3',master_user='slave',master_password='123456',master_log_file='mysql-bin.000007',master_log_pos=871,master_port=3306;

start slave;

```

注：查询主容器ip

```bash
docker inspect --format='{{.NetworkSettings.IPAddress}}' 容器名称|容器id
```

### 创建只读用户
```bash
create user 'reader'@'%' identified by '123456';

GRANT Select ON *.* TO 'reader'@'%';
```