---
title: git使用总结
date: 2019-11-25 16:09:57
tags:
---
## 首次使用 git 或长期未使用 git 导致 ssh 秘钥过期

### 添加ssh钥匙

1.在finder 中 ```command+shift+G``` 查找``` ~/.ssh``` 目录，如果有```id_rsa.pub```文件。则可以直接使用，使用text 打开，从头复制id_rsa.pub里的内容（末尾的邮箱或提示文字不需要），粘贴在GitHub库的-settings-keys下，Title 就是邮箱。

2.如果没有，则需要初始化创建 RSA 文件。在 terminal 中切换到用户目录下，之后运行

```ssh-keygen -t rsa -C "*****@qq.com" //github所使用的的邮箱名```

成功后会生成```id_rsa```和```id_rsa.pub```文件。参考 1. 复制.pub内容到 GitHub setting 里面即可。

3.在 terminal 中切换到合适的代码存放位置。Linux 创建目录（文件夹）语句```mkdir aaa```

<!--more-->

4.```git init ```初始化仓库

下面两句一般网页上有具体的值，可以根据实际情况直接复制使用。

5-1.```git remote add origin git@server-name:path/repo-name.git ``` 关联远程仓库。

一般远程没有内容；本地可能有内容，也可能没内容，简单的关联。

5-2.```git clone git@server-name:path/repo-name.git ```克隆远程仓库。

一般为远程有内容；本地没内容，或本地内容需要被远程内容覆盖掉时，从远程下载下来。


## 一般常用操作
```
git config --local --list   查询当前Git配置

git config user.name

git config user.email 查询当前的 用户名 /邮箱
```

---

```
git branch -a 查看本地+远程的所有分支

git pull --rebase origin master  在远端的基础上拉取最新内容，用于首次 push 不成功的情况
```
---

```
git status  最常用的，查看当前工作区|缓存区

git diff  balabala.text 查看《balabala.text》文件工作区与缓存区的不同地方

git add  balabala.text  把当前工作区的《balabala.text》文件添加到缓存区

git commit -m "每次提交必须带描述"  把当前缓存区的全部内容提交为一个版本

以上两步可以合并，但不推荐(因为它会把更新提交，新增默认不存入缓存区不会被提交)

git commit -m "合并时容易遗忘添加文件，只能下一次提交" -a 把当前“变更”【不包含增加】添加到缓存区并进行提交

//***********push前发现描述文字错误，或修改上次提交的描述文字*************

git commit --amend  查看并修改上一次，且为最近的上一次的提交内容，使用vi修改



git push  把本地仓库推送到远程仓库

git log --pretty=oneline  打印所有历史操作，可以快捷查看每个操作的缩略码

git reflog 打印所有的命令记录（主要是从未来回到过去后，用log无法找到未来的id）

git reset --hard  (6位id值)  回退到某一ID对应的版本（既可以是过去，也可以是未来）

git rm bala.text  删除缓存区内的《 bala.text》文件

git checkout -- bala.text  用缓存区的《bala.text 》文件替换工作区对应《bala.text 》文件的内容。
```
- 就这一点来看，可以有“删除当前内容”和“回退之前内容”两种结果。未add时，删除当前工作区的内容很容易理解;回退 的话要与  ```git reset --hard ``` (过去正确的版本id) 联合使用，先回退版本，再checkout该文件，就回退到了该文件还存在的时刻。


## 与分支相关的操作
### 分支间切换

```
git checkout -b  newBranch-001 等于下两句

git branch newBranch-001  新建一个名叫《newBranch-001》的分支
git checkout  newBranch-001  当前分支切换至《newBranch-001》分支


git branch  查看所有的分支（同时当前所在的分支会被加*号表示 ）
git checkout  aBranch-002 切换分支

```
### 合并分支（特别是往 master 分支上合并新开发完成的 issue ）
>合并分支需要确定一个概念:
主分支用【master】表示； 次要分支用【Issue】表示
>>把Issue合并到master之中， 必须   首先把当前分支切换至目标分支，即master之上

```
git merge Issue-001  把《Issue-001》分支内容合并到当前分支之中

git branch -d Issue-001 删除《Issue-001》分支

git branch -r -d Issue-001 删除《origin/Issue-001》远程分支
```
### 合并时常常需要解决冲突

可以使用vim 直接操作，（Vim 语法传送门）也可以点击进入文件手动更改。

```vi a.rtf ```


在需要的地方 ```dd ```（删除）

最后 ``` :wq ```(保存并退出)

 然后就可以顺利的重新提交 ```add  commit ```了
 

 ### 合并操作人为出错或强行合并操作

```
git log --graph --pretty=oneline --abbrev-commit 以缩略图形式，展示分支合并信息


/*  把本地分支嫁接到某一远端分支节点 
git fetch

git reset --hard origin/isuue-100 

```
---
## 最后记录一下版本合并的原则。

```Origin ```远端仓库，不解释

```Master ``` 权高位重，可以认为是“成熟版本”的记录者，它的每一次节点的更替，都意味着一个“经得起线上检验的”版本。面向版本，而不是面向功能。

```Develop ``` 战线最长，面向功能。可以认为是“完整新功能”的记录者，它的每一次节点更替，意味着一个“完整的功能”。一个版本可以有若干新旧功能。

```Future ``` 一般用于打某几个功能的较完整的测试包。比如开发周期为两周，第一周只完成ABC三个功能，D功能完成一半，就先把ABC merge 到Future中，查看整体效果，或用于展示。最终Future将在功能测试后销毁，不建议合并至Develop中！

```Issue``` 分支，面向功能模块，(或者说面向文件，尽可能只修改某一功能所涉及的某几个文件，尽量避免因不同的Issue修改同一文件而造成的合并冲突)可能包含一个或多个近似功能实现。需要就开辟，弃用即销毁，完成就rebase merge 到Develop中，实现 “某一功能开发完成”，或“针对性修改某一单一功能”的目的。
