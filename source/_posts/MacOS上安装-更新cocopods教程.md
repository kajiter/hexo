---
title: MacOS上安装/更新CocoaPods教程
date: 2017-10-01 11:39:58
tags:
cover: https://i.loli.net/2019/12/01/wyu6t85fM9oPia1.png
---
# 版本太低更新教程

```
$ pod --version
1.5.3

$ sudo gem update --system     //先更新Ruby-gem
Password:


$ sudo gem install cocoapods -n /usr/local/bin  //更新cocoapods


$ pod --version
1.8.4

$ pod update --no-repo-update
```
### 首次使用安装教程点击查看
<!--more-->



## ERROR:  While executing gem ... (Gem::FilePermissionError)
You don't have write permissions for the /usr/bin directory.

```
$ sudo gem install cocoapods -n /usr/local/bin
```
---

## 可选项：查看进度
### 1.在执行pod install命令时加上参数--verbose即可在终端详细显示安装信息，看到pod目前正在做什么(其实是在安装第三方库的索引)，确认是否是真的卡住。 
```
pod install 'ThirdPartyName' --verbose
```

### 2.或者进入终端家目录，输入ls -a可看到隐藏的pod文件夹，输入

```
$ cd ~/.cocoapods/
$ du -sh

```
### 即可看到repos文件夹的容量，隔几秒执行一下该命令，可看到repos的容量在不断增大，待容量增大至300+M时，说明，repos文件夹索引目录已安装完毕。此时，pod功能即可正常使用。

---

## 可选项：替换源

```
$ gem sources -l
*** CURRENT SOURCES ***

https://rubygems.org/


$ gem sources --remove https://rubygems.org/
https://rubygems.org/ removed from sources
$ gem sources -a https://gems.ruby-china.com/
https://gems.ruby-china.com/ added to sources


# 查看是否替换源成功
$ gem sources -l
*** CURRENT SOURCES ***

http://gems.ruby-china.com/
```

---
## 可选项：升级 Ruby

```
$ sudo gem update —-system
Password:

```

----


# 安装教程

## 一、查看CocoaPods 的配置情况
```
$ pod --version


command not found: pod
或
1.5.3

```
如果报错则表示本机没有安装 CocoaPods ，进入第二步
如果有版本号提示，责说明本机已经安装过 CocoaPods ,可以直接忽略“安装教程”，跳转查看“更新教程”或最下面的扩展阅读

## 二、检查 Ruby 环境
因为 CocoaPods 的安装是基于 Ruby 的，所以我们要先把 Ruby 环境配置好。

查看 ruby 的源地址、版本号，根据实际情况决定是否替换源或升级版本
```
$ gem sources -l
*** CURRENT SOURCES ***

https://rubygems.org/

$ ruby -v
ruby 2.3.7p456 (2018-03-28 revision 63024) [universal.x86_64-darwin18]
```

根据实际情况选择性操作
- 替换源

```
$ gem sources --remove https://rubygems.org/
https://rubygems.org/ removed from sources

$ gem sources -a https://gems.ruby-china.com/
https://gems.ruby-china.com/ added to sourcesg/


# 查看是否替换源成功
$ gem sources -l
*** CURRENT SOURCES ***

http://gems.ruby-china.com/
```


- 升级 ruby 版本

```
$ sudo gem update -—system
Password:
```
---

## 三、安装 CocoaPods 

```
$ sudo gem install cocoapods 
Password:

# 这里提示让你输入这台电脑的管理员密码
# 提示：在终端输入密码不会有提示，光标也不会移动，这是正常的。
# 只管正常输入，输完按 Enter 键就好。

```
### 之后会经历漫长的等待... 我一般选择打开电影等待

### 安装成功后会提示 ```Successfully installed cocoapods-1.8.4 ``` 大致界面如下，文字肯定不一样，仅供参考
```
$ sudo gem install cocoapods 
Password:


CHANGELOG:  
  
## 1.8.4  
  
##### Bug Fixes  
  
* Fixed the Podfile `default_subspec` attribute in nested subspecs.    
  [Fabio Pelosin][irrationalfab]  
 \ [#2050](https://github.com/CocoaPods/CocoaPods/issues/2050)  
  
  
Successfully installed cocoapods-1.8.4  
Installing ri documentation for cocoapods-1.8.4 
/System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/lib/ruby/1.8/rdoc/rdoc.rb:280: warning: conflicting chdir during another chdir block  
/System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/lib/ruby/1.8/rdoc/rdoc.rb:287: warning: conflicting chdir during another chdir block  
Done installing documentation for cocoapods after 10 seconds  
1 gem installed  

```

