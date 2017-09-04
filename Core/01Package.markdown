---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Core-Package
subtitle: ''
date: 2017-08-24T00:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 使用Core\(核心\)

### 通过Vapor

默认情况下,这个依赖包就包含在Vapor当中,只需要添加

```
import Core
```

### 没有Vapor

Core\(核心\)为任何服务器端的Swift项目提供了大量的便利,要将其包含在您的包中,请将以下内容添加到您的`Package.swift`文件中.

```
import PackageDescription

let package = Package(
    name: "Project",
    dependencies: [
        ...
        .Package(url: "https://github.com/vapor/core.git", majorVersion: 2)
    ],
    exclude: [ ... ]
)
```

使用`import Core`方位Core\(核心\)的API.

