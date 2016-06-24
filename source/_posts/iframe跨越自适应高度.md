---
title: iframe跨越自适应高度
date: 2016-06-24 10:49:03
tags: [js,iframe,'跨域']
comments: true
---

 每次iframe自适应高度都是一个问题,有一次需求需要跨域iframe高度 然后百度找了一些文章,总结了一个实现比较好的方法
 <!--more-->

 1. 实现原理
 ==============
    首先是需要一个中间的页面(此页面和展示的页面同一个域)

    一个是展示的页面

    还有一个是iframe的页面

    从iframe页面获取高度,里边放入中间的iframe那个页面src的hash上 每次load页面的时候触发
    中间的页面获取到 展示页面的节点 然后获取到自己的hash值 给展示的页面iframe设置高度

 2. 代码
 ==============================

 1.ifame 页面代码
 ---------------
 ```
<iframe src="" style="display:none" frameborder="0" id="iframeA" name="iframeA"></iframe>
 ```
 ```JavaScript

 <script>
  function sethash(){

             hashH = document.documentElement.scrollHeight; //获取自身高度

             urlC = "http://jiaju.sina.com.cn/5892969287299443046/2016/0524/6140714864307667108.html"; //设置中间页面的src

             document.getElementById("iframeA").src=urlC+"#"+hashH; //将高度作为参数传递

         }
         window.onload=sethash;
 </script>

 ```

 2. 展示的页面
 -----------------
```
 <iframe src="http://zx.jiaju.sina.com.cn/index.php?app=Vote&mod=ContestActivity&id=221" frameborder="0" width="1280" id="iframeB" style="min-height:370px"  name="iframeB"></iframe>
```

 3. 中间的页面
 ---------------
```javascript
<script>

function  pseth() {

    var iObj = parent.parent.document.getElementById('iframeB');//A和main同域，所以可以访问节点

    iObjH = parent.parent.frames["iframeB"].frames["iframeA"].location.hash;//访问自己的location对象获取hash值

    iObj.style.height = iObjH.split("#")[1]+"px";//操作dom

}

pseth();

</script>
```


