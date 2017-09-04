---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Debugging-Overview
subtitle: ''
date: 2017-08-24T01:09:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 调试

确认你的错误类型可以被调试,并且允许Vapor创建更丰富的错误消息,使调试变得更容易.

```
import Debugging

extension FooError: Debuggable {
    // conform here
}
```

现在当抛出一个`FooError`,你会得到一个很好的消息在您的控制台.

    Foo Error: You do not have a `foo`.

    Identifier: DebuggingTests.FooError.noFoo

    Here are some possible causes: 
    - You did not set the flongwaffle.
    - The session ended before a `Foo` could be made.
    - The universe conspires against us all.
    - Computers are hard.

    These suggestions could address the issue: 
    - You really want to use a `Bar` here.
    - Take up the guitar and move to the beach.

    Vapor's documentation talks about this: 
    - http://documentation.com/Foo
    - http://documentation.com/foo/noFoo



