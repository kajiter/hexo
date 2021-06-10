---
title: Node.js相关使用
date: 2019-11-27 17:49:47
tags:
cover: https://i.loli.net/2019/11/28/Kl7LfH1ItNCW8Jv.png
---
## Node.js 是一个基于 Chrome v8 引擎的 JavaScript 运行环境。npm是 Node.js 自带的包管理工具

<!--more-->

这里可以类比联想 JAVA 运行环境：一个 JAVA 程序在运行时，必须需要在 JRE(JAVA Running Environment) 环境下运行；同时，JAVA 程序在开发时，除了种类繁多的 IDE(Integrated Development Environment) (我们平时称为：开发工具，一般包括 代码编辑器、编译器、调试器、图形用户界面、等)以外，还需要 JVM (JAVA Virtual Machine) JAVA 虚拟机 以及 JDK(JAVA Development Kit)JAVA语言软件开发工具包的 JAVA 标准类库部分 等。

（实际上 JDK 是 JAVA开发的核心，它包含了JVM + JAVA 类库+ JAVA 工具，这里把JVM 单独拿出来是因为JVM 是其中非常重要的一个部件）

Node.js 使 JavaScript 语言可以运行在服务端，使用事件驱动，非阻塞 I/O模型。它轻量级和高效的特性使得它非常适合在分布式设备上运行数据密集型的实时应用。

![node.jpg](https://i.loli.net/2019/11/28/Kl7LfH1ItNCW8Jv.png)

## npm是 Node.js 自带的包管理工具。(Node Package Manager)

---

### npm 的常用方法
### 查看是否安装及版本号
```
node -v
v10.10.0

npm -v
6.13.1
```

### 更新npm
```
npm update
```
或
```
sudo npm install -g npm
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
npm config get registry
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

## node 的更新
```
第一步，先查看本机node.js版本：
node -v

第二步，清除node.js的cache：
sudo npm cache clean -f

第三步，安装 n 工具，这个工具是专门用来管理node.js版本的，别怀疑这个工具的名字，是他是他就是他，他的名字就是 "n"
sudo npm install -g n

第四步，安装稳定版本的node.js
sudo n stable

第五步，再次查看本机的node.js版本：
node -v

第六步，顺带更新npm到最新版
sudo npm install -g npm

第七步，验证node 和 npm 都已更新好
node -v

npm -v

```
## node 版本切换
需要用到上一步介绍过的npm中的包——n。
```
查看n包是否正常
n -V
2.1.12

列出所有node版本
$ n ls

安装某个版本node
$ n xx.xx.x (xx.xx.x 为要安装的版本号)
## 本机hexo所使用的的 node 为 12.20.1 版本

安装最新版本node
$ n lastest

安装最新稳定版node
$ n stable

切换node版本(输入命令后上下键盘选择确认,不推荐！)
$ n

删除某个版本node
$ n rm xx.xx.x

使用某个node版本来运行脚本
$ n use xx.xx.x a.js


```

## node 命令行的退出命令，输入```.exit``` ，别忘了"."

---

#### 关于 Homebrew 的安装参考[MacOS安装 Homebrew](https://kajiter.github.io/)

---
