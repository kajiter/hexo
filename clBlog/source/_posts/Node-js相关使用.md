---
title: Node.js相关使用
date: 2019-11-27 17:49:47
tags:
---
## Node.js 是一个基于 Chrome v8 引擎的 JavaScript 运行环境。npm是 Node.js 自带的包管理工具

<!--more-->

这里可以类比联想 JAVA 运行环境：一个 JAVA 程序在运行时，必须需要在 JRE(JAVA Running Environment) 环境下运行；同时，JAVA 程序在开发时，除了种类繁多的 IDE(Integrated Development Environment) (我们平时称为：开发工具，一般包括 代码编辑器、编译器、调试器、图形用户界面、等)以外，还需要 JVM (JAVA Virtual Machine) JAVA 虚拟机 以及 JDK(JAVA Development Kit)JAVA语言软件开发工具包的 JAVA 标准类库部分 等。

（实际上 JDK 是 JAVA开发的核心，它包含了JVM + JAVA 类库+ JAVA 工具，这里把JVM 单独拿出来是因为JVM 是其中非常重要的一个部件）

Node.js 使 JavaScript 语言可以运行在服务端，使用事件驱动，非阻塞 I/O模型。它轻量级和高效的特性使得它非常适合在分布式设备上运行数据密集型的实时应用。


## npm是 Node.js 自带的包管理工具。(Node Package Manager)

---

### npm 的常用方法
### 查看是否安装及版本号
```
➜  ~ node -v
v10.10.0
➜  ~ npm -v
6.13.1
```

### 更新
```
npm update
```

### 安装package
```
npm install <package>     # 安装在本地项目中 
npm install -g <package>  # 安装在全局  

// 安装包，并且将其保存你项目中的 package.json 文件: 

npm install <package> --save  

```
### 查看安装的 package
```
$ npm list     # 本地
$ npm list -g  # 全局  
```

### 对 package 的操作
```
/*查看版本较低的包（本地或全局）:
$ npm outdated [-g]  

/*更新全部或特别指定一个包:
$ npm update [<package>]  

/*卸载包:
$ npm uninstall <package>  
```

### 查看源地址
```
➜  ~ npm config get registry
https://registry.npm.taobao.org/
```
### 更换源/镜像 地址
```
#国内被墙，就切换成淘宝源
npm config set registry https://registry.npm.taobao.org




# 默认源
npm config set registry https://registry.npmjs.org

```

## Node.js 的安装

### MacOS 下使用 Homebrew 安装
```
brew install node 
```

---

#### 关于 Homebrew 的安装参考[MacOS安装 Homebrew](https://kajiter.github.io/)

---
