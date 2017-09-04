---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Core-Overview
subtitle: ''
date: 2017-08-24T00:55:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## Core\(核心\)

Core\(核心\)为常用任务提供了一些便利

### 后台

用`backgroud()`可以轻松创建一个后台线程

```
print("hello")

try background {
    print("world")  
}
```

### Portal

Protals允许你创建异步任务闭包

```
let result = try Portal.open { portal in
    someAsyncTask { result in
        portal.close(with: result)
    }
}

print(result) // the result from the async task
```

### RFC1123

创建RFC1123类型的日期.

```
let now = Date().rfc1123 // string
```

你也可以解析RFC1123的字符串

```
let parsed = Date(rfc1123: "Mon, 10 Apr 2017 11:26:13 GMT")
```



