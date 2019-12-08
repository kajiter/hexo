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


## 链接远程服务器

### ssh root@192.168.0.103

---

## 在终端断开ssh连接而不关闭终端的方法：

### 法1：Ctrl+D
### 法2：输入 logout


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

## 查看安装过的 CentOS 是 32 位机还是 64 位机

```
# echo $HOSTTYPE
x86_64      # 为64位

```



## yum（全称为 Yellow dog Updater, Modified）是一个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。


```
yum常用命令
安装软件(以foo-x.x.x.rpm为例）：yum install foo-x.x.x.rpm

删除软件：yum remove foo-x.x.x.rpm或者yum erase foo-x.x.x.rpm
升级软件：yum upgrade foo或者yum update foo
查询信息：yum info foo
搜索软件（以包含foo字段为例）：yum search foo
显示软件包依赖关系：yum deplist foo


upgrade 升级系统
update[RPM包] 更新包
search[关键词] 搜索包
list 可安装和可更新的RPM包
list installed 已安装的包
check-update 检查可更新的包


remove[RPM包] 卸载包
clean all 清除全部
clean packages 清除临时包文件（/var/cache/yum 下文件）
clean headers 清除rpm头文件
clean oldheaders 清除旧的rpm头文件

deplist 列出包的依赖

provides[关键词] 搜索特定包文件名
reinstall[RPM包] 重新安装包
repolist 显示资源库的配置
resolvedep 指定依赖

```

## wget是一个下载文件的工具，它用在命令行下。对于Linux用户是必不可少的工具，我们经常要下载一些软件或从远程服务器恢复备份到本地服务器。

wget支持HTTP，HTTPS和FTP协议，可以使用HTTP代理。所谓的自动下载是指，wget可以在用户退出系统的之后在后台执行。这意味这你可以登录系统，启动一个wget下载任务，然后退出系统，wget将在后台执行直到任务完成

 wget 可以跟踪HTML页面上的链接依次下载来创建远程服务器的本地版本，完全重建原始站点的目录结构。这又常被称作”递归下载”。

 wget 非常稳定，它在带宽很窄的情况下和不稳定网络中有很强的适应性.如果是由于网络的原因下载失败，wget会不断的尝试，直到整个文件下载完毕。如果是服务器打断下载过程，它会再次联到服务器上从停止的地方继续下载。这对从那些限定了链接时间的服务器上下载大文件非常有用
 
 ### 常用的命令展示
```
使用wget -O下载并以不同的文件名保存(-O：下载文件到对应目录，并且修改文件名称)
wget -O wordpress.zip http://www.minjieren.com/download.aspx?id=1080


使用wget -b url     进行后台下载
wget -b http://www.minjieren.com/wordpress-3.1-zh_CN.zip

备注： 你可以cd到下载目录，然后使用以下命令来察看下载进度：
$ tail -f wget-log
    并且可以 control + c 随时切出，进行后台下载


利用-spider: 模拟下载，不会下载，只是会检查是否网站是否好着
# wget --spider  www.baidu.com    #不下载任何文件

```


## 通用文件操作命令
```
文件的复制 - cp
移动 - mv (也可以做到文件重命名)
删除 - rm 

 cp path1/file1 path/file2
 mv ~/path/name1 /cl/docu/name2
 
 rm path/file
 删除时会默认询问是否确认，输入 y 即可。
 rm -r path
 删除某个目录，包括目录下的所有文件
 也可以选择强制删除语句
 rm -f path/file




简单查看文件内容(不进行编辑或修改)
cat path/file

查看文件权限
ls -al

查看空间使用情况
df -h


创建软连接，命令如下：
ln -s /源地址 /目标地址

ln的链接分软链接和硬链接两种：
1、软链接就是：“ln –s 源文件 目标文件”，
只会在选定的位置上生成一个文件的镜像，不会占用磁盘空间，类似与windows的快捷方式。

2、硬链接ln源文件目标文件，没有参数-s， 会在选定的位置上生成一个和源文件大小相同的文件，无论是软链接还是硬链接，文件都保持同步变化。

```

## 常用的 yum 工具包

```
yun install zip  
yun install -y unzip
#yum install xxx 如果安装的软件有询问会卡在询问页，如果希望安装过程自己很清楚的可以使用此命令；
#如果希加 -y 默认在下载过程中对所有的询问进行 yes 操作.


```



### netstat命令用于显示与IP、TCP、UDP和ICMP协议相关的统计数据，一般用于检验本机各端口的网络连接情况。netstat是在内核中访问网络及相关信息的程序，它能提供TCP连接，TCP和UDP监听，进程内存管理的相关报告。

