---
title: 正则
date: 2016-06-20 15:10:45
tags: [regRxp,正则,js]
comments: true
---

对正则的一些总结和简单应用
<!--more-->

1定义
======================

<pre>
    var reg=/\w+/g ;
    var reg1=regExp('\\w+','g);
</pre>

第一种定义方式 没有办法传参
第二种可以传参
一般不需要传参的话我一般用第一种定义正则

2 正则简单的基础
===============
2.1 开始符&结束符
-------------
^      匹配字符串的开头 如果设置了RegExp对象的Multiline属性， 也匹配\n \r 后的位置
$      匹配输入字符串的结束位置。如果设置了RegExp对象的Multiline属性，$也匹配“\n”或“\r”之前的位置。
```JavaScript
    var reg=/^\w+/gm;
    var reg1=/^\w+/g
    var str='sdasds1234523454\nsadhdasdj';
    var arr=str.match(reg);
    console.log(arr)//[ 'sdasds1234523454', 'sadhdasdj' ]

    var arr1=str.match(reg1);
    console.log(arr1)//['sdasds1234523454\nsadhdasdj']
```
2.2量词
-------
 ```JavaScript
 * 匹配前面的子表达式任意次。例如，zo*能匹配“z”，“zo”以及“zoo”，但是不匹配“bo”。*等价于{0,}
 + 匹配前面的子表达式至少一次 等价于 {1,}
 ? 可有可无 等价于{0,1}
 {n} n个
｛n,｝ 至少n个
 {n,m} n-m个
 ```

2.3字符缩写
----------------
 ```JavaScript
  x|y 或的关系 等价于 [xy]
 [^xy] 非xy
 [a-z] a到 z
  [^a-z] 非 a-z

  \b 匹配一个单词边界，也就是指单词和空格间的位置（即正则表达式的“匹配”有两种概念，一种是匹配字符，一种是匹配位置，这里的\b就是匹配位置的）。例如，“er\b”可以匹配“never”中的“er”，但不能匹配“verb”中的“er”。
  \B 匹配非单词边界。“er\B”能匹配“verb”中的“er”，但不能匹配“never”中的“er”。


  \d 匹配一个数字字符。等价于[0-9]。grep 要加上-P，perl正则支持
  \D 匹配一个非数字字符。等价于[^0-9]。grep要加上-Pperl正则支持
  \n 匹配一个换行符。等价于\x0a和\cJ。
  \r 匹配一个回车符。等价于\x0d和\cM。
  \s 匹配任何不可见字符，包括空格、制表符、换页符等等。等价于[ \f\n\r\t\v]。
  \S 匹配任何可见字符。等价于[^ \f\n\r\t\v]。
  \w 匹配包括下划线的任何单词字符。类似但不等价于“[A-Za-z0-9_]”，这里的"单词"字符使用Unicode字符集。
  \W 匹配任何非单词字符。等价于“[^A-Za-z0-9_]”。
```
2.4 参数
---------------
2.4.1 g
    g 只影响于 exec、match 方法。

    若不指定 g，则：每次调用 exec 都只返回第一个匹配；match 也是只返回第一个匹配。

    若指定 g，则：每次调用 exec 都从上一个匹配之后查找新的匹配；match 则是返回所有的匹配。

    还有一种情况，就是使用 string 对象的 replace 方法时，指定 g 表示替换所有。
2.4.2 i

  参数 i 是指忽略大小写，注意仅是忽略大小写，并不忽略全半角。
2.4.3 m
    附加参数m，表明可以进行多行匹配，但是这个只有当使用^和$模式时才会起作用，在其他的模式中，加不加入m都可以进行多行匹配（其实说多行的字符串也是一个普通字符串）
 3.贪婪非贪婪模式
 ================
```JavaScript
 ? 当该字符紧跟在任何一个其他限制符
  （*,+,?，{n}，{n,}，{n,m}）后面时，
  匹配模式是非贪婪的。非贪婪模式尽可能少的匹配所搜索的字符串
  ，而默认的贪婪模式则尽可能多的匹配所搜索的字符串。
  例如，对于字符串“oooo”，“o+?”将匹配单个“o”，
  而“o+”将匹配所有“o”。

 var reg=/[a-zA-Z]+?/g;
 var reg1=/[a-zA-Z]+/g
 var str='sasdqwew23q3e4a6s7d9asdas';
 console.log(str.match(reg));
 //[ 's','a','s','d','q','w','e','w','q','e','a', 's'...]

 console.log(str.match(reg1));
 //[ 'sasdqwew', 'q', 'e', 'a', 's', 'd', 'asdas' ]
 ```

 4.点
 ============
 ```JavaScript
 .点 匹配除“\r\n”之外的任何单个字符。要匹配包括“\r\n”在内的任何字符，请使用像“[\s\S]”的模式。

 var reg=/.+/g;
 var reg1=/[\s\S]+/g;
 console.log('assdlk8554867486\n\rasdhuijk.lkashjdsadnlpo./'.match(reg));
 //[ 'assdlk8554867486', 'asdhuijk.lkashjdsadnlpo./' ]
 console.log('assdlk8554867486\n\rasdhuijk.lkashjdsadnlpo./'.match(reg1));
 //[ 'assdlk8554867486\n\rasdhuijk.lkashjdsadnlpo./' ]
 ```
5.捕获非捕获
===============

 ```JavaScript
 //(pattern) 匹配pattern并获取这一匹配。所获取的匹配可以从产生的Matches集合得到，在VBScript中使用SubMatches集合，在JScript中则使用$0…$9属性。要匹配圆括号字符，请使用“\(”或“\)”。


 //var reg=/([a-z]+)(\d*)/g;

 //var str='sdsda;;sdahj8202xdsa9fdsfsd5sdf12sfdsd';
 //console.log(reg.test(str));//true
 //console.log(RegExp.$1);//sdahj
 //console.log(RegExp.$2);//8202


 // (?:pattern) 非获取匹配，匹配pattern但不获取匹配结果，不进行存储供以后使用。这在使用或字符“(|)”来组合一个模式的各个部分是很有用。例如“industr(?:y|ies)”就是一个比“industry|industries”更简略的表达式。


 //var reg=/([a-z]+)(?:8|\d+)/g;

 //console.log(str.match(reg));//[ 'sdahj8202', 'xdsa9', 'fdsfsd5', 'sdf12' ]

 //(?=pattern)非获取匹配，正向肯定预查，在任何匹配pattern的字符串开始处匹配查找字符串，该匹配不需要获取供以后使用。
 // 例如，“Windows(?=95|98|NT|2000)”能匹配“Windows2000”中的“Windows”，
 // 但不能匹配“Windows3.1”中的“Windows”。
 // 预查不消耗字符，也就是说，
 // 在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，
 // 而不是从包含预查的字符之后开始。
 //var reg1=/([a-z]+)(?=\d+)/g;

 //console.log(str.match(reg1)); //[ 'sdahj', 'xdsa', 'fdsfsd', 'sdf' ]
 //(?!pattern)非获取匹配，正向否定预查，
 // 在任何不匹配pattern的字符串开始处匹配查找字符串，
 // 该匹配不需要获取供以后使用。例如“Windows(?!95|98|NT|2000)”
 // 能匹配“Windows3.1”中的“Windows”，但不能匹配“Windows2000”中的“Windows”。
 ```
 6.常用正则
 =========
 ```JavaScript
 验证手机号码："^1[3|4|5|7|8][0-9]\\d{8}$"
 验证身份证号（15位或18位数字）："\\d{14}[[0-9],0-9xX]"
 验证Email地址：("^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$")

 验证URL："^https?://([\w-]+\.)+[\w-]+(/[\w-./?%&=]*)?$"
 匹配空白行的正则表达式：\n\s*\r

 匹配腾讯QQ号：[1-9][0-9]{4,}
 ```
 7.正则的方法
 ============
 ```JavaScript
 // 正则的方法
 // test 判断

 //eg
 var str='4567ssdsc85d 8s5s';
 var reg=/(\d+)([a-z]*)/g;

 console.log(reg.test(str));//true;



 //exec  检索字符串中指定的值。返回找到的值，并确定其位置。
 //如果 exec() 找到了匹配的文本，
 // 则返回一个结果数组。
 // 否则，返回 null。
 // 此数组的第 0 个元素是与正则表达式相匹配的文本，
 // 第 1 个元素是与 RegExpObject 的第 1 个子表达式相匹配的文本（如果有的话），
 // 第 2 个元素是与 RegExpObject 的第 2 个子表达式相匹配的文本（如果有的话），
 // 以此类推。除了数组元素和 length 属性之外，exec() 方法还返回两个属性
 // 。index 属性声明的是匹配文本的第一个字符的位置。
 // input 属性则存放的是被检索的字符串 string。
 // 我们可以看得出，在调用非全局的 RegExp 对象的 exec() 方法时，
 // 返回的数组与调用方法 String.match() 返回的数组是相同的。
 console.log(reg.exec(str)); //[ '4567ssdsc','4567','ssdsc',index: 0,input: '4567ssdsc85d 8s5s' ]



 //compile 编译正则表达式。



 // str的方法
 // match 返回匹配的数组

     console.log(str.match(reg));//[ '4567', '85', '8', '5' ]
 // replace() 方法用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。

 ```

 8.replace
 ==========
 ```JavaScript
 // replace 替换

 var str='hello,world hello,bob'
 var str1=str.replace('h','H');
 console.log(str1) //Hello,world hello,bob

 var str2=str.replace(/h/,'H');
 console.log(str2) //Hello,world hello,bob
 //全局匹配查找并替换
 console.log(str.replace(/h/g,'H')) // Hello,world Hello,bob
 console.log(str.replace(/b/g,'$`')) //  ello,world hello,world ello,bob
 // leftContext
 // 是当前表达式模式最后一个匹配字符串左边的所有内容，
 // 可以简写为$`（其中"'"为键盘上"Esc"下边的反单引号）。
 // 初始值为空字符串""。每次成功匹配时，其属性值都会随之改变。

 console.log(str.replace(/h/g,"$'"))
 ////rightContext
 // 是当前表达式模式最后一个匹配字符串右边的所有内容，可以简写为$'。
 // 初始值为空字符串""。每次成功匹配时，其属性值都会随之改变。


 function replacer(match, p1, p2, p3, offset, string){

     // match 匹配的字串（对应$&）
     // p1, p2, ..假如replace()方法的第一个参数是一个RegExp 对象，则代表第n个括号匹配的字符串。（对应于上述的$1，$2等。）
     // offset 匹配到的子字符串在原字符串中的偏移量。（比如，如果原字符串是"abcd"，匹配到的子字符串时"bc"，那么这个参数将时1）
     // string被匹配的原字符串。

     console.log(match); // abc12345#$*%
     console.log(p1);    // abc
     console.log(p2);    // 12345
     console.log(p3);    // #$*%
     console.log(string);// abc12345#$*%

     return [p1, p2, p3].join(' - ');

 }

 var newString = 'abc12345#$*%'.replace(/([^\d]*)(\d*)([^\w]*)/,replacer);


 //alert(newString);

 //////////////////////////////////

 /*
  var re = /apples/gi;
  var str = "Apples are round, and apples are juicy.";
  var newstr = str.replace(re, "oranges");
  */

 //alert(newstr);

 //////////////////////////////////

 /*var str = "Apples are round, and apples are juicy.";
  var newstr = str.replace("apples", "oranges", "gi");  // 这个不兼容IE
  alert(newstr);*/


 //////////////////////////////////

 // 交换字符串中的两个单词
 /*var re = /(\w+)\s(\w+)/;
  var str = "John Smith";
  var newstr = str.replace(re, "$2 $1");
  alert(newstr);
  */
  ```

  9.反向应用
  =======


  ```JavaScript

  /**
   * Created by Administrator on 2016/6/16.
   */
  // \1，\2 对序号为1和2的捕获组的反向引用

  //“(a|b)\1”在匹配“abaa”时，匹配成功，匹配到的结果是“aa”。
  // “(a|b)”在尝试匹配时，虽然既可以匹配“a”，也可以匹配“b”，
  // 但是在进行反向引用时，对应()中匹配的内容已经是固定的了。

  var reg=/(a|b)\1/g;
  var reg2=/(a|b)(\w)\2/g;
  var str='abaabbdsfsdfsd';
  console.log(reg)

  console.log(str.match(reg)); [ 'aa', 'bb' ]
  console.log(str.match(reg2)) [ 'baa' ]
  ```
