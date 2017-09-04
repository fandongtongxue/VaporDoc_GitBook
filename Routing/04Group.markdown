---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Routing-Group
subtitle: ''
date: 2017-08-12T00:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 路由组

将路由分组可以很方便的将公用前缀,中间件,主机添加到多个路由.  
路由组有两种不同的形式,Group和Grouped.

### Group

Group\(没有"ed"的那个\)需要通过一个`RouteBuilder`闭包

```
drop.group("v1"){ v1 in
    v1.get("users"){ request in
        //get the user
    }
}
```

### Grouped

Grouped会返回一个你可以用来传递的`RouteBuilder`

```
let va = drop.grouped("v1")
v1.get("users"){ request in
    //get the users
}
```

### 中间件

你可以像一组路由中添加中间件,这对于身份验证特别有用.

```
drop.group(AuthMiddleware()){ authorized in
    authorized.get("token"){ request in
        //has been authorized
    }
}
```

### 主机

你可以限制一组路由的主机

```
drop.group(host:"vapor.codes"){ vapor in
    vapor.get {request in
        //only responds to requests to vapor.codes
    }
}
```

### 链

组可以被链在一起

```
drop.grouped(host:"vapor.codes").grouped(AuthMiddleware()).group("v1"){ authedSecureV1 in
    //add routes here
}
```



