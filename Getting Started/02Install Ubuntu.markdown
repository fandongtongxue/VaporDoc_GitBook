---
layout: post
title: '基于Swift的Web框架Vapor2.0文档（翻译）Install: Ubuntu'
subtitle: ''
date: 2017-08-04T04:00:00.000Z
author: 范东
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - iOS
  - Swift
  - Web
  - Vapor
---

## 在Ubuntu上安装

只需要花一点时间就可以在Ubuntu上安装Vapor

### 支持

Vapor支持Swift支持的所有Ubuntu版本

| 版本 | 版本代号 |
| --- | --- |
| 16.10 | Yakkety Yak |
| 16.04 | Xenial Xerus |
| 16.10 | Trusty Tahr |

### APT Repo

添加Vapor的APT repo来获取Vapor所有的系统包

#### 快速脚本

用下面这个脚本简单添加Vapor的APT repo

```
eval "$(curl -sL https://apt.vapor.sh)"
```

> 备注  
> 这个命令需要curl  
> 你可以通过`sudo apt-get install curl`来安装curl

#### 手动安装

或者手动添加repo

```
wget -q https://repo.vapor.codes/apt/keyring.gpg -O- | sudo apt-key add -
```

```
echo "deb https://repo.vapor.codes/apt $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/vapor.list
```

```
sudo apt-get update
```

### 安装Vapor

现在你已经添加了Vapor的APT repo，你可以安装需要的依赖了

```
sudo apt-get install swift vapor
```

### 安装校验

双击回车检查安装是否已完成

```
eval "$(curl -sL check.vapor.sh)"
```

### 下一步

想要学习更多关于Vapor Toolbox CLI在[ToolBox章节](https://docs.vapor.codes/2.0/getting-started/toolbox/)在准备开始章节中

### Swift.org

对于安装Swift3.0的更多细节请到[Swift.org](https://swift.org/)获取更多指引

