---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Config
subtitle: ''
date: 2017-08-07T14:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 使用路由

### 通过Vapor

这是Vapor默认就包含的包，只需要

```
import Routing
```

### 不通过Vapor

路由提供器是一个可以用在任意Web端Swift框架的纯Swift路由，要将它包含在你的包中，添加如下代码到你的`Package.swift`文件中

```
import PackageDescription
let package = Package{
      name:"Project",
      dependencies:[
      ...  
 .Package(url:"https://github.com/vapor/routing.git",majorVersion:2)
],
exculde:[...]
```

用`import Routing`来获取路由的APIs

