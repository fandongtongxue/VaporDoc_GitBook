---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Redis-Package
subtitle: ''
date: 2017-08-12T04:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 使用Redis

这章节讲解如何导入Redis包,无论你是否使用Vapor项目

### 使用Vapor

最简单的在Vapor项目中使用Redis的方式包含Redis依赖

```
import PackageDescription

let package = Package(
    name:"Project",
    dependencies:[
        .Package(url: "https://github.com/vapor/vapor.git", majorVersion: 2),
       .Package(url: "https://github.com/vapor/redis-provider.git", majorVersion: 2)
    ],
    exclude: [...]
)
```

Redis提供程序包将Redis添加到你的项目中,并将符合Vapor的`CacheProtocol`  
使用`import RedisProvider.`

### 仅使用Redis

Redis提供程序的核心是一个纯粹的Swift Redis客户端,软件包本身可以用于将原始缓存查询发送到您的Redis数据库

```
import PackageDescription

let package = Package(
    name:"Project",
    dependencies:[
        .Package(url: "https://github.com/vapor/vapor.git", majorVersion: 2),
       .Package(url: "https://github.com/vapor/redis.git", majorVersion: 2)
    ],
    exclude: [...]
```

使用`import Redis`

