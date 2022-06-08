---
title: Maven Archetype搭建模板工程
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2021-11-22 17:59:12
subtitle: 基于Maven Archetype插件创建模板工程，快速创建应用
tags:
- maven
- archetype
categories:
- Java
---

## Archetype简介
- Archetype是一个maven项目模板工具包，帮助用户创建 Maven 项目模板，并为用户提供生成这些项目模板的参数化版本的方法

## Archetype创建
### 创建一个maven项目
- 任意创建一个maven项目，单module或多module都可以，示例如下：

```
demo-01 //主工程
 - demo-01-admmin-java //后台服务应用
 - demo-01-common //外围依赖服务聚合组件
 - demo-01-dao //业务db操作组件
 - demo-01-service-api //对外服务接口契约定义
 - demo-01-service-java //对外服务应用
 - demo-01-util //业务工具组件
```

- 在主pmo文件中引入maven-archetype-plugin，如下所示：

```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-archetype-plugin</artifactId>
    <version>3.2.0</version>
</plugin>
```
### 生成archetype
- 在刚才创建的maven工程根目录执行如下maven命令：

```
mvn archetype:create-from-project
```
- 如果出现类似`Could not resolve dependencies for project xxx`错误，是由于多module依赖导致，执行如下命令之后，再执行上述命令：

```
mvn clean install
```

### 发布archetype
- 生成archetype成功之后，会在项目根路径下生成target目录
- 进入target/generated-sources/archetype目录,目录结构如下，执行`mvn install`，将模板安装到本地，也可以deploy到私服

```
├── pom.xml
├── src
│   ├── main
│   │   └── resources
│   │       ├── META-INF
│   │       │   └── maven
│   │       │       └── archetype-metadata.xml      //模板描述文件
│   │       └── archetype-resources                 //模板资源目录，以下是多module资源文件
│   │           ├── README.md
│   │           ├── __rootArtifactId__-admin-java
│   │           │   ├── pom.xml
│   │           │   └── src
│   │           ├── __rootArtifactId__-common
│   │           │   ├── pom.xml
│   │           │   └── src
│   │           ├── __rootArtifactId__-dao
│   │           │   ├── pom.xml
│   │           │   └── src
│   │           ├── __rootArtifactId__-service-api
│   │           │   ├── pom.xml
│   │           │   └── src
│   │           ├── __rootArtifactId__-service-java
│   │           │   ├── pom.xml
│   │           │   └── src
│   │           ├── __rootArtifactId__-util
│   │           │   ├── pom.xml
│   │           │   └── src
│   │           └── pom.xml
│   └── test
│       └── resources
│           └── projects
│               └── basic
│                   ├── archetype.properties
│                   └── goal.txt



```

- [archetype-metadata.xml配置参考](http://maven.apache.org/archetype/archetype-models/archetype-descriptor/archetype-descriptor.html)

## Archetype使用
- [Maven Archetype Plugin文档](http://maven.apache.org/archetype/maven-archetype-plugin/generate-mojo.html)

### archetype命令行参数说明
- mvn archetype:generate：构建maven项目起始命令
- interactiveMode：交互模式，默认为true，在交互模式下运行命令，要求用户指定选用的原型，以及生成项目模版的groupId、artifactId、version、package等属性，否则执行失败
- archetypeCatalog：Archetype查找规则

```
archetype分类，这里按位置分类有:
‘local’  本地，通常是本地仓库的archetype-catalog.xml文件
‘remote’  远程，是maven的中央仓库
file://...' 直接指定本地文件位置archetype-catalog.xml
http://...' or 'https://...'  网络上的文件位置 archetype-catalog.xml
‘internal’ maven-archetype-plugin内置的
默认值是remote，local，创建原型时设置成internal，根据自定义的原型创建自定义工程时设置成local
```
- archetypeRepository：仓库URL地址；不指定，则默认从中央库查找
- archetypeGroupId：原型的groupId；默认值为org.apache.maven.archetypes
- archetypeArtifactId：原型的artifactId；默认值为maven-archetype-quickstart
- archetypeVersion：原型的version；默认值为1.0
- groupId：生成项目的groupId；必选
- artifactId：生成项目的artifactId；必选
- version：生成项目的version；默认值1.0-SNAPSHOT
- package：生成项目的源码包结构；默认值使用${groupId}
- basedir：项目生成的目录；默认值为当前目录

### 基于archetype模板构建新工程，命令示例如下：

```
mvn archetype:generate  \
    -DgroupId=xxx \                 //替换成自定义groupId
    -DartifactId=xxx \              //替换成自定义artifactId
    -Dversion=xxx \                 //替换成自定义version
    -Dpackage=xxx \                 //替换成自定义package路径
    -DarchetypeArtifactId=xxx \     //替换成自己生成的模板工程artifactId
    -DarchetypeGroupId=xxx \        //替换成自己生成的模板工程groupId
    -DarchetypeVersion=xxx          //替换成自己生成的模板工程version
```

