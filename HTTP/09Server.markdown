---
layout: post
title: 基于Swift的Web框架Vapor2.0文档（翻译）HTTP-Server
subtitle: ''
date: 2017-08-21T14:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 服务器

服务器负责接受来自客户端的连接,解析他们的请求,并给他们发送响应

### 默认

使用默认服务器启动Droplet很简单

```
import Vapor

let drop = try Droplet()
try drop.run()
```

默认服务器将`0.0.0.0`主机绑定到`8080`端口.

### 配置文件

如果你正在使用`Config/server.json`文件,那么你可以轻松地更改你的主机和端口

```
{
    "port": "$PORT:8080",
    "host": "0.0.0.0",
    "securityLayer": "none"
}
```

以上就是`server.json`的默认形式,端口试图解决环境变量`$PORT`或者回退到`8080`.

### TLS

TLS\(以前成为SSL\)可以配置各种不同的证书和签名类型.

### 验证

可以禁用主机和证书的验证,默认情况下它们是启用的.

> 注意:禁用这些选项时请格外小心

```
"tls": {
    "verifyHost": false,
    "verifyCertificates": false
}
```

#### 证书

##### 无证书

```
"tls": {
    "certificates": "none"
}
```

##### 链

```
"tls": {
    "certificates": "chain",
    "chainFile": "/path/to/chainfile"
}
```

##### 文件

```
"tls": {
    "certificates": "files",
    "certificateFile": "/path/to/cert.pem",
    "privateKeyFile": "/path/to/key.pem"
}
```

##### 认证机构

```
"tls": {
    "certificates": "ca"
}
```

#### 签名

##### 自己签名

```
"tls": {
    "signature": "selfSigned"
}
```

##### 文件签名

```
"tls": {
    "signature": "signedFile",
    "caCertificateFile": "/path/to/file"
}
```

##### 目录签名

```
"tls": {
    "signature": "signedDirectory",
    "caCertificateDirectory": "/path/to/dir"
}
```

### 示例

以下是使用自己签名签名和主机冗余设置为真的证书文件的`server.json`文件的示例.

```
{
    "port": "8443",
    "host": "0.0.0.0",
    "securityLayer": "tls",
    "tls": {
        "verifyHost": true,
        "certificates": "files",
        "certificateFile": "/vapor/certs/cert.pem",
        "privateKeyFile": "/vapor/certs/key.pem",
        "signature": "selfSigned"
    }
}
```

### Nginx

强烈建议您在生产环境中运行您的Vapor项目时依托于Nginx,在[部署Nginx](http://www.jianshu.com/p/e211efa92785)章节中了解更多.

