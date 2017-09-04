---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Debugging-Package
subtitle: ''
date: 2017-08-24T01:05:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 使用调试

### 通过Vapor

默认情况下,调试包已经包含在Vapor中,只需要添加

```
import Debugging
```

### 没有Vapor

调试是一个便利的协议,用于提供有关错误消息的更多信息,你可以在任何Swift项目中使用它.

```
import PackageDescription

let package = Package(
    name: "Project",
    dependencies: [
        ...
        .Package(url: "https://github.com/vapor/debugging.git", majorVersion: 1)
    ],
    exclude: [ ... ]
)
```

使用`import Debugging`来访问调试的API.

