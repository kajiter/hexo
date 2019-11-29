---
title: 网络唤醒你的Windows复机
date: 2019-11-29 16:32:06
tags:
cover:
---

## 本文采用演示示例为：
### 1.主工作机 MacBookPro 
### 2.复机 微星B450+Windows10
### 3.网络条件：同一路由器下，即同一个网络。
### 4.MacOS 下软件名：wakeonlan （Linux 插件）
### 5.Windows 下软件名：Wake on Lan Monitor  (主要用于测通，用完即删)


<!--more-->

“远程控制” 这一操作对我们来说都不陌生，从当年的 QQ 远程控制，到后来的微信视频“远程”帮教父母解决各种这样的软件问题，我一直想找出一个最简洁高效的方案，向日葵控制端 之类的商业软件仍避免不了物理开机的问题，所说也有“花生棒”之类的物理配件，但是特别是对于2000 年之后的PC，主板网卡自带网络唤醒功能，而我们要做的就是攻克远程唤醒这最后一个障碍。

## 一、确认被控制计算机硬件上支持网络唤醒

硬件上实现网络开机，需要主板、网卡、电源 3 个设备支持。首先需要查看主板是否支持 Wake-Up OnInternal Modem（WOM）或者 Wake-up OnLAN（WOL）技术，如果支持就说明主板支持远程开机。
能否实现远程唤醒，其中最主要的一个部件就是网卡，一般来说 2000 年以后的主板均支持，更不用说最近两年的新机型。但如果你对你的主板没有信心，那么一定要进 BIOS 里进行检查，或上网搜索自己的主板相关的  Wakeup On Lan(WOL)信息。

### 这里以最流行的 微星 B450m -迫击炮 为例，开启主板Wakeup On Lan(WOL) 功能。

 ```高级``` -> 
    ```唤醒事件设置``` ->
        ```将 PCIE设备唤醒``` 和 ```网络唤醒``` 设置为 ```允许 (Enable)```
        
----
### 注：不同的机型差异较大，需要自行在互联网搜集自己型号主板 BIOS 的开启Wakeup On Lan(WOL) 功能。
---

## 二、Windows系统设置

这里给出[Intel的网卡设置教程](https://www.jianshu.com/p/d89b5560c3ed)

然而我的AMD 主板并不需要这么复杂，网卡不需要做出设置。

需要做的是获取此电脑的 ip 地址，和物理 MAC 地址。记在小本本上。

小白的话是打开路由器查看：
不同路由器界面不一，但原理相通。
![Screen Shot 2019-11-29 at 16.40.47.png](https://i.loli.net/2019/11/29/wGH7YtIJKDNaX3C.png)


有 Linux 基础的同学，自然是进命令行查看，这里提示下非 Windows 用户可以在 win10 中搜索使用 “Windows PowerShell” ，这个要比 cmd 更 Linux 一点点。
```
$ ipconfig

```

---

## 三、Windows 安装测试接受软件

软件名：Wake on Lan Monitor  (主要用于测试通接受到唤醒 UDP，测试成功后即可删除)

### [官方下载链接](https://www.depicus.com/wake-on-lan/wake-on-lan-monitor)

### 安装后点击 start ，即进入测试等待状态。

---
## 四、MacOS 安装 wakeonlan 包

```
➜  ~ brew install wakeonlan

```
安装成功后，使用代码启动，发送 wakeup 的 UDP
注意-p 4343 这个端口号是 Windows 上 Wake on Lan Monitor 的测试端口，实际使用时不需要加端口号。

### 此处的 ```MAC 地址``` 即为第二步 Windows 下查看到的 MAC地址 ，这里用```00:D8:61:71:FF:97``` 表示

```
➜  ~ wakeonlan -p 4343  00:D8:61:71:FF:97
Sending magic packet to 255.255.255.255:4343 with 00:D8:61:71:FF:97
```

### 这时如果你发现 Windows 中的 Wake on Lan Monitor 软件中k开始打印数据，即表示一切配置成功，你终于可以实现一行代码网络唤醒另一台主机了！

### 如果你Windows 中的Wake on Lan Monitor毫无反应，则表示你哪一步做错了，返回好好检查一下吧。




## 五、实际使用
把你的 Windows 关机后，在 Mac 中输入

```
➜  ~ wakeonlan  你记下的MAC地址
Sending magic packet to 255.255.255.255:9 with 00:**:61:71:FF:97

```

# 铛铛铛铛~~  大功告成！


---

这里特意截出来 wakeonlan 的安装信息，18KB真的小。

```
➜  ~ brew install wakeonlan

==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/wakeonlan-0
######################################################################## 100.0%
==> Pouring wakeonlan-0.41.mojave.bottle.tar.gz
🍺  /usr/local/Cellar/wakeonlan/0.41: 6 files, 18.6KB

```
---
---
---
---
---

# 扩展和补充知识点


## MacBookPro 上控制 Windows 的官方软件
### [Microsoft Remote Desktop for Mac](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/Microsoft-Remote-Desktop-for-Mac/distribution_groups/All-users-of-Microsoft-Remote-Desktop-for-Mac)

### [microsoft 官方使用文档](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-mac)


---

# 一些题外话，留作记录
## 设置 Windows 远程桌面


### Windows 设置允许远程连接
![851575021625_.pic_hd.jpg](https://i.loli.net/2019/11/29/KJ84unm3rdylezv.png)

![861575021758_.pic_hd.jpg](https://i.loli.net/2019/11/29/Cuf1cLPwhx8UT6t.png)

---

## 设置 Windows 访问局域网共享文档

![871575021914_.pic_hd.jpg](https://i.loli.net/2019/11/29/sdrVHZgb1hEa3p2.png)

首次进入需要设置游客账号密码，这里没有截图
![881575021948_.pic_hd.jpg](https://i.loli.net/2019/11/29/UBSOgPxvATrJcXM.png)
