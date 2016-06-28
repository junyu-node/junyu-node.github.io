---
title: 基本的shell命令
date: 2016-06-28 09:01:43
tags: [shell,liunx]
comments: true
---

随着node的应用,一些前端的一些工具也越来越多, 一些工具都会用到一些linux命令.下边介绍一些简单的shell命令
<!--more-->

cd 目录切换
================
```
# 格式 cd dirname  dirname是想要进入的目录
cd /d/dir //进入到d盘的dir下目录下
cd ../ //返回上一层目录
cd ../../ //返回上一层的上一层目录
```

mkdir 新建文件夹
===============
```
 mkdir dirname
 mkdir website dirname
```

touch 创建文件
==========

```
touch .gitignore
touch a.js b.js
```

ls 显示文件
==============

```
# 显示详细列表
ls -l

# ls -l的简写
ll

#显示所有文件,包含隐藏文件
ls -a

#显示文件及所有子目录
ls -R

```

pwd 显示当前目录
===============
```
pwd
```

cat 显示文件内容
========

```
cat filename
```

rm 删除文件或者目录
==============

```
# 删除 档名为 file1的文档
rm file1

# 删除文档中有五个字元,之前的四个字为file
rm file

#删除 档名中 以f打头的 文档
rm f*

#删除 目录 dir1 及以下所有温昂及子目录
rm -r dir1
```

cp 文档的复制
=============

```
# 将文档 file1 复制成 file2
$ cp file1 file2
# 将文档 file1 复制到目录 dir1 下，文件名仍为 file1.
$ cp file1 dir1
# 将目录 /tmp 下的文档 file1复制到现行目录下，文件名仍为 file1.
$ cp /tmp/file1 .
# 将目录 /tmp 下的文档 file1现行目录下，档名为file2
$ cp /tmp/file1 file2
# (recursive copy) 复制整个目录.
$ cp -r dir1 dir2
# 复制dir1整个目录到dir2
$ cp -R dir1 dir2

```

mv 移动文件
====================

```
# 将文档 file1，更改档名为 file2.
$ mv file1 file2
# 将文档 file1，移到目录 dir1 下，档名仍为 file1.
$ mv file1 dir1
# 若目录 dir2 不存在，则将目录 dir1，及其所有档案和子目录，移到目录 dir2 下，新目录名称为 dir1.若目录dir2 不存在，则将dir1，及其所有文档和子目录，更改为目录 dir2.
$ mv dir1 dir2
```

vim 编辑器
=====================

```
j,k,h,l:上下左右
0： 行首
$: 行尾
i,I :插入命令，i 在当前光标处插入 I 行首插入
a,A:追加命令，a 在当前光标后追加，A 在行末追加
o,O:打开命令，o 在当前行下打开一行，O在当前行上插入一行
r,R :替换命令，r 替换当前光标处字符，R从光标处开始替换
数字s: 替换指定数量字符
x: 删除光标处字符
dd: 删除当前行
d0: 删除光标前半行
d$: 删除光标后半行
ctrl+f :后翻页
ctrl+b:前翻页
G : 文件尾
数字G: 数字所指定行
/string 查找字符串
n 继续查找
N 反向继续查找
% 查找对应括号
u 取消上次操作
ex命令状态
：0 文件首
：1,5 copy 7 块拷贝
：1，5 del 块删除
：1，5 move 7 块移动
：1，$s/string1/string2/g 全文件查找string1并替换为string2
：wq! 存盘退出
```
