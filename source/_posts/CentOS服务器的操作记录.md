---
title: CentOS服务器的操作记录
date: 2019-12-02 10:22:07
tags:
cover: 
---
## 1.网络教程

[CentOS 服务器（带 GUI 图形界面）的安装教程](http://baijiahao.baidu.com/s?id=1599601257937774752&wfr=spider&for=pc)

[CentOS 各版本163.com 镜像下载](http://mirrors.163.com/centos/7/isos/x86_64/) 支持迅雷等种子下载

[配置开机自启项](https://jingyan.baidu.com/article/ed15cb1b571a631be36981c4.html)

促使我下定决心安装 CentOS 的两个教程：

[充分利用服务器闲置资源，搭建成私有网盘](https://www.jianshu.com/p/63b29135c041)

[闲置电脑搭建为云服务器(Holer开源框架)](https://blog.csdn.net/qq_41098163/article/details/100568932) 内网穿透=从外网可访问



<!--more-->


## 出现 ssh 链接警告时的解决办法
### 前提是我清楚知道是我自己重新载入的 Linux 系统导致的证书不一致，并不是网络攻击导致的证书错误。

```
➜  ~ ssh root@192.168.0.103
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:5DImiWgSYapc1LhSsvBmctGHwXmtwIGJTJjfhWCMQxc.
Please contact your system administrator.
Add correct host key in /Users/CL/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /Users/CL/.ssh/known_hosts:7
ECDSA host key for 192.168.0.103 has changed and you have requested strict checking.
Host key verification failed.

➜  ~ ssh-keygen -R 192.168.0.103
# Host 192.168.0.103 found: line 7
/Users/CL/.ssh/known_hosts updated.
Original contents retained as /Users/CL/.ssh/known_hosts.old

➜  ~ ssh root@192.168.0.103
The authenticity of host '192.168.0.103 (192.168.0.103)' can't be established.
ECDSA key fingerprint is SHA256:5DImiWgSYapc1LhSsvBmctGHwXmtwIGJTJjfhWCMQxc.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.103' (ECDSA) to the list of known hosts.
root@192.168.0.103's password:

```



```


```


----
