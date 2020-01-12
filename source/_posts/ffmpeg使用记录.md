---
title: ffmpeg使用记录
date: 2019-12-16 22:49:50
tags:
cover:
---

## ffmpeg语法：
```
// 改后缀名
ffmpeg -i aaa.avi newName.mp4

// 视频截取 注意-to 后的时间参数为从初始值开始截取多少时间
ffmpeg -ss 00:11:05 -i old.mp4 -to 00:01:50 new.mp4
# 解释：从视频 old.mp4的第11分05秒开始，截取1分05秒的视频，并命名为new.mp4


// -y 参数含义导出文件时，如果发现路径下已有该命名的文件，则强制覆盖。
ffmpeg -y *****


```


---
<!--more-->
----


---
