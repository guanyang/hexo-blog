---
title: 用Serverless搭建个人静态相册网站
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-01-02 21:22:50
subtitle: 利用ThumbsUp工具，结合Serverless Framework 的 component 快速搭建个人相册网站，为存储空间减压
tags:
- Serverless
- ThumbsUp
categories:
- 综合
---

### 工具介绍
- Serverless Framework：Serverless Framework 是业界非常受欢迎的无服务器应用框架，开发者无需关心底层资源即可部署完整可用的 Serverless 应用架构
- ThumbsUp：是一款让使用者方便检索及管理图片的看图软件，不但具有可以快速的操作图片切换预览的使用介面，而且对于图片的简单影像处理也有相当直接、便捷的操作方式

### 安装与初始化
#### 首先确保系统包含以下环境：
- [Node.js](https://nodejs.org/en/) (Node.js 版本需不低于 8.6，建议使用 Node.js 10.0 及以上版本)
- [Exiftool](https://exiftool.org/)
- [图形 Magick](http://www.graphicsmagick.org/)
>如未安装上述应用程序，可以参考[安装说明](https://thumbsup.github.io/docs/2-installation/npm/)

#### 安装 Serverless Framework
```
$ npm install -g serverless
```
#### 安装 ThumbsUp
```
$ npm install -g thumbsup
```
#### 初始化项目
```
$ mkdir photos
$ thumbsup --input .\photos\ --output website
```
- 初始化成功后，可以看到项目目录结构：
```
.
├── photos
└── website
    └── index.html
```

### 配置 yml 文件【可选】
- 配置serverless.yml需要云服务资源支持，需要收费，作为可选项
- 项目目录下，创建 serverless.yml 文件
```
touch serverless.yml
```
- 将以下内容写入上述的 yml 文件里：
```
# serverless.yml

myWebsite:
  component: "@serverless/tencent-website"
  inputs:
    code:
      src: ./website
      index: index.html
      error: index.html
    region: ap-guangzhou
    bucketName: my-bucket-1111
```
- 配置完成后，文件目录如下：
```
.
├── photos
├── website
|   └── index.html
└── serverless.yml
```

### 部署
- 部署有如下两种方式：
  - 一种通过serverless.yml部署，需要云服务资源支持，需要收费
  - 通过自己的域名直接解析到上述`website`目录即可，自行上网搜索处理即可

#### serverless.yml部署介绍
- 通过 sls 命令进行部署，并可以添加 --debug 参数查看部署过程中的信息
- 如您的账号未登陆或[注册](https://cloud.tencent.com/register)腾讯云，您可以直接通过微信扫描命令行中的二维码进行授权登陆和注册


```
sls --debug

  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Starting Website Component.
  DEBUG ─ Preparing website Tencent COS bucket my-bucket-thumbsup-1256386184.
  DEBUG ─ Deploying "my-bucket-thumbsup-1256386184" bucket in the "ap-guangzhou" region.
  DEBUG ─ "my-bucket-thumbsup-1256386184" bucket was successfully deployed to the "ap-guangzhou" region.
  DEBUG ─ Setting ACL for "my-bucket-thumbsup-1256386184" bucket in the "ap-guangzhou" region.
  DEBUG ─ Ensuring no CORS are set for "my-bucket-thumbsup-1256386184" bucket in the "ap-guangzhou" region.
  DEBUG ─ Ensuring no Tags are set for "my-bucket-thumbsup-1256386184" bucket in the "ap-guangzhou" region.
  DEBUG ─ Configuring bucket my-bucket-thumbsup-1256386184 for website hosting.
  DEBUG ─ Uploading website files from D:\tencent-serverless\thumbsup\website to bucket my-bucket-thumbsup-1256386184.
  DEBUG ─ Starting upload to bucket my-bucket-thumbsup-1256386184 in region ap-guangzhou
  DEBUG ─ Uploading directory D:\tencent-serverless\thumbsup\website to bucket my-bucket-thumbsup-1256386184
  DEBUG ─ Website deployed successfully to URL: http://my-bucket-thumbsup-1256386184.cos-website.ap-guangzhou.myqcloud.com.

  myWebsite:
    url: http://my-bucket-thumbsup-1256386184.cos-website.ap-guangzhou.myqcloud.com
    env:

  13s » myWebsite » done
```
- 访问命令行输出的 website url，即可查看即可查看使用 Serverless Framework 部署的照片墙网站

>注：如果希望更新网站中的照片或者视频等文件，可以在 photos 文件夹更新照片后，在本地重新运行 thumbsup --input .\photos\ --output website 更新本地页面，再运行 sls 即可更新网站

### 小结
本文使用了非常流行的无服务器框架 Serverless Framework来搭建照片墙网站，更多产品信息可以点击进入官网学习。

>传送门：
- GitHub: [github.com/serverless](https://github.com/serverless/serverless/blob/master/README_CN.md)
- 官网：[serverless.com](https://cn.serverless.com/)
