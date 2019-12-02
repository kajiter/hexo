---
title: CentOS服务器的操作记录
date: 2019-12-02 10:22:07
tags:
cover: 
---

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
