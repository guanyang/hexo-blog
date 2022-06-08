---
title: Alpine Linux教程
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-06-08 16:32:20
subtitle: Alpine Linux是一个由社区开发的Linux操作系统，该操作系统以安全为理念，面向x86路由器、防火墙、虚拟专用网、IP电话盒及服务器而设计
tags:
- Alpine
categories:
- Linux
---

### Alpine更新国内源
#### 源文件
- 文件名：`/etc/apk/repositories`
- 默认的源地址为：`https://dl-cdn.alpinelinux.org/`

#### 国内源
- 注意查看源文件对应的版本，以下版本号需要对应修改
- 采用国内阿里云的源，文件内容为：
```
https://mirrors.aliyun.com/alpine/v3.9/main/
https://mirrors.aliyun.com/alpine/v3.9/community/
```

- 如果采用中国科技大学的源，文件内容为：
```
https://mirrors.ustc.edu.cn/alpine/v3.9/main/
https://mirrors.ustc.edu.cn/alpine/v3.9/community/
```
- 采用清华源，文件内容为
```
https://mirror.tuna.tsinghua.edu.cn/alpine/v3.9/main/
https://mirror.tuna.tsinghua.edu.cn/alpine/v3.9/community/

```

#### 更新源
```
sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
```

### 软件包管理工具apk使用
- 查询软件包
```
apk search xxx 
```
- 安装软件包
```
apk add xxx 
```
- 删除软件包
```
apk del xxx 
```
- 获取更多apk包管理的命令参数
```
apk --help
```

### 参考文档
- 官网：https://www.alpinelinux.org/
- Github：https://github.com/alpinelinux