```

yum -y install net-tools

显示网卡列表
netstat –i

显示组播组的关系
netstat –g

显示网络统计
netstat -s


常用组合：
netstat -lntup  
说明： l:listening   n:num   t:tcp  u:udp  p:process


显示关于以太网的统计数据
netstat –e
说明：用于显示关于以太网的统计数据。它列出的项目包括传送的数据报的总字节数、错误数、删除数、数据报的数量和广播的数量。这些统计数据既有发送的数据报数量，也有接收的数据报数量。这个选项可以用来统计一些基本的网络流量）


显示路由信息
netstat –r
route –n   【也可以显示路由信息】

找出程序运行的端口
netstat -ap | grep ssh

在 netstat 输出中显示 TCP连接信息
netstat -pt




```

## 查看 CentOS/ RedHat 版本号
```
# cat /etc/redhat-release
CentOS Linux release 7.7.1908 (Core)

```

## 查看 Linux 内核版本号
```
[root@localhost ~]# uname
Linux
[root@localhost ~]# uname -r
3.10.0-1062.el7.x86_64
[root@localhost ~]# uname -a
Linux localhost.localdomain 3.10.0-1062.el7.x86_64 #1 SMP Wed Aug 7 18:08:02 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux

```

## 安装 Xampp 教程

```
#开启xampp，命令为：
sudo/opt/lampp/xampp start


#停止xampp，命令为：
sudo/opt/lampp/xampp stop

```

### [https://www.cnblogs.com/wanghuaijun/p/5476435.html](https://www.cnblogs.com/wanghuaijun/p/5476435.html)  这个教程比较清晰，但也比较老了。如果安装的是新一点版本的话还会遇到开启 CentOS 端口防火墙的问题。下面是解决思路

## 开启 CentOS 某个端口 如：80 端口
CentOS7中，默认会开启 firewall 防火墙，只暴露一个 22 端口。
```
1.需要工具包查看端口使用情况
# netstat
-bash: netstat: 未找到命令
# yum install -y net-tools

···
#
2.显示出当前主机打开的所有端口
# netstat -tlunp
···
-A IN_public_allow -p tcp -m tcp --dport 22 -m conntrack --ctstate NEW,UNTRACKED -j ACCEPT
COMMIT
#检查 80 端口是否开放

3.查看防火墙设置
# iptables-save
···
#如果没后几行没有提示 80 端口打开的语句，则需要手动开放防火墙保护的端口

4.手动开放防火墙保护的80端口：第一条命令是添加端口，第二条命令是重载防火墙。
# firewall-cmd --zone=public --add-port=80/tcp --permanent
# firewall-cmd --reload

5.再次检查防火墙设置
# iptables-save
···
-A IN_public_allow -p tcp -m tcp --dport 22 -m conntrack --ctstate NEW,UNTRACKED -j ACCEPT
-A IN_public_allow -p tcp -m tcp --dport 80 -m conntrack --ctstate NEW,UNTRACKED -j ACCEPT
COMMIT
#最后出现 80 即表示成功！


```

## nginx 服务
```
启动服务
$ /usr/local/nginx/sbin/nginx
重新加载服务
$ /usr/local/nginx/sbin/nginx -s reload
停止服务
$ /usr/local/nginx/sbin/nginx -s stop
查看nginx服务进程
$ ps -ef | grep nginx # 查看服务进程

```

## 使用 systemctl 设置开机自启动某服务

[https://blog.csdn.net/niufenger/article/details/94648199](https://blog.csdn.net/niufenger/article/details/94648199)

```
1.登录系统后，切换到以下目录
cd /lib/systemd/system/

2.在此目录下，新建一个lampp.service。

3.vi /lib/systemd/system/lampp.service
文件内容如下

-------------


[Unit]
Description=lampp
After=network.target
   
[Service]
Type=forking
ExecStart=/opt/lampp/lampp start
ExecReload=/opt/lampp/lampp restart
ExecStop=/opt/lampp/lampp  stop
PrivateTmp=true  
   
[Install]
WantedBy=multi-user.target


---------------
###   解释   ###
[Unit]:服务的说明
Description:描述服务
After:描述服务类别
[Service]服务运行参数的设置
Type=forking是后台运行的形式
ExecStart为服务的具体运行命令
ExecReload为重启命令
ExecStop为停止命令
PrivateTmp=True表示给服务分配独立的临时空间
注意：[Service]的启动、重启、停止命令全部要求使用绝对路径
[Install]服务安装的相关设置，可设置为多用户

4.编辑好了，就保存退出。用下面的命令来修改文件权限。
chmod 754 /lib/systemd/system/lampp.service

5.设置开机启动
systemctl enable lampp.service


6.扩展操作

启动lampp服务
systemctl start lampp.service


设置开机自启动
systemctl enable lampp.service


停止开机自启动
systemctl disable lampp.service


查看服务当前状态
systemctl status lampp.service


重新启动服务
systemctl restart lampp.service


查看所有已启动的服务
systemctl list-units --type=service

```
### 结束

### [脚本方式，未验证](https://blog.csdn.net/niufenger/article/details/94648199)



----
