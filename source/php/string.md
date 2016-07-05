---
title: php
date: 2016-06-29 10:03:15
tags: [php]
comments: true
---

string
=======

```
<?php
    // 注释用双斜杠注释
    // php加结束符分好 否则会报错
 echo "hello world";

 echo 'hello world';
 // 点事连接符 相当于js里边的 +

 echo '你好'."呵呵";

?>
```

变量
=====
变量必须遵守的规则
---------------
    1 变量名必须以字母或者下划线开头
    2.变量名只能由字母数字及_组成
    3.变量名不允许包含空壳
```
<?php
//定义变量
$str="hello PHP";


?>
```
变量的类型
-----------

1字符串类型
```
$str="hello world";
```
2.整形
```
$int=123;
```
3.浮点型
```
$fl=2.3;
```
4数组
```
$array=array(123,456);
```
5标量类型-布尔类型
$flag=TRUE;

判断类型
```
var_dump($int);//int(123)
var_dump($fl);// float(2.3)
var_dump($str)//string(11) "hello world" 一个汉子相当于3个字节
var_dump(#array) // array(2) {[0]=>int(123) [1]=>int(456)}
```