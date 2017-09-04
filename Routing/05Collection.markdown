---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Routing-Collection
subtitle: ''
date: 2017-08-12T01:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 路由集合

路由集合允许将多个路由和路由组组织在不同的文件和模块中.

### 示例

这是`v1`API部分的路由集合示例

```
import Vapor
import HTTP
import Routing

class V1Collection: RouteCollection{
    func build(_builder:RouteBuilder){
        let v1 = builder.grouped("v1")
        let users = v1.grouped("users")
        let articles = v1.grouped("articles")

        users.get{ request in
            return "Requested all users."
        }

        articles.get(Article.init){ request, article in
            return "Requested \(article.name)"
        }
    }
}
```

这个类可以放到任何文件中,我们也可以把它添加到我们的Droplet甚至另一个路由组.

```
let v1 = V1Collection()
drop.collection(v1)
```

Droplet将会被传递给您的路由集合的`build(_:)`方法,并添加各种路由.

### 空的初始化方法

你可以添加`EmptyInitializable`到你的路由集合,并且如果路由集合有一个空的初始化方法,这就允许你通过其类型名称添加路由集合

```
class V1Collection: RouteCollection,EmptyInitiallizable {
    init(){}
    ...
}
```

现在我们可以添加路由集合而不初始化它

