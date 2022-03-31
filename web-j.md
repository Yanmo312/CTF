# 攻防世界—web

### 1、view_source

> 题目：X老师让小宁同学查看一个网页的源代码，但小宁同学发现鼠标右键好像不管用了。

解答：![image-20211109164735624](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109164735624.png)

打开以后只有一句话，在看了许多解答这方面的题目的题解后，没啥提示就F12查看源代码

![image-20211109165038091](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109165038091.png)

然后就看到绿色的答案了

```
cyberpeace{7fab66c1a65c3fddc23ef94b339a01e1}
```

### 2、robots

> 题目：X老师上课讲了Robots协议，小宁同学却上课打了瞌睡，赶紧来教教小宁Robots协议是什么吧。

解答：

#[robots协议_](https://baike.baidu.com/item/Robots协议/2483797)：robots协议也叫robots.txt，是一种存放于网站根目录下的[ASCII](https://baike.baidu.com/item/ASCII)编码的[文本文件](https://baike.baidu.com/item/文本文件)，它通常告诉网络[搜索引擎](https://baike.baidu.com/item/搜索引擎)的漫游器（又称[网络蜘蛛](https://baike.baidu.com/item/网络蜘蛛)），此网站中的哪些内容是不应被搜索引擎的漫游器获取的，哪些是可以被漫游器获取的。

***robots是一个协议，作用是告诉爬虫robots里面的内容不能被搜索引擎搜索引擎。***

![image-20211109170134035](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109170134035.png)

直接在url后加/robots.txt就弹出了这个页面

![image-20211109170300493](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109170300493.png)

然后用相同方法将/f1ag_1s_h3re.php加到后面得到答案

```
cyberpeace{0d74e8fd2e81168c08f4e240880635cd}
```

### 3、backup

> 题目：X老师忘记删除备份文件，他派小宁同学去把备份文件找出来,一起来帮小宁同学吧！

解答：

#php的备份有两种.php~和.php.bak

所以直接在URL后面添加 /index.php.bak

![image-20211109170740196](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109170740196.png)

就会自动下载这个文件

![image-20211109170826300](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109170826300.png)

得到答案

```
Cyberpeace{855A1C4B3401294CB6604CCC98BDE334}
```

### 4、cookie

> 题目：X老师告诉小宁他在cookie里放了些东西，小宁疑惑地想：‘这是夹心饼干的意思吗？’

解答：

#[cookie（储存在用户本地终端上的数据）](https://baike.baidu.com/item/cookie/1119)cookie是服务器发给浏览器的一个身份验证信息的一个值

通过在浏览器控制台输入：document.cookie 获得cookie

![image-20211109171345060](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109171345060.png)

然后浏览器输入/cookie.php

![image-20211109171509438](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109171509438.png)

![image-20211109171744746](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109171744746.png)

F12后看network找到答案

```
cyberpeace{01e645148fef38473bec26047e658635}
```

### 5、disabled_button

> 题目：X老师今天上课讲了前端知识，然后给了大家一个不能按的按钮，小宁惊奇地发现这个按钮按不下去，到底怎么才能按下去呢？

解答：

##### ![image-20211109172124416](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109172124416.png)

将此处改成abled

![image-20211109172216723](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211109172216723.png)

然后这个按钮就可以点了，得到答案

```
cyberpeace{96680751c578a5ccf6833ec0355ce31f}
```

### 6、weak_auth

> 题目：小宁写了一个登陆验证页面，随手就设了一个密码。

解答：

#一般都会有一个用户名为admin 密码为123456或admin123之类的

本题输入admin 123456即可的得到答案

![image-20211110083449832](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110083449832.png)

![image-20211110083427678](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110083427678.png)

```
cyberpeace{8d5d416d532ac70e04332025d504b243}
```

#也可使用burpsuite破译密码[BurpSuite系列(五)----Intruder模块(暴力破解)_fendo-CSDN博客](https://blog.csdn.net/u011781521/article/details/54772795)

### 7、simple_php

> 题目：小宁听说php是最好的语言,于是她简单学习之后写了几行php代码。

解答：

#[PHP（计算机编程语言）](https://baike.baidu.com/item/PHP/9337?fr=aladdin)

打开以后看到![image-20211110084020792](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110084020792.png)

读取信息得知a和b都是get得到，a若为零并且a不为错，b要大于大于1234但不为数字，所以输入a=0.0,b=1234a

![image-20211110084618695](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110084618695.png)

得到答案

![image-20211110084637878](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110084637878.png)

```
Cyberpeace{647E37C7627CC3E4019EC69324F66C7C}
```

### 8、get_post

> 题目：X老师告诉小宁同学HTTP通常使用两种请求方法，你知道是哪两种吗？

解答：

