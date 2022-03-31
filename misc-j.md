# 攻防世界-misc

### 1.this_is_flag

> 题目：Most flags are in the form flag{xxx}, for example:flag{th1s_!s_a_d4m0_4la9}

解答：答案就在题目里

```
flag{th1s_!s_a_d4m0_4la9}
```



### 2.pdf

> 题目：菜猫给了菜狗一张图，说图下面什么都没有

![2020051012590940](F:\ctf\做题\2020051012590940.png)

解答：双击图片后发现图下有东西，复制下来就是flag

```
flag{security_through_obscurity}
```

*网上说还可以把pdf转换成word

### 3.如来十三掌

> 题目：菜狗为了打败菜猫，学了一套如来十三掌。

![20200510133031331](F:\ctf\做题\20200510133031331.png)

解答：通过看题解知道在[与佛论禅](http://www.keyfc.net/bbs/tools/tudoucode.aspx)上解密，记得要加”佛曰：“

解密后会出来：

```
MzkuM3gvMUAwnzuvn3cgozMlMTuvqzAenJchMUAeqzWenzEmLJW9
```

通过查资料和看题解，说这个是先用rot-13解码，再base64解密

```
flag{bdscjhbkzmnfrdhbvckijndskvbkjdsab}
```



*ROT-13（回转13位，rotateby13places，有时中间加了个减号称作ROT-13）是一种简易的置换暗码。

*使用Converter转换，再用Notepad++进行base64解密

### 4.give_you_flag

> 题目：菜狗找到了文件中的彩蛋很开心，给菜猫发了个表情包

![](F:\ctf\做题\4b0799f9a4d649f09a882b6b1130bb70.gif)

解答：动图发现有一帧弹出了二维码，考虑将这一帧拿出来，然后补全二维码

![](F:\ctf\做题\frame50.bmp)

```
flag{e7d478cf6b915f50ab1277f78502a2c5}
```



*分解动图用的CTFCrackTools-V2

*在电脑上生成二维码，识别二维码用到QR Research

### 5.stegano

> 题目：菜狗收到了图后很开心，玩起了pdf 提交格式为flag{xxx}，解密字符需小写

![image-20211103103506929](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211103103506929.png)

解答：看题解说要全部复制下来到notepad++，然后发现顶上有一串和flag有关的文字

```
BABA BBB BA BBA ABA AB B AAB ABAA AB B AA BBB BA AAA BBAABB AABA ABAA AB BBA BBBAAA ABBBB BA AAAB ABBBB AAAAA ABBBB BAAA ABAA AAABB BB AAABB AAAAA AAAAA AAAAB BBA AAABB
```

解析说，如果没有空格的话，考虑二进制，有空格就考虑摩斯电码

```
flag{1nv151bl3m3554g3}
```

*在[密码机器]([密码机器 (ctftools.com)](http://www.ctftools.com/down/down/passwd/))里转化摩斯电码

### 6.坚持60s

> 题目：菜狗发现最近菜猫不爱理他，反而迷上了菜鸡

![image-20211103115306304](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211103115306304.png)

解答：题解说要用jd-gui打开，打开后直接在搜索栏搜索flag，就能找到，找到之后再用base64解码

![image-20211103115726614](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211103115726614.png)

```java
case 6:         					
	printInfo(g,"flag{RGFqaURhbGlfSmlud2FuQ2hpamk=}",50,150,300);
    break;
```

用Notepad++解码后得：

```
flag{DajiDali_JinwanChiji}
```

### 7.gif

> 题目：菜狗截获了一张菜鸡发给菜猫的动态图，却发现另有玄机

![image-20211103120341419](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211103120341419.png)

解答：gif文件打开后是黑白的图片，考虑二进制转化

以下是在题解里看到的两种代码

```python
white = open(“0.jpg”,“rb”).read()
black = open(“1.jpg”,“rb”).read()
color = “”
for i in range(104):
with open("%d.jpg"%i,“rb”) as f:
if f.read() == white:
color += “0”
else:
color += “1”
flag = “”
for i in range(13):
flag += chr(int(color[i*8:(i+1)*8],2))
print(flag)
```

```python
x=[0b01100110, 0b01101100, 0b01100001, 0b01100111, 0b01111011, 0b01000110, 0b01110101, 0b01001110, 0b01011111, 0b01100111, 0b01101001, 0b01000110, 0b01111101]
b="";
for a in x:
    b+=chr(a);
print(b)
```

得到结果：

```
flag{FuN_giF}
```

### 8.掀桌子

> 题目：菜狗截获了一份报文如下c8e9aca0c6f2e5f3e8c4efe7a1a0d4e8e5a0e6ece1e7a0e9f3baa0e8eafae3f9e4eafae2eae4e3eaebfaebe3f5e7e9f3e4e3e8eaf9eaf3e2e4e6f2，生气地掀翻了桌子(╯°□°）╯︵ ┻━┻

解答：

应该就是变换这一大串，题解说因为这是字母+数字为一组，像是16进制，而一共是118个，但发现转换成ASCII码不行，试一下发现要-128，

```python
string = "c8e9aca0c6f2e5f3e8c4efe7a1a0d4e8e5a0e6ece1e7a0e9f3baa0e8eafae3f9e4eafae2eae4e3eaebfaebe3f5e7e9f3e4e3e8eaf9eaf3e2e4e6f2"
flag = ''
for i in range(0,len(string), 2):
    s = "0x" + string[i] + string[i+1]
    flag += chr(int(s, 16) - 128)
print(flag)
```

得到结果：

```
flag{hjzcydjzbjdcjkzkcugisdchjyjsbdfr}
```

### 9.ext3

> 题目：今天是菜狗的生日，他收到了一个linux系统光盘

*还没装linux,周末就装:( 先看看题解

解答：

把文件拖到linux，查看flag，会发现

![img](https://img-blog.csdnimg.cn/20200909140647721.png#pic_center)

查看发现是让你恢复文件，那就使用

```
ext3grep f1fc23f5c743425d9e0073887c846d23 --restore-all
```

然后进入到刚才看到的那个文件夹中发现一串base64，再进行解码

得到结果：

```
flag{sajbcibzskjjcnbhsbvcjbjszcszbkzj}
```

### 10.SimpleRAR

> 题目：菜狗最近学会了拼图，这是他刚拼好的，可是却搞错了一块(ps:双图层)

解答：

用010 Editor 6.0_shenyongran打开，题解判断not here后面是想要的文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020060713460489.png)

要的是文件块而不是子块，所以修改7A为74

![image-20211103122525588](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211103122525588.png)

然后就出现

![image-20211103122618830](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211103122618830.png)

解压出来后是空白的图片，再用CTFCrackTools-V2发现是gif文件，再把每一帧都分离出来，然后把残缺的两块二维码拼一块

补全后用QRResearch扫描得结果

```
flag{yanji4n_bu_we1shi}
```

*如何识别是否是base64编码加密？

首先我们根据base64编码特点分析：

- 字符串只可能包含A-Z，a-z，0-9，+，/，=字符

- 字符串长度是4的倍数

- =只会出现在字符串最后，可能没有或者一个等号或者两个等号

  因此通过以上特点很容易辨别base64编码

### 11.base64stego

> 题目：下载附件后有一个压缩包,菜狗经过几天的学习，终于发现了如来十三掌最后一步的精髓

解答：

压缩包需要密码，在网上搜索两种解决方案，本次使用的第一种：

1、使用winRAR打开压缩包，使用工具栏的“修复功能”后，再次解压即可

![image-20220329154718045](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220329154718045.png)

2、简单了解zip文件的结构:
zip文件由三部分构成：压缩源文件数据区+目录区+目录结束区
源文件数据区：文件头+文件数据+数据描述符

通过百度我们知道这个zip文件是一个伪加密
需要使用winhex工具去修改文件头的加密标志位，或者使用zipcenop.jar
下面说说两种工具的简单使用：

- winhex
  可参考https://blog.csdn.net/pdsu161530247/article/details/73612910
  大致操作如下截图：
  ![img](https://img2020.cnblogs.com/blog/2057437/202103/2057437-20210307154104537-884426188.png)
  为什么要搜索50 4B呢，因为50 4B 01 02是目录中文件文件头标记，关于更多详细信息参考上面给出的帖子

解压后是一堆base64，而直接解压后是

```
Steganography is the art and science of writing hidden messages in such a way that no one
```

是个base64隐写

```python
b="""
U3RlZ2Fub2dyYXBoeSBpcyB0aGUgYXJ0IGFuZCBzY2llbmNlIG9m
IHdyaXRpbmcgaGlkZGVuIG1lc3NhZ2VzIGluIHN1Y2ggYSB3YXkgdGhhdCBubyBvbmV=
LCBhcGFydCBmcm9tIHRoZSBzZW5kZXIgYW5kIGludGVuZGVkIHJlY2lwaWVudCwgc3VzcGU=
Y3RzIHRoZSBleGlzdGVuY2Ugb2YgdGhlIG1lc3M=
YWdlLCBhIGZvcm0gb2Ygc2VjdXJpdHkgdGhyb3VnaCBvYnNjdXJpdHkuIFS=
aGUgd29yZCBzdGVnYW5vZ3JhcGh5IGlzIG9mIEdyZWVrIG9yaWdpbiBhbmQgbWVhbnMgImNvbmNlYW==
bGVkIHdyaXRpbmciIGZyb20gdGhlIEdyZWVrIHdvcmRzIHN0ZWdhbm9zIG1lYW5pbmcgImNv
dmVyZWQgb3IgcHJvdGVjdGVkIiwgYW5kIGdyYXBoZWluIG1lYW5pbmcgInRvIHc=
cml0ZSIuIFRoZSBmaXJzdCByZWNvcmRlZCB1c2Ugb2YgdGhlIHRlcm0gd2FzIGluIDE0OTkgYnkgSm9o
YW5uZXMgVHJpdGhlbWl1cyBpbiBoaXMgU3RlZ2Fub2dyYXBoaWEsIGEgdHJlYV==
dGlzZSBvbiBjcnlwdG9ncmFwaHkgYW5kIHN0ZWdhbm9ncmFwaHkgZGlzZ8==
dWlzZWQgYXMgYSBib29rIG9uIG1hZ2ljLiBHZW5lcmFsbHksIG1lc3P=
YWdlcyB3aWxsIGFwcGVhciB0byBiZSBzb21ldGhpbmcgZWxzZTogaW1hZ2VzLCBhcnRp
Y2xlcywgc2hvcHBpbmcgbGlzdHMsIG9yIHNvbWUgb3R=
aGVyIGNvdmVydGV4dCBhbmQsIGNsYXNzaWNhbGx5LCB0aGUgaGlkZGVuIG1lc3NhZ2UgbWF5IGJlIGluIGludmm=
c2libGUgaW5rIGJldHdlZW4gdGhlIHZpc2libGUgbGluZXMgb2YgYSBwcml2YXRlIGxldHRlci4NCg0KVGhl
IGFkdmFudGFnZSBvZiBzdGVnYW5vZ3JhcGh5LCBvdmVyIGNy
eXB0b2dyYXBoeSBhbG9uZSwgaXMgdGhhdCBtZXNzYWdlcyBkbyBub3QgYXR0cmFjdCBhdHRlbnRpb25=
IHRvIHRoZW1zZWx2ZXMuIFBsYWlubHkgdmlzaWJsZSBlbmNyeXB0ZWQgbWVzc2FnZXOXbm8gbWF0dGVyIF==
aG93IHVuYnJlYWthYmxll3dpbGwgYXJvdXNlIHN=
dXNwaWNpb24sIGFuZCBtYXkgaW4gdGhlbXNlbHZlcyBiZSBpbmNyaW1pbmF0aW5nIP==
aW4gY291bnRyaWVzIHdoZXJlIGVuY3J5cHRpb24gaXMgaWxsZWdhbC4gVGhlcmVmb3JlLH==
IHdoZXJlYXMgY3J5cHRvZ3JhcGh5IHByb3RlY3RzIHRoZSBjb250ZW50cyBvZj==
IGEgbWVzc2FnZSwgc3RlZ2Fub2dyYXBoeSBjYW4gYmUgc2FpZCB0byBwcm90ZWN0IGJ=
b3RoIG1lc3NhZ2VzIGFuZCBjb21tdW5pY2F0aW5nIHBhcnRpZXMuDQoNClN0ZWdhbm9ncmFwaHkgaW5jbHW=
ZGVzIHRoZSBjb25jZWFsbWVudCBvZiBpbmZvcm1hdGlvbiB3aXRoaW4gY29t
cHV0ZXIgZmlsZXMuIEluIGRpZ2l0YWwgc3RlZ2Fub2dyYXBoeSwgZWxlY3Ryb25pYyBjb21tdW5pY2F0aW9u
cyBtYXkgaW5jbHVkZSBzdGVnYW5vZ3JhcGhpYyBjb2RpbmcgaW5zaZ==
ZGUgb2YgYSB0cmFuc3BvcnQgbGF5ZXIsIHN1Y2ggYXMgYSBkb2N1bWVudCBmaWxlLCBpbWFnZSBmaWx=
ZSwgcHJvZ3JhbSBvciBwcm90b2NvbC4gTWVkaWEg
ZmlsZXMgYXJlIGlkZWFsIGZvciBzdGVnYW5vZ3JhcGhpYyB0cmFuc21pc3Npb+==
biBiZWNhdXNlIG9mIHRoZWlyIGxhcmdlIHNpemUuIEFzIB==
YSBzaW1wbGUgZXhhbXBsZSwgYSBzZW5kZXIgbWlnaHQgc3RhcnQgd2l0aCBh
biBpbm5vY3VvdXMgaW1hZ2UgZmlsZSBhbmQgYWRqdXN0IHRoZSBjb2xvciBvZiBldmVyeSAxMDB0aCBwaXhlbCD=
dG8gY29ycmVzcG9uZCB0byBhIGxldHRlciBpbiB0aGUgYWxwaGFiZXQsIGF=
IGNoYW5nZSBzbyBzdWJ0bGUgdGhhdCBzb21lb25lIG5vdCBzcGVjaWZpY2FsbHkgbG9va2luZyBm
b3IgaXQgaXMgdW5saWtlbHkgdG8gbm90aWNlIGl0Lg0KDQpUaGU=
IGZpcnN0IHJlY29yZGVkIHVzZXMgb2Ygc3RlZ2Fub2dyYXBoeSBjYW4gYmUgdHJ=
YWNlZCBiYWNrIHRvIDQ0MCBCQyB3aGVuIEhlcm9kb3R1cyBtZW50aW9ucyB0d28gZXhhbXBsZXMgb+==
ZiBzdGVnYW5vZ3JhcGh5IGluIFRoZSBIaXN0b3JpZXMgb2Yg
SGVyb2RvdHVzLiBEZW1hcmF0dXMgc2VudCBhIHdhcm5pbmcgYWJvdXQgYSB=
Zm9ydGhjb21pbmcgYXR0YWNrIHRvIEdyZWVjZSBieSB3
cml0aW5nIGl0IGRpcmVjdGx5IG9uIHRoZSB3b29kZW4gYmFja2luZyBvZiBhIHdheCB0YWJsZXQgYmVm
b3JlIGFwcGx5aW5nIGl0cyBiZWVzd2F4IHN1cmZhY2UuIFdheCB0YWJsZXRzIHdlcmUgaW4gY29tbW9uIHVzZV==
IHRoZW4gYXMgcmV1c2FibGUgd3JpdGluZyBzdXJmYWNlcywgc29tZXRpbWX=
cyB1c2VkIGZvciBzaG9ydGhhbmQuIEFub3RoZXIgYW5jaWVudCBleGFtcGxlIGlzIHRoYXQgb9==
ZiBIaXN0aWFldXMsIHdobyBzaGF2ZWQgdGhlIGhlYWQgb2YgaGlzIG1vc3QgdHJ1c3RlZCBz
bGF2ZSBhbmQgdGF0dG9vZWQgYSBtZXNzYWdlIG9uIGl0LiBBZnRlciBoaXMgaGFpciBoYWQgZ5==
cm93biB0aGUgbWVzc2FnZSB3YXMgaGlkZGVuLiBUaGUgcHVycG9zZSB3YXMgdG+=
IGluc3RpZ2F0ZSBhIHJldm9sdCBhZ2FpbnN0IHRoZSBQZXJzaWFucy4NCg0KU3RlZ2Fub2dyYXBoeSBoYXMgYm==
ZWVuIHdpZGVseSB1c2VkLCBpbmNsdWRpbmcgaW4gcmVjZW50IGhpc3RvcmljYWwgdGltZXMgYW5kIHT=
aGUgcHJlc2VudCBkYXkuIFBvc3NpYmxlIHBlcm11dGF0aW9ucyBhcmUgZW5kbGVzcyBhbmT=
IGtub3duIGV4YW1wbGVzIGluY2x1ZGU6DQoqIEhpZGRlbiBtZXNzYWdlcyB3aXRoaW4gd2F4IHRh
YmxldHM6IGluIGFuY2llbnQgR3JlZWNlLCBwZW9wbGUgd3JvdGUgbWV=
c3NhZ2VzIG9uIHRoZSB3b29kLCB0aGVuIGNvdmVyZWQgaXQgd2l0aCB3YXggdXBvbiB3aGljaCBhbiBpbm5vY2Vu
dCBjb3ZlcmluZyBtZXNzYWdlIHdhcyB3cml0dGVu
Lg0KKiBIaWRkZW4gbWVzc2FnZXMgb24gbWVzc2VuZ2VyJ3MgYm9keTogYWxzbyB1c2VkIGluIGFuY2llbt==
dCBHcmVlY2UuIEhlcm9kb3R1cyB0ZWxscyB0aGUgc3Rvcnkgb1==
ZiBhIG1lc3NhZ2UgdGF0dG9vZWQgb24gYSBzbGF2ZSdzIHNoYXZlZCBoZWFkLCBoaWRkZW4gYnkgdGhl
IGdyb3d0aCBvZiBoaXMgaGFpciwgYW5kIGV4cG9zZWQgYnkgc2hhdmluZyBoaXMgaGVhZM==
IGFnYWluLiBUaGUgbWVzc2FnZSBhbGxlZ2VkbHkgY2FycmllZCBhIHdhcm5pbmcgdG8gR3JlZWNlIGFib5==
dXQgUGVyc2lhbiBpbnZhc2lvbiBwbGFucy4gVGh=
aXMgbWV0aG9kIGhhcyBvYnZpb3VzIGRyYXdiYWNrcyz=
IHN1Y2ggYXMgZGVsYXllZCB0cmFuc21pc3Npb24gd2hpbGUgd2FpdGluZyBmb3IgdGhlIHP=
bGF2ZSdzIGhhaXIgdG8gZ3JvdywgYW5kIHRoZSByZXN0cmljdGlvbnMgb3==
biB0aGUgbnVtYmVyIGFuZCBzaXplIG9mIG1lc3M=
YWdlcyB0aGF0IGNhbiBiZSBlbmNvZGVkIG9uIG9uZSBwZXJzb24=
J3Mgc2NhbHAuDQoqIEluIFdXSUksIHRoZSBGcmVuY2ggUmVzaXN0YW5jZSBzZW50IHNvbWUgbWVzc2FnZXMgd2==
cml0dGVuIG9uIHRoZSBiYWNrcyBvZiBjb3VyaWVycyD=
dXNpbmcgaW52aXNpYmxlIGluay4NCiogSGlkZGVuIG1lc3NhZ2VzIG9uIHBhcGVyIHdy
aXR0ZW4gaW4gc2VjcmV0IGlua3MsIHVuZGVyIG90aGVyIG1lc3NhZ2Vz
IG9yIG9uIHRoZSBibGFuayBwYXJ0cyBvZiBvdGhlct==
IG1lc3NhZ2VzLg0KKiBNZXNzYWdlcyB3cml0dGVuIGluIE1vcnNlIGNvZGUgb24ga25pdHRpbmcgeWFybiBhbmQg
dGhlbiBrbml0dGVkIGludG8gYSBwaWVjZSBvZiBjbG90aGluZyB3b3K=
biBieSBhIGNvdXJpZXIuDQoqIE1lc3NhZ2VzIHdyaXR0ZW4gb24gdGhlIGJhY2sgb5==
ZiBwb3N0YWdlIHN0YW1wcy4NCiogRHVyaW5nIGFuZCBhZnRlcm==
IFdvcmxkIFdhciBJSSwgZXNwaW9uYWdlIGFnZW50cyB1c2VkIHBob3RvZ3JhcGhpY2FsbHkgcO==
cm9kdWNlZCBtaWNyb2RvdHMgdG8gc2VuZCBpbmZvcm1hdGlvbiBiYWNrIGFuZH==
IGZvcnRoLiBNaWNyb2RvdHMgd2VyZSB0eXBpY2FsbHkg
bWludXRlLCBhcHByb3hpbWF0ZWx5IGxlc3MgdGhhbiB0aGUgc2l6ZSBvZiB0aGUgcGVyaW9kIHByb2R=
dWNlZCBieSBhIHR5cGV3cml0ZXIuIFdXSUkgbWljcm9kb3RzIG5lZWRlZCB0byBiZSBlbWJlZGRlZB==
IGluIHRoZSBwYXBlciBhbmQgY292ZXJlZCB3aXRoIGFuIGFkaGVzaXZlIChzdWNoIGFzIGNvbGxvZGlvbikuIFR=
aGlzIHdhcyByZWZsZWN0aXZlIGFuZCB0aHVzIGRldGVjdGFibGUg
Ynkgdmlld2luZyBhZ2FpbnN0IGdsYW5jaW5nIGxpZ2h0LiBBbHRlcm5hdGl2ZSB0ZWNobmlxdWVzIGluY2x1ZGVk
IGluc2VydGluZyBtaWNyb2RvdHMgaW50byBzbGl0cyBjdXQgaW50byB0aGUgZWRnZSBvZv==
IHBvc3QgY2FyZHMuDQoqIER1cmluZyBXb3JsZCBXYXIgSUksIGEgc3B5IGZvciB=
SmFwYW4gaW4gTmV3IFlvcmsgQ2l0eSwgVmVsdmFsZWW=
IERpY2tpbnNvbiwgc2VudCBpbmZvcm1hdGlvbiB0byBhY2NvbW1vZGF0aW9=
biBhZGRyZXNzZXMgaW4gbmV1dHJhbCBTb3V0aCBBbWVyaWO=
YS4gU2hlIHdhcyBhIGRlYWxlciBpbiBkb2xscywgYW5kIG==
aGVyIGxldHRlcnMgZGlzY3Vzc2VkIGhvdyBtYW55IG9mIHRoaXMgb3IgdGhhdCBkb2xs
IHRvIHNoaXAuIFRoZSBzdGVnb3RleHQgd2FzIHRoZSBkb2xsIG9yZGVycywgd2hpbGUgdGhl
IGNvbmNlYWxlZCAicGxhaW50ZXh0IiB3YXMgaXRzZWxmIGVuY2+=
ZGVkIGFuZCBnYXZlIGluZm9ybWF0aW9uIGFib3V0IHNoaXAgbW92ZW1lbnRzLF==
IGV0Yy4gSGVyIGNhc2UgYmVjYW1lIHNvbWV3aGF0IGZh
bW91cyBhbmQgc2hlIGJlY2FtZSBrbm93biBhcyB0aGX=
IERvbGwgV29tYW4uDQoqIENvbGQgV2FyIGNvdW50
ZXItcHJvcGFnYW5kYS4gSW4gMTk2OCwgY3JldyBtZW1iZW==
cnMgb2YgdGhlIFVTUyBQdWVibG8gKEFHRVItMikgaW50ZWxsaWdlbmNlIHNoaXAgaGVsZCBhcyBwcm==
aXNvbmVycyBieSBOb3J0aCBLb3JlYSwgY29tbXVuaWNhdGVkIGluIHNpZ25=
IGxhbmd1YWdlIGR1cmluZyBzdGFnZWQgcGhvdG8gb3Bwb3J0
dW5pdGllcywgaW5mb3JtaW5nIHRoZSBVbml0ZWQgU3RhdGVzIHRoZXkg
d2VyZSBub3QgZGVmZWN0b3JzIGJ1dCByYXRoZXIgd2VyZSBiZWluZyBoZWxkIGNh
cHRpdmUgYnkgdGhlIE5vcnRoIEtvcmVhbnMuIEluIG90aGVyIHBob3Rv
cyBwcmVzZW50ZWQgdG8gdGhlIFVTLCBjcmV3IG1lbWJlcnMgZ2F2ZSAidGhlIGZpbmdlciIgdG8g
dGhlIHVuc3VzcGVjdGluZyBOb3J0aCBLb3JlYW5zLCBpbiBhbiBhdHRlbXB0IHRvIE==
ZGlzY3JlZGl0IHBob3RvcyB0aGF0IHNob3dlZCB0aGVtIHNtaQ==
bGluZyBhbmQgY29tZm9ydGFibGUuDQoNCi0tDQpodHRwOi8vZW4ud2lraXBlZGlhLm9yZw==
L3dpa2kvU3RlZ2Fub2dyYXBoeQ0K

"""
e = b.splitlines()
binstr = ""
base64 = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
for i in e:
    if i.find("==") > 0:
        temp = bin((base64.find(i[-3]) & 15))[2:]  # 取倒数第3个字符，在base64找到对应的索引数（就是编码数），取低4位，再转换为二进制字符
        binstr = binstr + "0" * (4 - len(temp)) + temp  # 二进制字符补高位0后，连接字符到binstr
    elif i.find("=") > 0:
        temp = bin((base64.find(i[-2]) & 3))[2:]  # 取倒数第2个字符，在base64找到对应的索引数（就是编码数），取低2位，再转换为二进制字符
        binstr = binstr + "0" * (2 - len(temp)) + temp  # 二进制字符补高位0后，连接字符到binstr
str = ""
for i in range(0, len(binstr), 8):
    str = str + chr(int(binstr[i:i + 8], 2))  # 从左到右，每取8位转换为ascii字符，连接字符到字符串
print(str)  # 结果是 Base_sixty_four_point_five转换为

```

得到flag。

### 12.功夫再高也怕菜刀

> 题目：解压后是一个PCAPNG文件，菜狗决定用菜刀和菜鸡决一死战

解答：

关于PCAPNG文件[pcapng 文件解析_wireshark文件及数据包操作_爱学习的狮子的博客-CSDN博客](https://blog.csdn.net/weixin_36258891/article/details/112332822)

拖到kali中，使用binwalk发现流量包里有个Zip压缩包

```
binwalk 文件名
```

再使用dd命令分离文件

if=file：输入文件名，缺省为标准输入
of=file：输出文件名，缺省为标准输出
bs=bytes：同时设置读写块的大小为 bytes ，可代替 ibs 和 obs
skip=blocks：从输入文件开头跳过 blocks 个块后再开始复制

```
dd if=acfff53ce3fa4e2bbe8654284dfc18e1.pcapng of=flag bs=1 skip=1422689
```

of=flag，输出文件名为flag，Zip类型压缩包

![image-20220330173401025](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220330173401025.png)

打开flag压缩包，点击flag.txt，发现需要密码

使用wireshark分析，分组详情，字符串，flag.txt，查找

![image-20220330173550460](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220330173550460.png)

![image-20220330173607971](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220330173607971.png)

要查找到第1150个包时，追踪流才看到

FF D8是jpg文件的开头，FF D9是jpg文件的结尾，复制下来，再winhex中新建文件并粘贴，注意粘贴格式选择为ASCII Hex，保存为jpg文件格式得到一张jpg格式的图片

![image-20220330173901617](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220330173901617.png)

得到flag文件密码

输入后得flag

关于winhex[winhex使用简介_SpongeB0B的博客-CSDN博客_winhex](https://blog.csdn.net/john_david_/article/details/87274860)

关于binwalk、foremost、dd隐藏文件分离[binwalk、foremost、dd隐藏文件分离_啾啾啾七的博客-CSDN博客_foremost分离](https://blog.csdn.net/qq_50785772/article/details/109271001)

关于文件头![img](https://img-blog.csdnimg.cn/img_convert/4c05af18e6009006cd7ff62c1c84169e.png)

参考：

[CTF学习-MISC杂项解题思路_菜鸟-传奇的博客-CSDN博客](https://caichuanqi.blog.csdn.net/article/details/119963209?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1.pc_relevant_paycolumn_v3&utm_relevant_index=2)

[CTF-misc(解题思路/做题经验)_hangshao0.0的博客-CSDN博客_ctf misc解题思路](https://blog.csdn.net/weixin_45254208/article/details/105427317)

