---
title: Mac下创建CentOS的U盘引导文件
date: 2019-12-02 00:52:59
tags:
cover: https://i.loli.net/2019/12/02/QIUPXgnoJqW9a81.jpg
---
# 想搞个服务器玩玩，于是就在淘汰的旧电脑上装上了 CentOS


<!--more-->

## 第一步格式化你的 U盘，注意给你 U盘起一个简单（不能超过 8 个字符！！！）（不要用汉字！！！）特殊的名称（不要简单叫作 C、D、E 之类的）
# 上面三个括号的忠告不遵循的话都会伴随着说大不大、说小不小的坑，君请自便。


## 核心代码
```
➜  ~ diskutil list
/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *251.0 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:                 Apple_APFS Container disk1         171.8 GB   disk0s2
   3:       Microsoft Basic Data                         79.0 GB    disk0s3

/dev/disk1 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +171.8 GB   disk1
                                 Physical Store disk0s2
   1:                APFS Volume Macintosh HD            129.2 GB   disk1s1
   2:                APFS Volume Preboot                 46.2 MB    disk1s2
   3:                APFS Volume Recovery                510.5 MB   disk1s3
   4:                APFS Volume VM                      1.1 GB     disk1s4

/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *7.8 GB     disk2
   1:                 DOS_FAT_32 CL                      7.8 GB     disk2s1




➜  ~ diskutil unmountDisk /dev/disk2
Unmount of all volumes on disk2 was successful


➜  ~ sudo dd if=/Users/CL/Desktop/CentOS-7-x86_64-Minimal-1908.iso of=/dev/disk2 bs=1m
Password:
942+0 records in
942+0 records out
987758592 bytes transferred in 543.310278 secs (1818038 bytes/sec)


```
### 注释：
diskutil list ：查看本机上所有磁盘
-    /dev/disk0 为我的 MacOS 主系统盘
-    /dev/disk1 为我安装的 Windows 双系统
-    /dev/disk2 为我的 U盘，NAME 就叫做 CL

所以我 unmount 的是我的 /dev/disk2 ，要根据实际情况决定

最后一句命令会运行很长时间，这是正常情况！！！不要轻易中断。根据网络以及自己的经验，执行这句代码需要 8-12 分钟左右。请起身运动，或者多喝热水。

```
942+0 records in
942+0 records out
987758592 bytes transferred in 543.310278 secs (1818038 bytes/sec)
```
这些就是成功提示，同时你的电脑会弹窗提示不识别你的 U盘，这也是正常情况，根据提示弹出 U盘即可。你的 U盘并没有损坏！！！

# 最后，再给你看一眼我的鞋盒 Linux 服务器

![IMG_7979.jpg](https://i.loli.net/2019/12/02/QIUPXgnoJqW9a81.jpg)

---


