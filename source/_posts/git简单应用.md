---
title: git简单应用
date: 2016-06-21 14:18:26
tags: [git,js]
comments: true
---

一些git的简单应用入门

<!--more-->


1.安装git
===============
安装地址为[https://git-scm.com/download/](https://git-scm.com/download/)

2.基本配置
===============
1.配置自己的用户名密码
------------------
```
git config --global user.name "junyu-node";
git config --global user.email "1161976385@qq.com";


```
2.可以查看已有的配置信息

```
git config --list

```
3.基本操作
===========


3.1新建一个仓库
--------------
```
    git init
    //如果已经有了一个仓库 直接clone到本地即可
    git clone (git地址)
```

3.2 讲文件添加到缓存
-----------------

```
//添加一个文件
git add README.md
//添加所有的文件
git add -A
//或者
git add *

```
3.3查看当前版本库各个文件的状态
---------------
```
git status
```

3.4将缓冲区的内容添加到仓库
---------
```
git commit -m"注释"
```
3.5取消已经缓存的文件
--------------
```
git reset HEAD --hello.php
//如果粗暴些
git reset --bard 版本号
// 删除某个文件并且从git的仓库移除
git rm 文件
```

3.6设置别名
----------
设置别名的好处就是方便写命令

```
 git config --golbal alias.st status
 git config --golbal alias.ci commit
 git config --golbal alias.co checkout
 git config --golbal alias.br btanch

```

4 push到服务器上
=================

```
//你可以为这个仓库设置一个远程地址
git remote add origin git地址
//origin 为别名
git push origin master//(master为分支名称)
```
如果不想每次上传都输入密码可以在本地生成一个key 配置在github上
```
ssh-keygen -t -rse -C "1161976385@qq.com"

```

复制key
```
cat ~/ssh_rea.pub

```
然后在github的账户 点击头像-> settiings ->SSH KEYS ->ADD KEYS

5.分支
=============

5.1创建分支

-----------

```
git branch mybranch(分支名字)

```
5.2切换分支
--------------
```
git checkout mybranch


// 创建并且切换到该分支上
git checkout -b mybranch
```
5.3删除分支
----------
```
git branch -d mybranch

```
5.4 push到远程仓库
-----------
```
git push origin mybranch
```

5.5 跟新分支
----------
```
//这样就把本地的master 分支和远程同步了
git pull origin master

```

5.6合并分支
------------
```
//  把 mybranch分支合并到当前分支 当前分支为master
git merge mybranch
```