## 四、第一次使用
### 用命令行 (cd) 到你需要使用 CocoaPods 管理的 Xcode 工程目录下。
```
$ cd Documents/GitHub/MyProject
$ touch Podfile    //(新建一个名称必须为 Podfile 的文件)

```
### 会用 vim 编辑的使用 vim ，不会用的直接鼠标打开,
### 然后往 Podfile 文件中输入以下内容：
```
# Uncomment the next line to define a global platform for your project
platform :ios, '11.0'
inhibit_all_warnings!

target 'MyProject' do
  # Uncomment the next line if you're using Swift or would like to use dynamic frameworks
  # use_frameworks!

  # Pods for MyProject
  
   pod 'AFNetworking'
   pod 'YYKit'
   pod 'Masonry'
   pod 'MJRefresh'
   pod 'FMDB'
   pod 'SVProgressHUD'

end

```
### 其中要把 ```MyProject``` 替换成你的工程的名称
### ```pod 'AFNetworking'```等 这样的语句就是需要导入的第三方库，根据自己的实际需求添加或更改。


## 五、最后一步——部署

### 第一次部署此 Podfile
```
pod install --verbose --no-repo-update

```

### 更新此 Podfile
```
pod update --verbose --no-repo-update

```

### 然后就可以通过 ```MyProjectName.Xcodeproj ``` 来打开工程查看结果了。
### （注意以后在通过蓝色的 ```MyProjectName.xcworkspace``` 打开运行的话一定会报错的! 这里新手容易犯这个错误。）

# CocoaPods 语句

## 一、使用search命令搜索类库名：
```
$pod search AFNetworking

-> AFNetworking (3.2.1)
A delightful iOS and OS X networking framework.
pod 'AFNetworking', '~> 3.2.1'
- Homepage: https://github.com/AFNetworking/AFNetworking
- Source:   https://github.com/AFNetworking/AFNetworking.git
- Versions: 3.2.1, 3.2.0, 3.1.0, 3.0.4, 3.0.3, 3.0.2, 3.0.1, 3.0.0,
3.0.0-beta.3, 3.0.0-beta.2, 3.0.0-beta.1, 2.7.0, 2.6.3, 2.6.2, 2.6.1, 2.6.0,
2.5.4, 2.5.3, 2.5.2, 2.5.1, 2.5.0, 2.4.1, 2.4.0, 2.3.1, 2.3.0, 2.2.4, 2.2.3,
2.2.2, 2.2.1, 2.2.0, 2.1.0, 2.0.3, 2.0.2, 2.0.1, 2.0.0, 2.0.0-RC3, 2.0.0-RC2,
2.0.0-RC1, 1.3.4, 1.3.3, 1.3.2, 1.3.1, 1.3.0, 1.2.1, 1.2.0, 1.1.0, 1.0.1,
1.0, 1.0RC3, 1.0RC2, 1.0RC1, 0.10.1, 0.10.0, 0.9.2, 0.9.1, 0.9.0, 0.7.0,
0.5.1 [master repo]
- Subspecs:
  - AFNetworking/Serialization (3.2.1)
  - AFNetworking/Security (3.2.1)
  - AFNetworking/Reachability (3.2.1)
  - AFNetworking/NSURLSession (3.2.1)
  - AFNetworking/UIKit (3.2.1)

....
 
```


## 二、快速更新库
```
pod update --verbose --no-repo-update

pod install --verbose --no-repo-update

```





# 扩展阅读
## CocoaPods
![Screen Shot 2019-12-01 at 12.13.10.png](https://i.loli.net/2019/12/01/TLnBEKrklOw2GyD.png)

![image.png](https://i.loli.net/2019/12/01/wyu6t85fM9oPia1.png)

## CocoaPods的核心组件

CocoaPods是用Ruby写的，并划分成了若干个 Ruby-Gem 包。

CocoaPods在解析执行过程中最重要的几个包的路径分别是：
```CocoaPods/CocoaPods```
``` CocoaPods/Core```
```CocoaPods/Xcodeproj``` 

CocoaPods / CocoaPod：这是面向用户的组件，每当执行一个pod命令时，这个组件将被激活。它包括了所有实用CocoaPods的功能，并且还能调用其他gem包来执行任务。 

CocoaPods / Core：Core gem提供了与CocoaPods相关的文件（主要是podfile和podspecs）的处理。 



Podfile：该文件用于配置项目所需要的第三方库，它可以被高度定制。本文中我们主要在这里做动作。

Podspec：该文件描述了一个库将怎样被添加进工程中。.podspec文件可以标识该第三方库所需要的源码文件、依赖库、编译选项，以及其他第三方库需要的配置。 

CocoaPods / Xcodeproj：这个包负责处理工程文件，它能创建以及修改.xcodeproj文件和.xcworkspace文件。
它也可以作为一个独立的包使用，当你要编写修改项目文件的脚本时，可以考虑使用CocoaPods/Xcodeproj。

### 简而言之就是，使用 CocoaPods 管理第三方类库后，必需在 Xcode 中用``` ****.Xcodeproj ``` 打开工程。
### 而对于哪一个/哪些第三方类库的引用，只需要以固定格式写在 ```Podfile```文件中，然后用命令行即可一键配置。

----
