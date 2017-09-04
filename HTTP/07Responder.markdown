---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）HTTP-Responder
subtitle: ''
date: 2017-08-21T01:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 响应者

`Responder`是一个简单的协议,定义了可以接受请求并且返回响应的对象的行为,在Vapor中最值得注意的是,他是链接`Droplet`和`Server`的API端点,我们来看看这个定义

```
public protocol Responder {
    func respond(to request: Request) throws -> Response
}
```

> 这个响应者协议和`Droplet`的相关性最明显,它是和服务器的关系,一般用户不太可能和它进行交互

### 简单

当然,Vapor为此提供了一些便利,作为练习,我们一般调用

```
try drop.run()
```

### 手动

正如我们刚刚提到的那样,Vapor的`Droplet`本身就符合`Responser`\(响应者协议\),和服务器的连接,这就意味着如果我们想手动的去服务我们的`Droplet`,我们可以

```
let server = try Server<TCPServerStream, Parser<Request>, Serializer<Response>>(port: port)
try server.start(responder: droplet)  { error in
    print("Got error: \(error)")
}
```

### 高级

我们可以让我们自己的对象遵循`Responder`\(响应者协议\),并且传递给服务器,我们来看一个例子

```
final class Responder: HTTP.Responder {
    func respond(to request: Request) throws -> Response {
        let body = "Hello World".makeBody()
        return Response(body: body)
    }
}
```

这只能为每个请求返回`Hello World`最常见的做法是与一些类型的路由进行关联.

```
final class Responder: HTTP.Responder {
    let router: Router = ...

    func respond(to request: Request) throws -> Response {
        return try router.route(request)
    }
}
```

然后我们将这个响应者传递给服务器,然后让他执行

```
let server = try Server<TCPServerStream, Parser<Request>, Serializer<Response>>(port: port)

print("visit http://localhost:\(port)/")
try server.start(responder: Responder()) { error in
    print("Got error: \(error)")
}
```

这可以用作手动实现功能的应用程序的跳出点

### 客户端

虽然`HTTP.Client`本身就是一个响应者,它本身不处理请求,它将传递到底层URI

