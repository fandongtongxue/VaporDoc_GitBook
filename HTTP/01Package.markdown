---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）HTTP-Package
subtitle: ''
date: 2017-08-15T13:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 使用HTTP

### 通过Vapor

这个包是Vapor默认包含的,只需要添加下面这句

```
import HTTP
```

### 不通过Vapor

HTTP提供了为任何服务器端项目创建基于HTTP的应用程序所需的一切,要将其包含在您的包中,请将以下内容添加到您的`Package.swift`文件中.

```
import PackageDescription

let package = Package(
    name: "Project",
    dependencies: [
        ...
        .Package(url: "https://github.com/vapor/engine.git", majorVersion: 2)
    ],
    exclude: [ ... ]
)
```

使用`import HTTP`来访问HTTP的API

