---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）JWT-Package
subtitle: ''
date: 2017-08-13T12:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 使用JWT

这章节讲述怎么导入JWT包,不论你使用Vapor或者不使用Vapor

### 使用Vapor

最简单使用Vapor使用JWT就是包含JWT provider

```
import PackageDescription

let package = Package(
    name: "Project",
    dependencies: [
        .Package(url: "https://github.com/vapor/vapor.git", majorVersion: 2),
        .Package(url: "https://github.com/vapor/jwt-provider.git", majorVersion: 1)
    ],
    exclude: [ ... ]
)
```

JWT提供程序包会添加JWT到你的工程,并且会添加额外的,比如Vapor特别方便的就像`drop.signers`  
使用`import JWTProvider`

### 仅使用JWT

JWT提供程序包的核心是一个快速的,纯Swift的JWT对于解码,序列化和验证JSON Web令牌的实现

```
import PackageDescription

let package = Package(
    name: "Project",
    dependencies: [
        ...
        .Package(url: "https://github.com/vapor/jwt.git", majorVersion: 2)
    ],
    exclude: [ ... ]
)
```

使用`import JWT`来使用JWT类

