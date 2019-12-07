---
title: Markdown
date: 2019-11-27 13:39:36
tags:
cover: https://i.loli.net/2019/11/28/ZnYCwlHD1x4AzGF.jpg
---

>### Markdown 就是 Mark（标记后）down (写下来)，就是所记即所得。
>### Markdown 是通过字符来约束内容的，但是它是整行约束,即换行不继承

<!--more-->

---
## “#”的个数表示1-6级标题：
\#一级标题
\###三级标题

# 一级标题
### 三级标题

---

## **      **表示加粗文字
普通的文字
\*\*加粗的文字\*\*
**加粗的文字**

## *        *表示倾斜文字
\*这是一段斜体字\*
*这是一段斜体字*


## \~~   \~~表示删除文字
\~\~删除线\~\~  与文字间不能有空格
~~aaa~~

---

## --- 或 *** 表示分割线

>---

---
## ">"表示引用，引用内可以嵌套引用

\>这是一个引用
这是引用的结尾
\>>这是一个二级引用

>这是一个引用
这是引用的结尾
>>这是一个二级引用


---
## \```   #import std.io   \```  三个点组圈出来的为代码块
### 注意 " ` " 与 " ' " 不同，位置在键盘中数字键“1”的左边，不是引号！

单行```高亮```显示，多行格式化代码：
\```
\#import a.h
if (a > 3) {
printf("yes");
}
\```
```
#import a.h
if (a > 3) {
printf("yes"); //代码注解
}
```

-------
## " - " 表示无序序列

\- 第一天
下海捉鱼
\- 第二天
上岛撒欢
- 第一天
下海捉鱼
- 第二天
上岛撒欢

---
## “1.2.3. 等”表示有序序列

1. 吃海鲜
2. 睡帐篷
3. 打豆豆
4. 开飞机
-  开啤酒
5. 打豆豆

---
## <> 表示网址
<1260807001@qq.com(邮箱地址)  >
 <1260807001@qq.com>


---

## 插入图片

\!\[图片叫什么\]\(图片的网址)

![图片叫什么，网址为：http://iconfont.alicdn.com/t/1512879992270.jpg@200h_200w.jpg](http://upload-images.jianshu.io/upload_images/2517476-5c6e85898cc83f30.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

## 加文字超链接

\[这是一个带超链接的文字\]\(https://www.baidu.com/)

[这是一个带超链接的文字,点击即跳转https://www.baidu.com/](https://www.baidu.com/)

---

## 化学式不同平台支持不一，仅做参考

化学价或平方的写法 = Sad\^2\^ + H\~2\~O
#### 此处不支持 化学价或平方的写法 = Sad^2^ + H~2~O
其中“-”减号要注意最好转译 7 \- 4 = 3    
 #### 此处不支持 7 - 4 = 3

---

## 流程图不同平台支持不一，仅做参考

```
```flow 
st=>start: 开始 
op=>operation: My Operation 
cond=>condition: Yes or No? 
e=>end 
st->op->cond 
cond(yes)->e 
cond(no)->op 
&```

```


----
### 最后放一个[不太全的注解^_^](https://upload-images.jianshu.io/upload_images/7505161-d574f0af224b7df7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/551)
----

