---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）HTTP-Response
subtitle: ''
date: 2017-08-17T00:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 响应

当我们构建结束点时,我们通常会返回请求的响应,如果我们正在发出请求,我们将受到.

```
public let status: Status
public var headers: [HeaderKey: String]
public var body: Body
public var data: Content
```

### 状态

与事件关联的http状态,例如`.ok`==200 ok

### 请求头

这些是与请求相关的头,如果你正在准备一个传出的响应,这可以用来添加你的密钥.

```
let contentType = response.headers["Content-Type"]
```

或者外发响应

```
let response = response ...
response.headers["Content-Type"] = "application/json"
response.headers["Authorization"] = ... my auth token
```

#### 扩展头

我们通常会尽可能的删除字符串类型的代码来改进代码库,我们可以使用通用的扩展向请求头中添加变量.

```
extension HTTP.KeyAccessible where Key == HeaderKey, Value == String {
    var customKey: String? {
      get {
        return self["Custom-Key"]
      }
      set {
        self["Custom-Key"] = newValue
      }
    }
}
```

实现这种模式后,我们的字符串`Custom-Key`包含在我们代码的一个部分中,我们现在可以这样访问:

```
let customKey = response.headers.customKey

// or

let request = ...
response.headers.customKey = "my custom value"
```

#### 请求体

这是与响应相关联的请求体,并表示通用数据有效载荷,您可以在相关联的[文档](https://docs.vapor.codes/2.0/http/body/)中查看有关请求体的更多信息  
对于响应,请求体最初设置为初始化,有两种主要类型.  
`BODYREPRESENTABLE`  
可以转换成二进制的对象,比如

```
let response = Response(status: .ok, body: "some string")
```

在上面的例子中,字符串将自动转换为正文,你自己的类型也可以做到这样.  
`BYTES DIRECTLY`  
如果我们已经有了我们自己的字节数组,我们可以像这样传递给它

```
let response = Response(status: .ok, body: .data(myArrayOfBytes))
```

`CHUNKED(分块)`  
要发送一个`HTTP.Response`块,我们可以传递一个闭包,我们将用来发送我们的响应部分.

```
let response = Response(status: .ok) { chunker in
  for name in ["joe", "pam", "cheryl"] {
      sleep(1)
      try chunker.send(name)
  }

  try chunker.close()
}
```

> 确保`close()`在chunker离开范围之前调用.

## 内容

我们可以访问内容和我们在请求中一样,这最常用于外发请求

```
let pokemonResponse = try drop.client.get("http://pokeapi.co/api/v2/pokemon/")
let names = pokemonResponse.data["results", "name"]?.array
```

## JSON

要在给定的响应中访问JSON,使用下面的代码

```
let json = request.response["hello"]
```

## 关键路径

获取更多信息,访问[这里](https://github.com/fandongtongxue/VaporDoc/blob/master/HTTP/02Request.markdown)

## 服务端文件

如果你只想从公共目录来查看服务端文件,你查看`FileMiddleware`应该是有用的.

```
let res = try Response(filePath: "/path/to/file.txt")
```

使用它来初始化文件路径的文件响应,例如,如果使用公共文件夹,文件名应该在前面添加公共目录的路径,即`drop.publicDir + "myFile.cool"`

```
Response(filePath: String, ifNoneMatch: String? = nil, chunkSize: Int = 2048) throws
```

如果没有匹配表示将用于检查客户端上次加载后文件是否已更改的ETag,这样像浏览器这样的客户端,可以缓存他们的文件,避免不必要的重复下载,最常计算的是`/ https://tools.ietf.org/html/rfc7232#section-3.2`

有关怎么使用的示例,请查看"FileMiddleware"

