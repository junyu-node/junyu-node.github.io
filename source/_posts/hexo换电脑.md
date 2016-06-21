---
title: hexo换电脑
date: 2016-06-21 09:33:04
tags: [hexo,git]
comments: true
---
换了电脑编辑我的方法是新建一个hexo的分支储存编辑的文件
<!--more-->
1.给自己的仓库创建一个新的分支,并且把仓库的分支切换默认为hexo
===================
```python

git branch hexo //创建一个分支为hexo
git chckout hexo //本地切换到hexo位默认分支
```
 线上切换默认的分支

1.1点击branches( 如果 branches 只有一个分支,许新建分支hexo)
-----
1.2 点击 Change default branch
-----
1.3 切换 Default branch 下的 master到hexo 点击update

2.添加一个npm
======
```python

npm install hexo-deployer-git --save

```

3.push到服务器上
=============

 1.创建文件 .gitignore 写入要忽略上传的项目
 --------------------
 ```
 touch .gitignore
 ```
 里边填写内容

 <pre>
    node_modules
    public
    .deploy_git
 <pre>

 2.上传到github上
 --------------
 ```
 git add -A //
 git commit -m"注释"
 git remote add origin(别名) https://github.com/junyu-node/junyu-node.github.io.git(Github网址)
 git push origin hexo


 ```
 3.push master 分支
 -----------------
 ```
 hexo clean
 hexo g
 hexo d
 ```

4.在新的电脑上拉去代码
=================
1 拉取代码

-----------
```
git clone https://github.com/junyu-node/junyu-node.github.io.git

cd junyu-node.github.io.git
```

2.安装npm

```
npm install hexo
npm install
npm install hexo-deployer-git//（记得，不需要hexo init这条指令）。
```



