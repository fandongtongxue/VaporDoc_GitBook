---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Validation-Package
subtitle: ''
date: 2017-08-22T08:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 使用验证

本概述章节讲解如何导入Validation软件包,无论你是否使用Vapor项目.

### 使用Vapor

使用Vapor来使用验证软件包最简单的方法就是包含验证包的提供程序.

```
import PackageDescription

let package = Package(
    name: "Project",
    dependencies: [
        .Package(url: "https://github.com/vapor/vapor.git", majorVersion: 2),
        .Package(url: "https://github.com/vapor/validation-provider.git", majorVersion: 1)
    ],
    exclude: [ ... ]
)
```

验证提供程序添加验证包到你的Vapor工程,并且添加了一些Vapor特定的便利,比如验证的中间件.  
使用`import ValidationProvider`将会导入验证中间件和验证模块.

### 仅使用验证

验证提供程序的核心是验证模块.

```
import PackageDescription

let package = Package(
    name: "Project",
    dependencies: [
        ...
        .Package(url: "https://github.com/vapor/validation.git", majorVersion: 1)
    ],
    exclude: [ ... ]
)
```

使用`import Validation`来访问核心验证的类