#[HTTP 请求方法 | 菜鸟教程 (runoob.com)](https://www.runoob.com/http/http-methods.html#:~:text=根据 HTTP 标准，HTTP 请求可以使用多种请求方法。 HTTP1.0 定义了三种请求方法： GET%2C POST,HEAD 方法。 HTTP1.1 新增了六种请求方法：OPTIONS、PUT、PATCH、DELETE、TRACE 和 CONNECT 方法。 请求指定的页面信息，并返回实体主体。)根据 HTTP 标准，HTTP 请求可以使用多种请求方法。HTTP1.0 定义了三种请求方法： GET, POST 和 HEAD 方法。HTTP1.1 新增了六种请求方法：OPTIONS、PUT、PATCH、DELETE、TRACE 和 CONNECT 方法。

先使用get输入a，用/?a=1

![image-20211110085202315](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110085202315.png)

再用post方式提交b=2，这里使用hackbar提交，F12找到该插件

![image-20211110085400832](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110085400832.png)

单击load打开enable post，在body里输入b=2

![image-20211110085522632](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110085522632.png)

单击execute，得到答案

![image-20211110085600680](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110085600680.png)

```
cyberpeace{576cf8b7c3d9dda1e194b82aad7e68ed}
```

### 9、xff_referer

> 题目：X老师告诉小宁其实xff和referer是可以伪造的。

解答：

#xff：是告诉服务器当前请求者的最原始的HTTP请求头字段，通常可以直接通过修改HTTP头中的X-Forwarded-For字段来仿造请求的最原始IP。

#referer：referer是告诉服务器当前访问者是从哪个url地址跳转到自己的，也可以直接修改。

打开以后看到这个

![image-20211110085924406](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110085924406.png)

F12使用hackbar

![image-20211110090132902](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110090132902.png)

然后就会出现

![image-20211110090210158](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110090210158.png)

再使用一次hackbar

![image-20211110090300878](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110090300878.png)

得到结果

![image-20211110090322991](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110090322991.png)

```
cyberpeace{a6f18c0fac8205327745dc7584116618}
```

#[HTTP X-Forwarded-For 介绍 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/http-x-forwarded-for.html)

#[Referer - HTTP | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referer)

### 10、webshell

> 题目：小宁百度了php一句话,觉着很有意思,并且把它放在index.php里

解答：

#[PHP一句话木马之小马 - 简书 (jianshu.com)](https://www.jianshu.com/p/90473b8e6667)

#[webshell_百度百科 (baidu.com)](https://baike.baidu.com/item/webshell/966625)

#[eval()_百度百科 (baidu.com)](https://baike.baidu.com/item/eval()/3763558)

打开题目场景看到如下

![image-20211110090738384](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110090738384.png)

F12打开hackbar，输入shell=phpinfo();

![image-20211110091223917](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110091223917.png)

再输入shell=system("Is");

![image-20211110091429060](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110091429060.png)

得知这有一个txt,输入shell=system("cat flag.txt");

![image-20211110091642336](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211110091642336.png)

得到答案

```
cyberpeace{f4574ab5ff838cbbf69ca99f719f864b}
```

### 11、command_execution

> 题目:小宁写了个ping功能,但没有写waf,X老师告诉她这是非常危险的，你知道为什么吗。

关于ping[PING命令入门详解 ——世界网络 (linkwan.com)](http://www.linkwan.com/gb/tech/htm/928.htm)

关于waf[WAF_百度百科 (baidu.com)](https://baike.baidu.com/item/WAF/3239498)

解答：先ping一下127.0.0.1试试

![image-20220331192508619](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220331192508619.png)

```
command1 & command2 ：不管command1执行成功与否，都会执行command2（将上一个命令的输出作为下一个命令的输入），也就是command1和command2都执行
command1 && command2 ：先执行command1执行成功后才会执行command2，若command1执行失败，则不执行command2
command1 | command2 ：只执行command2
command1 || command2 ：command1执行失败，再执行command2(若command1执行成功，就不再执行command2)
```

以上是相关命令规则

找找看有没有flag

![image-20220331192603344](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220331192603344.png)

看到flag了，用cat抓取一下

![image-20220331192650462](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220331192650462.png)

![image-20220331192723158](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220331192723158.png)

得到flag

### 12、simple_js

> 题目:小宁发现了一个网页，但却一直输不对密码。

打开如图，随便输入个密码试试

![image-20220331192807671](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220331192807671.png)

![image-20220331192928647](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220331192928647.png)

好像输什么都会出现这个，关掉对话框，F12试试

发现一串似乎看得懂的代码

  ![image-20220331193114495](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220331193114495.png)

感觉底下那一串像是密码

复制下来16进制转ASCII,

```python
s="\x35\x35\x2c\x35\x36\x2c\x35\x34\x2c\x37\x39\x2c\x31\x31\x35\x2c\x36\x39\x2c\x31\x31\x34\x2c\x31\x31\x36\x2c\x31\x30\x37\x2c\x34\x39\x2c\x35\x30"
print (s)
//[55,56,54,79,115,69,114,116,107,49,50] 注：tab此时是字符串数组！！！

```

再ASCII转字符

```python
s=[55,56,54,79,115,69,114,116,107,49,50]
for i in s:
  print(chr(i),end='')
```

![image-20220331193406481](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220331193406481.png)

得到flag
