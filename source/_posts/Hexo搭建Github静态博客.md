---
title: Hexo搭建Github静态博客
date: 2016-06-19 06:52:38
tags: [hexo]
comments: true
type: "tags"
---
通过一些文章自己搭建hexo 并且掉的一些坑

<!-- more -->

一环境
============
    1. 安装git
--------
    2. 安装node
--------


二 配置Github
==============

    1. 建立Repository
------------
建立与你用户名对应的仓库，仓库名必须为【your_user_name.github.io】
比如的自己的git用户名叫junyu-node 仓库名字必须为 junyu-node.github.io

    2. 配置SSH-Key
--------
2.1
在Git Bash输入以下指令（任意位置点击鼠标右键），检查是否已经存在了SSH keys。
```
ls -al ~/.ssh
```
2.2
输入以下指令（邮箱就是你注册Github时候的邮箱）后，回车：
```
ssh-keygen -t rsa -C "angelen10@163.com"
```
2.3
然后它会提示要你输入passphrase（如上图，我没有输入直接回车，如果你输入的话，要记得，到时候会用到）。
2.4
然后键入以下指令：
```
ssh-agent -s
```
2.5
继续输入指令：
```
ssh-add ~/.ssh/id_rsa
```
输入之后，在我这里是出错了，不知道你的有没有出错。

如果你的也是这样子出错了的话，就输入以下指令：
```
eval `ssh-agent -s`
ssh-add
```

到了这一步，就可以添加SSH key到你的Github账户了。键入以下指令，拷贝Key（先拷贝了，等一下可以直接粘贴）：
```
clip < ~/.ssh/id_rsa.pub
```
2.6
然后到Github里面 然后点击 settings
左边导航有个 SSH and GPG keys 点击 进去
然后 点击  New SSH key 设置一个名字 然后粘贴进去 保存即可

-------------
详情请参考[史上最详细“截图”搭建Hexo博客并部署到Github](http://jingyan.baidu.com/article/d8072ac47aca0fec95cefd2d.html)

三 安装Hexo
========
   1. Installation
------------------------
```
npm install -g hexo
```


   2. 在电脑中建立一个名字叫「Hexo」的文件夹，然后在此文件夹中右键打开Git Bash。
------------------------

初始化 hexo
```
hexo init
```
成功会出现
```
[info] Copying data
[info] You are almost done! Don't forget to run `npm install` before you start b
logging with Hexo!
```
Hexo随后会自动在目标文件夹建立网站所需要的文件。然后按照提示，运行 npm install（在 /D/Hexo下）
```
npm install
```
会在D:\Hexo目录中安装 node_modules。

 3.起服务 测试 start the server

 --------
 ```
 $ hexo server
 ```
 [info] Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.

 表明Hexo Server已经启动了，在浏览器中打开 http://localhost:4000/，这时可以看到Hexo已为你生成了一篇blog。

 你可以按Ctrl+C 停止Server

 4. 创建一个新的页 Create a new post
 --------------
 ```
 $ hexo new "My New Post"
 ```
 [info] File created at d:\Hexo\source\_posts\My-New-Post.md

 刷新 (localhost:4000/)，可以发现已生成了一篇新文章 "My New Post"。

 <p style="color:#f00">
 有一个问题，发现 "My New Post" 被发了2遍，在Hexo server所在的git bash窗口也能看到create了2次。
 经验证，在hexo new "My New Post" 时，如果按Ctrl+C将hexo server停掉，就不会出现发2次的问题了。

 所以，在hexo new文章时，需要stop server。

 </p>


 5 Generate static files
 --------------
执行下面的命令，将markdown文件生成静态网页。
```
$ hexo generate
```
该命令执行完后，会在 D:\Hexo\public\ 目录下生成一系列html，css等文件


6.编辑文章
-----------------
hexo new "My New Post"会在D:\Hexo\source\_posts目录下生成一个markdown文件：My-New-Post.md

可以使用一个支持markdown语法的编辑器（比如 Sublime Text 2）来编辑该文件。

 7.部署到Github
  ------------
  部署到Github前需要配置_config.yml文件，首先找到下面的内容

  deploy:
    type: git
    repository: https://github.com/junyu-node/junyu-node.github.io.git
    branch: master

<p style="color:#f00">
    配置冒号后边必须有空格
     hexo 3.0 type 需要配置成git 其他的配置成github
     ```
     npm install hexo-deployer-git --save
     ```
</p>
8. 测试
------------

当部署完成后，在浏览器中打开http://junyu-node.github.io/（https://junyu-node.github.io/） ，正常显示网页，表明部署成功。

9. 总结：部署步骤
------------------

每次部署的步骤，可按以下三步来进行。
```
hexo clean
hexo generate
hexo deploy
```

10. 总结：本地调试
--------------------

1. 在执行下面的命令后，
```
$ hexo g #生成
$ hexo s #启动本地服务，进行文章预览调试
```
浏览器输入http://localhost:4000，查看搭建效果。此后的每次变更_config.yml 文件或者新建文件都可以先用此命令调试，尤其是当你想调试新添加的主题时。

2. 可以用简化的一条命令
```
hexo s -g
```
11 命令总结
-------------
 11.1常用命令

<pre>
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本
</pre>

11.2复合命令

<pre>
hexo deploy -g  #生成加部署
hexo server -g  #生成加预览
</pre>
命令的简写为：
<pre>
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
</pre>

四 配置 主题 和一些功能
==================

1 主题
---------

我安装的主题是next,[next](http://theme-next.iissnan.com/getting-started.html)
1.1在你的根目录下下载主题

```
git clone https://github.com/iissnan/hexo-theme-next themes/next


```

1.2 在hexo/_config.yml 里边搜索

<pre>
    theme: next
</pre>

1.3语言设置
<pre>
    language: zh-Hans
</pre>
1.4主题设定
hexo/themes/next/_config.yml 里边搜索 scheme
<pre>
    #scheme: Muse
    #scheme: Mist
    scheme: Pisces
</pre>
1.5设置 菜单
<pre>
menu:
  home: /
  archives: /archives
  #about: /about
  #categories: /categories
  tags: /tags
  #commonweal: /404.html
</pre>

2多说评论
--------

iissnan-notes 为多说的域名
<pre>
duoshuo_shortname: iissnan-notes
</pre>

3.搜索服务[Swiftype](https://swiftype.com/) 站内搜索
------------------

xxx的值为 图片涂灰的部分
swiftype_key: xxxxxxxxx

4百度统计
---------------------

<pre>
    baidu_analytics:
</pre>


五 参考文档 网址
================

1.[Hexo搭建Github静态博客](http://www.cnblogs.com/zhcncn/p/4097881.html)
2.[站内搜索](https://swiftype.com/)
3.[next主题](http://theme-next.iissnan.com/)






