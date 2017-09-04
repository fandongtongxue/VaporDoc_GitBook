---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Routing-Parameters
subtitle: ''
date: 2017-08-09T14:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 路由参数

传统的Web框架通过使用路由参数名称和类型的字符串为路由留出错误控件,Vapor提取了Swift闭包的优势提供更安全和更直观的访问路由参数的方法.

> 也可以看看  
> 路由参数是指URL路径的一部分\(例如:/users/:id\)对于查询参数\(例如:?foo=bar\),请查阅[请求查询参数](https://docs.vapor.codes/2.0/http/request/#query-parameters)

### 类型安全

要创建一个类型安全的路由,只需要用一个类型替换你路径中的一部分

```
drop.get("users",Int.parameter){ req in
    let userId = try req.parameters.next(Int.self)
    return "You requester User #\(userId)"
}
```

这将创建一个匹配路径`users/:id`的路由,其中`:id`是一个`Int`类型,这是手动设置路由参数的样子

```
drop.get("users",":id"){ request in
    guard let userId = request.parameters["id"]?.int else{
        throw Abort.badRequest
    }
    return "You requested User #\(userId)"
}
```

这里你可以看到类型安全路由保存了~3行代码,并且还可以防止运行时错误,如拼写错误`:id`

### 可参数化

任何遵循可参数化的都可以被用作参数,默认情况下所有的Vapor [Models](http://www.jianshu.com/p/a919cd994f5b)都符合  
使用这一点,我们之前关于用户的例子可以进一步简化

```
drop.get("users",User.parameter){ req in
    let user = try req.parameters.next(User.self)
    return "You requested \(user.name)"
}
```

这里提供的标识符将自动用于查找用户,举个例子,如果`/users/5`被请求,会去找一个具有标识符5的用户,如果找到了,则请求成功并且调用关闭,如果没有找到,则抛出未找到的错误  
这里展示的是手动查找模型的方法

```
drop.get("users",Int.parameters){ req in
    let userId = try req.parameters.next(Int.self)
    guard let user = try User.find(userId) else{
        throw Abort.notFound
    }
    return "You requested \(user.name)"
}
```

### 协议

你可以符合自己的可参数化的类型

```
import Routing

extension Foo:Parameterizable {
    ///This unique slug is used to identify
    ///the parameter in ther router
    static var uniqueSlug: String{
        return "foo"
    }
    static func make(for parameter : String) throws -> Foo{
        ///custom lookup logic here
        ///the parameter string contains the infomation
        ///parsed from the URL.
        ...
    }
}
```

现在你可以使用这个类型进行类型安全的路由

```
drop.get("users","nickname",Foo.parameter) { req in
    let foo = try req.parameters.next(Foo.self)
}
```

### 组

类型安全参数也适用于[组](https://docs.vapor.codes/2.0/routing/group/)

```
let userGroup = drop.grouped("users",User.parameter)
userGroup.get("message"){req in
    let user = try req.parameters.next(User.self)
}
```



