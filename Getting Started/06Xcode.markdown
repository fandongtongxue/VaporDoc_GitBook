---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）Xcode
subtitle: ''
date: 2017-08-06T14:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## Xcode

如果你在Mac做开发，你可以在Xocde上开发你的Vapor工程，通过Xcode你可以编译，运行，停止你的服务，当然你也可以用断点来调试你的代码  
![](http://om2bks7xs.bkt.clouddn.com/2017-08-06-Swift-Vapor-Web-06-1.png)  
你首先需要生成一个\*.xcodeproj文件来使用Xcode开发  
选择'Run'  
在你生成Xcode工程文件之后确保你选择了可执行的运行方式  
![](http://om2bks7xs.bkt.clouddn.com/2017-08-06-Swift-Vapor-Web-06-2.png)

### 生成工程文件

#### Vapor 工具箱

用以下命令生成Xcode工程

```
vapor xcode
```

> 提示  
> 如果你希望它生成完工程文件直接打开用`vapor xcode -y`

#### 手动

手动生成一个Xcode工程文件

```
swift package generate-xcodeproj
```

打开工程文件来正常继续

