---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）HTTP-ResponseRepresentable
subtitle: ''
date: 2017-08-20T13:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## ResponseRepresentable

传统的HTTP服务器,发送一个请求,返回一个响应,Vapor也不例外,但是我们可以利用Swift强大的协议来使用户面对API更加灵活.  
让我们从定义`ResponseRepresentable`开始吧

```
public protocol ResponseRepresentable {
    func makeResponse() throws -> Response
}
```

通过遵循这个协议,我们可以更灵活的返回符合要求的内容,而不是每次手动创建响应,Vapor默认提供其中的一些,包含但不仅限于:

#### 字符串

因为字符串遵循`ResponseRepresentable`,所以我们可以直接在Vapor路由处理程序中直接返回.

```
drop.get("hello") { request in
    return "Hello, World!"
}
```

#### JSON

`JSON`可以直接返回,而不是每次重新创建响应.

```
drop.get("hello") { request in
    var json = JSON()
    try json.set("hello", "world")
    try json.set("some-numbers", [1, 2, 3])
    return json
}
```

#### 响应

当然我们也可以返回任何未涵盖的内容作为响应

```
drop.get("hello") { request in
    return Response(
        status: .ok, 
        headers: ["Content-Type": "text/plain"], 
        body: "Hello, World!"
    )
}
```

### 遵循

我们所需要做的就是返回我们的遵循`ResponseRepresentable`的对象,我们来看一个示例类型,一个简单的博客发布模型:

```
import Foundation

struct BlogPost {
  let id: String
  let content: String
  let createdAt: NSDate
}
```

然后我们让他遵循`ResponseRepresentable`

```
import HTTP

extension BlogPost: ResponseRepresentable {
    func makeResponse() throws -> Response {
        var json = JSON()
        try json.set("id", id)
        try json.set("content", content)
        try json.set("created-at", createdAt.timeIntervalSince1970)
        return try json.makeResponse()
    }
}
```

现在我们已经建立了BlogPost,我们可以直接在路由处理程序中返回

```
drop.post("post") { req in
    guard let content = request.data["content"] else { 
        throw Error.missingContent 
    }
    let post = Post(content: content)
    try post.save(to: database)
    return post
}
```



