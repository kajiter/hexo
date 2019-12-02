---
title: 捷波X-BlueP43主板BIOS设置记录
date: 2019-12-02 21:48:01
tags:
cover: 
---
# 这是一个十多年前奇葩的主板，让我无数次的掉进深沟的老主板，必须记录下来 


## 开机按 Del 进入 BIOS


<!--more-->

## 配置 U盘引导系统异常麻烦
### 1.选择主板整合设备设置 ，第四项“Integrated Peripherals”
![image.png](https://i.loli.net/2019/12/02/tjH5XnGg4NQqVuZ.png)

---
### 2.进入菜单之后选择第二项“Onboard Device Function”
![image.png](https://i.loli.net/2019/12/02/x4iErJ5Vd8ZqzcM.png)

---
### 3.一定要把图中高亮部最后一项，分支持U盘设备，“USB Storage Legacy Support”设置为Enabled ;
- ### 同时也可以把除了第二项“ Onboard PCIE Lan BootRom”保持 Disabled以外，其他所有项均设置为 Enabled 。
- ### 设置成功后 *“保存退出并重新启动”(F10)* ，
- ### 然后再重新回到这个页面，检查能否在最后一行识别出我们插上的 U盘。 

![image.png](https://i.loli.net/2019/12/02/atdS43pg6mIG9Qi.png)

↑如图，最后一行就已经识别出 U盘了。

----
### 4. 按两次ESC ，回到BIOS主菜单，选择第二项“Advanced BIOS Setup”，进入高级系统设置

![image.png](https://i.loli.net/2019/12/02/EAmSHU51raKkzpn.png)

### 提示：启动时想要关闭硬件检测（这里指鼠标，键盘不需要连接也希望能够正常启动），需要进入第一项“Standard CMOS Features” -> 找到“Halt On” -> 设置为“No Errors” 即可。

----
### 5.选择进入第三项“Hard Disk Boot Priority”，手动设置硬盘启动顺序

![image.png](https://i.loli.net/2019/12/02/N8VHQRpXrZAGOk4.png)


### ps: 本页面虽然有“First Boot Device”之类的，但是经试验发现没什么卵用。但最后还是进去设置一下第一启动项设为 USB-FDD ，第二启动项设为 SATA硬盘。
### 提示：“Boot Up Floppy Seek” 为启动时检查软盘，建议设为 Disabled ，否则每次启动均会卡在设备检查界面，必须手动按 F1才会进一步启动 BIOS。

----


### 6.此时应该出现我们的 USB 设备了，根据屏幕下方的提示，光标移动到此 USB 设备上，然后按键盘“Page UP”按钮，把 USB 启动项提升为第一启动项。保存退出并重启即可进入 U盘引导。

- ### 如果此处没有出现我们的 USB 设备，则需要检查第 3 步。 

![image.png](https://i.loli.net/2019/12/02/sz4Pi5Hf2yBD3hl.png)



----





---
