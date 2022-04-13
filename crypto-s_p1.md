# 攻防世界-crypto

## 一、sherlock

> 题目：附件下载下来，是英文原著小说，有几个大写的字母

### 1、知识补充

**用法: grep [选项]… 模式 [文件]…**
-E, --extended-regexp <模式> 是扩展正则表达式
-o, --only-matching 只显示行中非空匹配部分
[] #匹配一个指定范围内的字符，如’[Gg]rep’匹配Grep和grep。

**用法：tr [选项]… SET1 [SET2]**
-d, --delete delete characters in SET1, do not translate
#删除SET1中的字符，不进行翻译
\n 换行

### 2、解答

发现有重复出现的大写字母，且找几个看似乎是`zero`和`one`的重复出现。

在虚拟机利用命令

```
cat 文件名 | grep -Eo '[A-Z]' |tr -d '\n'
```

将大写字母提取出来，如下：

```
ZEROONEZEROZEROZEROZEROONEZEROZEROONEZEROZEROONEZEROZEROONEZEROONEZEROONEZEROONEZEROZEROZEROONEZEROONEZEROZEROONEONEZEROONEZEROZEROZEROZEROONEONEZEROONEZEROONEZEROONEZEROZEROZEROONEZEROZEROZEROONEONEZEROZEROONEONEONEONEZEROONEONEZEROONEONEZEROONEZEROZEROZEROZEROZEROONEONEZEROZEROZEROONEZEROONEONEZEROZEROONEZEROZEROZEROZEROONEONEZEROZEROONEONEZEROONEZEROONEONEONEONEONEZEROZEROONEONEZEROZEROZEROONEZEROONEONEZEROONEONEONEZEROZEROONEZEROONEONEONEONEONEZEROONEONEONEZEROZEROZEROZEROZEROONEONEZEROONEONEZEROZEROZEROZEROONEONEZEROONEZEROZEROZEROZEROONEONEZEROZEROZEROONEZEROONEONEZEROONEONEONEZEROZEROONEZEROONEONEONEONEONEZEROZEROONEONEZEROONEZEROONEZEROZEROONEONEZEROZEROZEROONEZEROZEROONEONEZEROONEONEONEZEROZEROONEONEZEROZEROONEONEZEROONEONEONEONEON
```

把0、1回代，回代代码如下：

```python
key1="ZEROONEZEROZEROZEROZEROONEZEROZEROONEZEROZEROONEZEROZEROONEZEROONEZEROONEZEROONEZEROZEROZEROONEZEROONEZEROZEROONEONEZEROONEZEROZEROZEROZEROONEONEZEROONEZEROONEZEROONEZEROZEROZEROONEZEROZEROZEROONEONEZEROZEROONEONEONEONEZEROONEONEZEROONEONEZEROONEZEROZEROZEROZEROZEROONEONEZEROZEROZEROONEZEROONEONEZEROZEROONEZEROZEROZEROZEROONEONEZEROZEROONEONEZEROONEZEROONEONEONEONEONEZEROZEROONEONEZEROZEROZEROONEZEROONEONEZEROONEONEONEZEROZEROONEZEROONEONEONEONEONEZEROONEONEONEZEROZEROZEROZEROZEROONEONEZEROONEONEZEROZEROZEROZEROONEONEZEROONEZEROZEROZEROZEROONEONEZEROZEROZEROONEZEROONEONEZEROONEONEONEZEROZEROONEZEROONEONEONEONEONEZEROZEROONEONEZEROONEZEROONEZEROZEROONEONEZEROZEROZEROONEZEROZEROONEONEZEROONEONEONEZEROZEROONEONEZEROZEROONEONEZEROONEONEONEONEONEZEROONE"
flag=""
i=0
while i<len(key1):
	if key1[i]=='Z'and key1[i+1]=='E'and key1[i+2]=='R'and key1[i+3]=='O':
		i+=4
		flag+='0'
	else:
		flag+='1'
		i+=3
print(flag)
```

得到结果

```
010000100100100101010100010100110100001101010100010001100111101101101000001100010110010000110011010111110011000101101110010111110111000001101100001101000011000101101110010111110011010100110001001101110011001101111101
```

再二进制转化成字符串[二进制到字符串转换器 (rapidtables.org)](https://www.rapidtables.org/zh-CN/convert/number/binary-to-string.html)

![image-20220402203534323](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220402203534323.png)

得到结果

### 3、注意

（1）注意区分摩斯电码和二进制，摩斯电码有分割线。

（2）虚拟机常用命令：

cd /home 进入 '/ home' 目录' 
cd .. 返回上一级目录 
cd ../.. 返回上两级目录 
cd 进入个人的主目录 
cd ~user1 进入个人的主目录 
cd - 返回上次所在的目录 
pwd 显示工作路径 
ls 查看目录中的文件 
ls -F 查看目录中的文件 
ls -l 显示文件和目录的详细资料 
ls -a 显示隐藏文件 
ls *[0-9]* 显示包含数字的文件名和目录名 
tree 显示文件和目录由根目录开始的树形结构
lstree 显示文件和目录由根目录开始的树形结构
mkdir dir1 创建一个叫做 'dir1' 的目录' 
mkdir dir1 dir2 同时创建两个目录 
mkdir -p /tmp/dir1/dir2 创建一个目录树 
rm -f file1 删除一个叫做 'file1' 的文件' 
rmdir dir1 删除一个叫做 'dir1' 的目录' 
rm -rf dir1 删除一个叫做 'dir1' 的目录并同时删除其内容 
rm -rf dir1 dir2 同时删除两个目录及它们的内容 
mv dir1 new_dir 重命名/移动 一个目录 
cp file1 file2 复制一个文件 
cp dir/* . 复制一个目录下的所有文件到当前工作目录 
cp -a /tmp/dir1 . 复制一个目录到当前工作目录 
cp -a dir1 dir2 复制一个目录 
ln -s file1 lnk1 创建一个指向文件或目录的软链接 
ln file1 lnk1 创建一个指向文件或目录的物理链接 
touch -t 0712250000 file1 修改一个文件或目录的时间戳 - (YYMMDDhhmm) 
file file1 outputs the mime type of the file as text 
iconv -l 列出已知的编码 
iconv -f fromEncoding -t toEncoding inputFile > outputFile creates a new from the given input file by assuming it is encoded in fromEncoding and converting it to toEncoding. 
find . -maxdepth 1 -name *.jpg -print -exec convert "{}" -resize 80x60 "thumbs/{}" \; batch resize files in the current directory and send them to a thumbnails directory (requires convert from Imagemagick) 

**文件搜索** 
find / -name file1 从 '/' 开始进入根文件系统搜索文件和目录 
find / -user user1 搜索属于用户 'user1' 的文件和目录 
find /home/user1 -name \*.bin 在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件 
find /usr/bin -type f -atime +100 搜索在过去100天内未被使用过的执行文件 
find /usr/bin -type f -mtime -10 搜索在10天内被创建或者修改过的文件 
find / -name \*.rpm -exec chmod 755 '{}' \; 搜索以 '.rpm' 结尾的文件并定义其权限 
find / -xdev -name \*.rpm 搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备 
locate \*.ps 寻找以 '.ps' 结尾的文件 - 先运行 'updatedb' 命令 
whereis halt 显示一个二进制文件、源码或man的位置 
which halt 显示一个二进制文件或可执行文件的完整路径 

**打包和压缩文件** 
bunzip2 file1.bz2 解压一个叫做 'file1.bz2'的文件 
bzip2 file1 压缩一个叫做 'file1' 的文件 
gunzip file1.gz 解压一个叫做 'file1.gz'的文件 
gzip file1 压缩一个叫做 'file1'的文件 
gzip -9 file1 最大程度压缩 
rar a file1.rar test_file 创建一个叫做 'file1.rar' 的包 
rar a file1.rar file1 file2 dir1 同时压缩 'file1', 'file2' 以及目录 'dir1' 
unrar x file1.rar 解压rar包 
tar -cvf archive.tar file1 创建一个非压缩的 tarball 
tar -cvf archive.tar file1 file2 dir1 创建一个包含了 'file1', 'file2' 以及 'dir1'的档案文件 
tar -tf archive.tar 显示一个包中的内容 
tar -xvf archive.tar 释放一个包 
tar -xvf archive.tar -C /tmp 将压缩包释放到 /tmp目录下 
tar -cvfj archive.tar.bz2 dir1 创建一个bzip2格式的压缩包 
tar -jxvf archive.tar.bz2 解压一个bzip2格式的压缩包 
tar -cvfz archive.tar.gz dir1 创建一个gzip格式的压缩包 
tar -zxvf archive.tar.gz 解压一个gzip格式的压缩包 
zip file1.zip file1 创建一个zip格式的压缩包 
zip -r file1.zip file1 file2 dir1 将几个文件和目录同时压缩成一个zip格式的压缩包 
unzip file1.zip 解压一个zip格式压缩包 

**查看文件内容** 
cat file1 从第一个字节开始正向查看文件的内容 
tac file1 从最后一行开始反向查看一个文件的内容 
more file1 查看一个长文件的内容 
less file1 类似于 'more' 命令，但是它允许在文件中和正向操作一样的反向操作 
head -2 file1 查看一个文件的前两行 
tail -2 file1 查看一个文件的最后两行 
tail -f /var/log/messages 实时查看被添加到一个文件中的内容 

**文本处理** 
cat file1 file2 ... | command <> file1_in.txt_or_file1_out.txt general syntax for text manipulation using PIPE, STDIN and STDOUT 
cat file1 | command( sed, grep, awk, grep, etc...) > result.txt 合并一个文件的详细说明文本，并将简介写入一个新文件中 
cat file1 | command( sed, grep, awk, grep, etc...) >> result.txt 合并一个文件的详细说明文本，并将简介写入一个已有的文件中 
grep Aug /var/log/messages 在文件 '/var/log/messages'中查找关键词"Aug" 
grep ^Aug /var/log/messages 在文件 '/var/log/messages'中查找以"Aug"开始的词汇 
grep [0-9] /var/log/messages 选择 '/var/log/messages' 文件中所有包含数字的行 
grep Aug -R /var/log/* 在目录 '/var/log' 及随后的目录中搜索字符串"Aug" 
sed 's/stringa1/stringa2/g' example.txt 将example.txt文件中的 "string1" 替换成 "string2" 
sed '/^/d' example.txt 从example.txt文件中删除所有空白行 
sed '/ *#/d; /^/d' example.txt 从example.txt文件中删除所有注释和空白行 
echo 'esempio' | tr '[:lower:]' '[:upper:]' 合并上下单元格内容 
sed -e '1d' result.txt 从文件example.txt 中排除第一行 
sed -n '/stringa1/p' 查看只包含词汇 "string1"的行 
sed -e 's/ *$//' example.txt 删除每一行最后的空白字符 
sed -e 's/stringa1//g' example.txt 从文档中只删除词汇 "string1" 并保留剩余全部 
sed -n '1,5p;5q' example.txt 查看从第一行到第5行内容 
sed -n '5p;5q' example.txt 查看第5行 
sed -e 's/00*/0/g' example.txt 用单个零替换多个零 
cat -n file1 标示文件的行数 
cat example.txt | awk 'NR%2==1' 删除example.txt文件中的所有偶数行 
echo a b c | awk '{print 1}' 查看一行第一栏 
echo a b c | awk '{print 1,3}' 查看一行的第一和第三栏 
paste file1 file2 合并两个文件或两栏的内容 
paste -d '+' file1 file2 合并两个文件或两栏的内容，中间用"+"区分 
sort file1 file2 排序两个文件的内容 
sort file1 file2 | uniq 取出两个文件的并集(重复的行只保留一份) 
sort file1 file2 | uniq -u 删除交集，留下其他的行 
sort file1 file2 | uniq -d 取出两个文件的交集(只留下同时存在于两个文件中的文件) 
comm -1 file1 file2 比较两个文件的内容只删除 'file1' 所包含的内容 
comm -2 file1 file2 比较两个文件的内容只删除 'file2' 所包含的内容 
comm -3 file1 file2 比较两个文件的内容只删除两个文件共有的部分 

参考:[Linux常用命令大全（非常全！！！） - fcyh - 博客园 (cnblogs.com)](https://www.cnblogs.com/yjd_hycf_space/p/7730690.html)

## 二、flag_in_your_hand

> 题目：解压文件后有一个html页面，和一个javascript源文件

### 1、知识补充

暂无

### 2、解答

进入网页，发现只有ic=true才可以出现flag

![image-20220402204526440](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220402204526440.png)

查看源码，看到和ic相关的源码，和一串疑似token的数组

![image-20220402204632263](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220402204632263.png)

则a数组的每一个元素减去3，再转换成对应的字符，就可以得到token的值，使得ic=true

以下为转换代码：

```python
a=[118, 104, 102, 120, 117, 108, 119, 124, 48, 123, 101, 120]
s=''
for i in a:
	s+=chr(i-3)
print(s)
```

得到token:security-xbu

![image-20220402204932862](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220402204932862.png)

### 3、注意

注意查看网页源码，关注疑似密码数字或字符串

## 三、告诉你个秘密

> 题目：下载附件，是两串数

### 1、知识补充

暂无

### 2、解答

打开是两串16进制

```
636A56355279427363446C4A49454A7154534230526D6843
56445A31614342354E326C4B4946467A5769426961453067
```

16进制转换ASCII

```
cjV5RyBscDlJIEJqTSB0RmhCVDZ1aCB5N2lKIFFzWiBiaE0g
```

很明显是base64加密，再解密得

```
r5yG lp9I BjM tFhBT6uh y7iJ QsZ bhM 
```

一开始不知道这是个啥，查资料后，原来是按键盘上的分布，每四个包着一个按键，把每个包的中间的输出并大写即得到答案

### 3、注意

注意一些奇奇怪怪的解答方式（）

## 四、你猜猜

> 题目：我们刚刚拦截了，敌军的文件传输获取一份机密文件，请君速速破解。

### 1、知识补充

利用文件开头判断文件类型：[利用文件头标志判断文件类型 - maxiongying - 博客园 (cnblogs.com)](https://www.cnblogs.com/senior-engineer/p/9541719.html)

判断zip文件加密真伪：[(1条消息) 判断zip文件加密的真假_心bor的博客-CSDN博客](https://blog.csdn.net/qq_42667177/article/details/116646338)

关于伪加密：[(1条消息) 判断zip文件加密的真假_心bor的博客-CSDN博客](https://blog.csdn.net/qq_42667177/article/details/116646338)

### 2、解答

文件下载下来是一串看起来像16进制的数

```
504B03040A0001080000626D0A49F4B5091F1E0000001200000008000000666C61672E7478746C9F170D35D0A45826A03E161FB96870EDDFC7C89A11862F9199B4CD78E7504B01023F000A0001080000626D0A49F4B5091F1E00000012000000080024000000000000002000000000000000666C61672E7478740A0020000000000001001800AF150210CAF2D1015CAEAA05CAF2D1015CAEAA05CAF2D101504B050600000000010001005A000000440000000000
```

送到16进制转ASCII解码

```
PK
bm
Iôµ	flag.txtl
5Ð¤X& >¹hpíßÇÈ/´ÍxçPK?
bm
Iôµ	$ flag.txt
 ¯ÊòÑ\®ªÊòÑ\®ªÊòÑPKZD
```

一堆乱码，但看到了`flag.txt`，结合开头504B0304，猜测这是一个zip的二进制数据

**此时判断该zip是真加密还是假加密：**

1.压缩源文件目录区的标记第二位是奇数：01 08

![img](https://img-blog.csdnimg.cn/20200702161500285.png)

2.压缩源文件数据区标记第二位是奇数：01 08

![img](https://img-blog.csdnimg.cn/20200702161631332.png)

尝试将其修改为偶数失败，真加密实锤了。

打开winhex64复制粘贴成zip文件，但打开时显示文件已破损，修复后，需要解密密码才可以看到flag，利用Ziperello穷举解密，得到密码123456，于是得到flag

### 3、注意

识别文件头，巧用Ziperello减少穷举时间

## 五、Broadcast

> 题目：粗心的Alice在制作密码的时候，把明文留下来，聪明的你能快速找出来吗？

### 1、知识补充

暂无

### 2、解答

打开附件task.py文件，果然答案就在里面

![image-20220402211204336](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220402211204336.png)

### 3、注意

暂无

## 六、工业协议分析2

> 题目：在进行工业企业检查评估工作中，发现了疑似感染恶意软件的上位机。现已提取出上位机通信流量，尝试分析出异常点，获取FLAG。 flag形式为 flag{}

### 1、知识补充

暂无

### 2、解答

下载下来是个PCAPNG文件，拖到虚拟机去，查看文件长度，发现大部分重复，极个别单独出现一次

![image-20220402212027903](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220402212027903.png)



找到一处带有一串字符的，复制下来，发现最大不超过f，猜测是16进制，将其转成字符串

```
666c61677b37466f4d3253746b6865507a7d
flag{7FoM2StkhePz}
```

### 3、注意

查找时可关注文件大小、长度

## 七、cr3-what-is-this-encryption

> 题目：Fady同学以为你是菜鸟，不怕你看到他发的东西。他以明文形式将下面这些东西发给了他的朋友 p=0xa6055ec186de51800ddd6fcbf0192384ff42d707a55f57af4fcfb0d1dc7bd97055e8275cd4b78ec63c5d592f567c66393a061324aa2e6a8d8fc2a910cbee1ed9 q=0xfa0f9463ea0a93b929c099320d31c277e0b0dbc65b189ed76124f5a1218f5d91fd0102a4c8de11f28be5e4d0ae91ab319f4537e97ed74bc663e972a4a9119307 e=0x6d1fdab4ce3217b3fc32c9ed480a31d067fd57d93a9ab52b472dc393ab7852fbcb11abbebfd6aaae8032db1316dc22d3f7c3d631e24df13ef23d3b381a1c3e04abcc745d402ee3a031ac2718fae63b240837b4f657f29ca4702da9af22a3a019d68904a969ddb01bcf941df70af042f4fae5cbeb9c2151b324f387e525094c41 c=0x7fe1a4f743675d1987d25d38111fae0f78bbea6852cba5beda47db76d119a3efe24cb04b9449f53becd43b0b46e269826a983f832abb53b7a7e24a43ad15378344ed5c20f51e268186d24c76050c1e73647523bd5f91d9b6ad3e86bbf9126588b1dee21e6997372e36c3e74284734748891829665086e0dc523ed23c386bb520 他严重低估了我们的解密能力

### 1、知识补充

暂无

### 2、解答

有p,q,e,n,c，就是RSA，可以用虚拟机的工具，也可用脚本，这次用代码

```Python
import libnum
from Crypto.Util.number import long_to_bytes

q = int("0xa6055ec186de51800ddd6fcbf0192384ff42d707a55f57af4fcfb0d1dc7bd97055e8275cd4b78ec63c5d592f567c66393a061324aa2e6a8d8fc2a910cbee1ed9",16)
p = int("0xfa0f9463ea0a93b929c099320d31c277e0b0dbc65b189ed76124f5a1218f5d91fd0102a4c8de11f28be5e4d0ae91ab319f4537e97ed74bc663e972a4a9119307",16)

e = int("0x6d1fdab4ce3217b3fc32c9ed480a31d067fd57d93a9ab52b472dc393ab7852fbcb11abbebfd6aaae8032db1316dc22d3f7c3d631e24df13ef23d3b381a1c3e04abcc745d402ee3a031ac2718fae63b240837b4f657f29ca4702da9af22a3a019d68904a969ddb01bcf941df70af042f4fae5cbeb9c2151b324f387e525094c41",16)

c = int("0x7fe1a4f743675d1987d25d38111fae0f78bbea6852cba5beda47db76d119a3efe24cb04b9449f53becd43b0b46e269826a983f832abb53b7a7e24a43ad15378344ed5c20f51e268186d24c76050c1e73647523bd5f91d9b6ad3e86bbf9126588b1dee21e6997372e36c3e74284734748891829665086e0dc523ed23c386bb520",16)

n = q*p
 
d = libnum.invmod(e, (p - 1) * (q - 1))
m = pow(c, d, n)  
string = long_to_bytes(m)  
print(string)
```

得到答案

### 3、注意

先把16进制转化成10进制在计算

## 八、banana-princess

> 题目：下载下来是个损坏的pdf

### 1、知识补充

损坏的pdf试着使用notepad++打开

![image-20220405130216794](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220405130216794.png)

看不出什么，再打开一个正常的pdf对比，发现开头就不一样

|   这个   |   正常   |
| :------: | :------: |
| %CQS-1.5 | %PDF-1.7 |

感觉像是进行了移位

![image-20220405130728935](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220405130728935.png)

确实是移位，还是13，想到rot13

再随机找个字符测试

![image-20220405130840940](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220405130840940.png)

对整个pdf进行rot解密

```
cat 9e45191069704531accd66f1ee1d5b2b.pdf | tr 'A-Za-z' 'N-ZA-Mn-za-m' > new.pdf
```

得到flag被挡住的图片，使用pdftohtml命令转化图片，得到结果

![image-20220405131640000](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220405131640000.png)

![image-20220405131701560](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220405131701560.png)

## 九、flag_in_your_hand1

> 题目重了，见二

## 十、Decrypt-the-Message

> 题目：解密这段信息！
>
> The life that I have
> Is all that I have
> And the life that I have
> Is yours.
>
> The love that I have
> Of the life that I have
> Is yours and yours and yours.
>
> A sleep I shall have
> A rest I shall have
> Yet death will be but a pause.
>
> For the peace of my years
> In the long green grass
> Will be yours and yours and yours.
>
> decrypted message: emzcf sebt yuwi ytrr ortl rbon aluo konf ihye cyog rowh prhj feom ihos perp twnb tpak heoc yaui usoa irtd tnlu ntke onds goym hmpq

### 1、知识补充

① 给出一首诗歌

> for my purpose holds to sail beyond the sunset, and the baths of all the western stars until I die.

② 给出5个关键单词。

> “for”, “sail”, “all”, “stars”, “die.”

对其进行拆散：

> f o r s a i l a l l s t a r s d i e

接下来按照 字母表顺序 进行编号，若遇相同字母，则继续 +1

|   f   |   o   |   r   |   s   |   a   |   i   |   l   |   a   |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|   6   |  12   |  13   |  15   |   1   |   7   |   9   |   2   |
| **l** | **l** | **s** | **t** | **r** | **r** | **s** | **d** |
|  10   |  11   |  16   |  18   |  14   |  14   |  17   |   4   |
| **i** | **e** |       |       |       |       |       |       |
|   8   |   5   |       |       |       |       |       |       |

③ 将要传递的消息进行加密。

> We have run out of cigars, situation desperate。

先对对其进行编码。因为给出的5个关键词，其长度为18.所以以18为一组。

若一组长度不满18，则用abc(不要求有序)进行补充。

![img](https://img-blog.csdnimg.cn/2020081519575793.png#pic_center)

将排好的消息，按照之前给出的诗歌字母编号写下密文。

> for my purpose holds to sail beyond the sunset, and the baths of all the western stars until I die.

如， for --> eud tdk oek 那么得到的又可以按照5个（适当个数）为一组进行重新分组，得到最后密文。

参考：[Poem Codes – William M. Briggs (wmbriggs.com)](http://www.wmbriggs.com/post/1001/)

### 2、解答

先将诗歌和信息分开存成文本，把标点去掉，和以下代码放在同一文件夹下，运行代码(虚拟机)即得到代码

```python
import sys
import itertools
from os import listdir
from os.path import isfile, join

abc='abcdefghijklmnopqrstuvwxyz'

def loadlist(infile):
	tlist = []
	for line in open(infile,'r'):
		for w in line.split(): tlist.append(w.lower())
	return tlist

def encrypt(code, poem, msg):
	# Load all words of the poem into a temporary list
	twords = loadlist(poem)

	# Select only those words specified in the code in a new list
	pwords = ''
	for c in code: pwords += twords[c].lower()
	plen = len(pwords)

	# We can only support encoding all alphabetical letters, a key length greater len(abc) is not reasonable here
	if plen > len(abc): sys.exit(3)

	# Assign an index for each letter in the key based on the alphabet
	pcode = [None] * plen
	count = 0
	while(count<plen):
		for al in abc:
			for pc, pl in enumerate(pwords):
				if al!=pl: continue
				pcode[pc]=count
				count+=1

	# Load all words of the message into a string
	mwords = ''
	for line in open(msg, 'r'):
		for w in line.split(): mwords+=w.lower()
	mlen = len(mwords)

	# Split message into chunks of size plen, append random (here alphabet) characters to fill the last chunk, if necessary
	cpairs = []
	curlen = plen
	while(curlen<mlen):
		cpairs.append(mwords[curlen-plen:curlen])
		curlen+=plen
	rword = mwords[curlen-plen:curlen]
	rlen = len(rword)
	if rlen < plen: rword += abc[:plen-rlen]
	cpairs.append(rword)

	# Encrypt the message according to the key
	cip = ''
	for i in code: cip+=abc[i]
	cip+=' '
	for i in pcode:
		for pair in cpairs:
			cip += pair[i]
		cip+=' '
	return cip

def decrypt(poem, cip):
	# Load all words of the poem into a temporary list
	twords = loadlist(poem)

	# Load all cipher chunks of the ciphertext into a list
	cwords = loadlist(cip)

	# Get the code rom the first chunk and remove it from the ciphertext list
	code = []
	for i in cwords.pop(0):
		code.append(abc.index(i))
	
	# Select only those words specified in the code in a new multi-arrayed list
	xwords = [[] for x in range(len(code))]
	for xcount, c in enumerate(code):
		tlen = c
		while(c<len(twords)):
			xwords[xcount].append(twords[c].lower())
			c+=26

	# Get all possible combinations
	for comb in itertools.product(*xwords):
		pwords = ''
		for c in comb: pwords+=c
		plen = len(pwords)

		# Rearrange the chunks according to the key
		pcode = [None] * plen
		count = 0
		while(count<plen):
			for al in abc:
				for pc, pl in enumerate(pwords):
					if al!=pl: continue
					pcode[count]=cwords[pc]
					count+=1

		# Decrypt the ciphertext
		msg = ''
		wlen = len(pcode[0])
		for c in range(0, wlen):
			for word in pcode:
				msg+=word[c]
		print (msg)

# first argument = poem
# second argument = ciphertxt or msg
if len(sys.argv) != 3:
    sys.exit(2)

#print encrypt([0, 5, 13, 16, 19], sys.argv[1], sys.argv[2])
decrypt(sys.argv[1], sys.argv[2])
```

得到答案

### 3、注意

对于诗歌加密的理解

## 十一、OldDriver

> 题目：有个年轻人得到了一份密文，身为老司机的你能帮他看看么？
>
> [{"c": 7366067574741171461722065133242916080495505913663250330082747465383676893970411476550748394841437418105312353971095003424322679616940371123028982189502042, "e": 10, "n": 25162507052339714421839688873734596177751124036723831003300959761137811490715205742941738406548150240861779301784133652165908227917415483137585388986274803},
> {"c": 21962825323300469151795920289886886562790942771546858500842179806566435767103803978885148772139305484319688249368999503784441507383476095946258011317951461, "e": 10, "n": 23976859589904419798320812097681858652325473791891232710431997202897819580634937070900625213218095330766877190212418023297341732808839488308551126409983193},
> {"c": 6569689420274066957835983390583585286570087619048110141187700584193792695235405077811544355169290382357149374107076406086154103351897890793598997687053983, "e": 10, "n": 18503782836858540043974558035601654610948915505645219820150251062305120148745545906567548650191832090823482852604346478335353784501076761922605361848703623},
> {"c": 4508246168044513518452493882713536390636741541551805821790338973797615971271867248584379813114125478195284692695928668946553625483179633266057122967547052, "e": 10, "n": 23383087478545512218713157932934746110721706819077423418060220083657713428503582801909807142802647367994289775015595100541168367083097506193809451365010723},
> {"c": 22966105670291282335588843018244161552764486373117942865966904076191122337435542553276743938817686729554714315494818922753880198945897222422137268427611672, "e": 10, "n": 31775649089861428671057909076144152870796722528112580479442073365053916012507273433028451755436987054722496057749731758475958301164082755003195632005308493},
> {"c": 17963313063405045742968136916219838352135561785389534381262979264585397896844470879023686508540355160998533122970239261072020689217153126649390825646712087, "e": 10, "n": 22246342022943432820696190444155665289928378653841172632283227888174495402248633061010615572642126584591103750338919213945646074833823905521643025879053949},
> {"c": 1652417534709029450380570653973705320986117679597563873022683140800507482560482948310131540948227797045505390333146191586749269249548168247316404074014639, "e": 10, "n": 25395461142670631268156106136028325744393358436617528677967249347353524924655001151849544022201772500033280822372661344352607434738696051779095736547813043},
> {"c": 15585771734488351039456631394040497759568679429510619219766191780807675361741859290490732451112648776648126779759368428205194684721516497026290981786239352, "e": 10, "n": 32056508892744184901289413287728039891303832311548608141088227876326753674154124775132776928481935378184756756785107540781632570295330486738268173167809047},
> {"c": 8965123421637694050044216844523379163347478029124815032832813225050732558524239660648746284884140746788823681886010577342254841014594570067467905682359797, "e": 10, "n": 52849766269541827474228189428820648574162539595985395992261649809907435742263020551050064268890333392877173572811691599841253150460219986817964461970736553},
> {"c": 13560945756543023008529388108446940847137853038437095244573035888531288577370829065666320069397898394848484847030321018915638381833935580958342719988978247, "e": 10, "n": 30415984800307578932946399987559088968355638354344823359397204419191241802721772499486615661699080998502439901585573950889047918537906687840725005496238621}]

### 1、知识补充

**低加密指数广播攻击特点：**

（1）加密指数e非常小
（2）一份明文使用不同的模数n，相同的加密指数e进行多次加密
（3）可以拿到每一份加密后的密文和对应的模数n、加密指数e

**识别：n非常大,e一般很小。**

参考：

[CTF中RSA攻击方法总结 - 简书 (jianshu.com)](https://www.jianshu.com/p/dda528239554)

[ctf中rsa攻击方法 - 11223326 - 博客园 (cnblogs.com)](https://www.cnblogs.com/GH-D/p/11544589.html)

[CTF中的RSA套路之低加密指数攻击攻击和低解密指数攻击_KogRow的博客-CSDN博客_低加密指数攻击](https://blog.csdn.net/shuaicenglou3032/article/details/119930783)

### 2、解答

直接套用代码

```python
import gmpy2
import libnum
c1=gmpy2.mpz(7366067574741171461722065133242916080495505913663250330082747465383676893970411476550748394841437418105312353971095003424322679616940371123028982189502042)
n1=gmpy2.mpz(25162507052339714421839688873734596177751124036723831003300959761137811490715205742941738406548150240861779301784133652165908227917415483137585388986274803)
c2=gmpy2.mpz(21962825323300469151795920289886886562790942771546858500842179806566435767103803978885148772139305484319688249368999503784441507383476095946258011317951461)
n2=gmpy2.mpz(23976859589904419798320812097681858652325473791891232710431997202897819580634937070900625213218095330766877190212418023297341732808839488308551126409983193)
c3=gmpy2.mpz(6569689420274066957835983390583585286570087619048110141187700584193792695235405077811544355169290382357149374107076406086154103351897890793598997687053983)
n3=gmpy2.mpz(18503782836858540043974558035601654610948915505645219820150251062305120148745545906567548650191832090823482852604346478335353784501076761922605361848703623)
c4=gmpy2.mpz(4508246168044513518452493882713536390636741541551805821790338973797615971271867248584379813114125478195284692695928668946553625483179633266057122967547052)
n4=gmpy2.mpz(23383087478545512218713157932934746110721706819077423418060220083657713428503582801909807142802647367994289775015595100541168367083097506193809451365010723)
c5=gmpy2.mpz(22966105670291282335588843018244161552764486373117942865966904076191122337435542553276743938817686729554714315494818922753880198945897222422137268427611672)
n5=gmpy2.mpz(31775649089861428671057909076144152870796722528112580479442073365053916012507273433028451755436987054722496057749731758475958301164082755003195632005308493)
c6=gmpy2.mpz(17963313063405045742968136916219838352135561785389534381262979264585397896844470879023686508540355160998533122970239261072020689217153126649390825646712087)
n6=gmpy2.mpz(22246342022943432820696190444155665289928378653841172632283227888174495402248633061010615572642126584591103750338919213945646074833823905521643025879053949)
c7=gmpy2.mpz(1652417534709029450380570653973705320986117679597563873022683140800507482560482948310131540948227797045505390333146191586749269249548168247316404074014639)
n7=gmpy2.mpz(25395461142670631268156106136028325744393358436617528677967249347353524924655001151849544022201772500033280822372661344352607434738696051779095736547813043)
c8=gmpy2.mpz(15585771734488351039456631394040497759568679429510619219766191780807675361741859290490732451112648776648126779759368428205194684721516497026290981786239352)
n8=gmpy2.mpz(32056508892744184901289413287728039891303832311548608141088227876326753674154124775132776928481935378184756756785107540781632570295330486738268173167809047)
c9=gmpy2.mpz(8965123421637694050044216844523379163347478029124815032832813225050732558524239660648746284884140746788823681886010577342254841014594570067467905682359797)
n9=gmpy2.mpz(52849766269541827474228189428820648574162539595985395992261649809907435742263020551050064268890333392877173572811691599841253150460219986817964461970736553)
c0=gmpy2.mpz(13560945756543023008529388108446940847137853038437095244573035888531288577370829065666320069397898394848484847030321018915638381833935580958342719988978247)
n0=gmpy2.mpz(30415984800307578932946399987559088968355638354344823359397204419191241802721772499486615661699080998502439901585573950889047918537906687840725005496238621)
e=10
M = n1*n2*n3*n4*n5*n6*n7*n8*n9*n0
m1 = M//n1
m2 = M//n2
m3 = M//n3
m4 = M//n4
m5 = M//n5
m6 = M//n6
m7 = M//n7
m8 = M//n8
m9 = M//n9
m0 = M//n0
t1 = c1*m1*gmpy2.invert(m1,n1)
t2 = c2*m2*gmpy2.invert(m2,n2)
t3 = c3*m3*gmpy2.invert(m3,n3)
t4 = c4*m4*gmpy2.invert(m4,n4)
t5 = c5*m5*gmpy2.invert(m5,n5)
t6 = c6*m6*gmpy2.invert(m6,n6)
t7 = c7*m7*gmpy2.invert(m7,n7)
t8 = c8*m8*gmpy2.invert(m8,n8)
t9 = c9*m9*gmpy2.invert(m9,n9)
t0 = c0*m0*gmpy2.invert(m0,n0)
x = (t1+t2+t3+t4+t5+t6+t7+t8+t9+t0) % M
m=gmpy2.iroot(x,e)
print(m)
m1=854589733786598088127099154138504953368140761371523704656865879247874533963639770706597129057405
print(hex(m1))
m2=0x666c61677b776f305f7468335f747234696e5f69355f6c656176316e675f6733745f6f6e5f69747d
flag=libnum.n2s(m2)
print(flag)
```

### 3、注意

总结学习几种rsa加密方法

## 十二、best_rsa

> 题目：解压后两个cipher两个publickey

### 1、知识补充

给出了2个公钥文件和和2个密文文件，用常规的RSA解密方式分别解密，解密失败（n为2048位难以分解）

猜想应该是同一个明文，使用了2个不同的公钥加密得到了不同的密文，对同一明文的多次加密使用相同的模数和不同的公钥指数可能导致**共模攻击**

**共模攻击适用情况：**

明文m、模数n相同，公钥指数e、密文c不同，gcd(e1,e2)==1也就是e1和e2互质

参考：

[【密码学RSA】共模攻击原理详解_已知e1*e2的共模攻击题_malloc_冲！的博客-CSDN博客_rsa共模攻击](https://blog.csdn.net/serendipity1130/article/details/120154534)

[RSA的共模攻击 - gwind - 博客园 (cnblogs.com)](https://www.cnblogs.com/gwind/p/8013154.html)

### 2、解答

使用脚本，把四个文件和脚本放到一起，运行的结果

```python
from Crypto.Util.number import long_to_bytes, bytes_to_long
from Crypto.PublicKey import RSA
from gmpy2 import gcd, invert


def egcd(a, b):
    if a == 0:
        return b, 0, 1
    else:
        g, y, x = egcd(b % a, a)
        return g, x - (b // a) * y, y


with open('publickey1.pem', 'rb') as f:
    f1 = f.read()
pub1 = RSA.importKey(f1)
# 拿到共模数
n = int(pub1.n)
# 拿到公钥e1
e1 = int(pub1.e)

with open('publickey2.pem', 'rb') as f:
    f2 = f.read()
pub2 = RSA.importKey(f2)

# 拿到公钥e2
e2 = int(pub2.e)

with open('cipher1.txt', 'rb') as f:
    c1 = f.read()
# 得到密文c1
c1 = bytes_to_long(c1)
print(c1)

with open('cipher2.txt', 'rb') as f:
    c2 = f.read()
# 得到密文c2
c2 = bytes_to_long(c2)
print(c2)

# 得到扩展欧几里得中的计算模系数
s = egcd(e1, e2)

s1 = s[1]
s2 = s[2]

# 避免负指数运算
if s1 < 0:
    s1 = -s1
    c1 = invert(c1, n)
elif s2 < 0:
    s2 = -s2
    c2 = invert(c2, n)

# 
m = pow(c1, s1, n) * pow(c2, s2, n) % n
print(m)
print(long_to_bytes(m).decode())

```

### 3、注意

注意几种常见rsa攻击的脚本

## 十三、shanghai

> 题目:打开是一个文本文件

### 1、知识补充

维吉尼亚密码：

![img](https://bkimg.cdn.bcebos.com/pic/58ee3d6d55fbb2fbf9e21dcb434a20a44723dc1a?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2U5Mg==,g_7,xp_5,yp_5/format,f_auto)

例如，假设明文为：
ATTACKATDAWN
选择某一关键词并重复而得到密钥，如关键词为LEMON时，密钥为：
LEMONLEMONLE
对于明文的第一个字母A，对应密钥的第一个字母L，于是使用表格中L行字母表进行加密，得到密文第一个字母L。类似地，明文第二个字母为T，在表格中使用对应的E行进行加密，得到密文第二个字母X。以此类推，可以得到：
明文：ATTACKATDAWN密钥：LEMONLEMONLE密文：LXFOPVEFRNHR
解密的过程则与加密相反。例如：根据密钥第一个字母L所对应的L行字母表，发现密文第一个字母L位于A列，因而明文第一个字母为A。密钥第二个字母E对应E行字母表，而密文第二个字母X位于此行T列，因而明文第二个字母为T。以此类推便可得到明文。

### 2、解答

题目提示为维吉尼亚密码，首先浏览文本，发现疑似flag的部分

```
jtcw, '{' vvj 'zvkvrmtudabiecveaaxpp' grq '}'
```

接下来就是找密钥

看文章：

**（1）大体猜测密钥**

文段里出现许多四位数字，显然是年份，那么在数字前面若是两个字母组成的单词，不难想到，就是“in”。比如第一段，有 “mv 1580”，第三段 “qp 1586”、第四段 “qp 1917”。

mv – ei qp – ic

注意到第五段的数字 “frxnimp 1914 qil 1940” ，像这种结构，不难想到是“between and”型。 frxnimp - between

qil - and 对此进行推算密钥。

frxnimp – enereic qil – qvi 因为between and 是连在一起的，那么现在已知的大致为 enereicqvi 顺序未定。

**（2）确定长度**

如何确定长度？最简单的办法，就是寻找相同长度的单词并且单词字母完全一致。

如：第四段最后一行 “opk gvtyiz kd opk 16xu gvrbwht.[6]” 。opk与opk，之间相差11，即为密钥长度。

由加密原理可知，改变的是偏移值，其单词长度不会发生改变。并且若加密结果相等，证明密钥恰好一致。间隔便为其密钥之长。 但我们手上掌握的却只有10位，因此，得继续寻找。

可以继续看这段话。 “16xu” 很像 “16th” 并且“opk”极有可能是“the”。来尝试一下

opk – vig xu – en 这样。密钥产生：enereicqvig （顺序未定）。
**（3）确定密钥**

1、来看第一段第一个单词。开头三个字母，可大致猜是 the ，推算一下 密钥： icq 。 恰好吻合。则真正的密钥便为： icqvigenere

将密钥和原文一并放入解密工具，产生原文。 解密网站[CTF在线工具-在线维吉尼亚密码加密|在线维吉尼亚解密|维吉尼亚密码算法|Vigenere Cipher (hiencode.com)](http://www.hiencode.com/vigenere.html)

然后在原文中查找。

2、在倒数第三段存在这样语句 ： jtcw, ‘{’ vvj ‘zvkvrmtudabiecveaaxpp’ grq ‘}’ 显然这就是 被加密的flag jtcw对用的就是flag。 那么用它推算一下：

jtcw – eicq 则直接对 jtcw, ‘{’ vvj ‘zvkvrmtudabiecveaaxpp’ grq ‘}’ 解密 。 密钥为：eicqvigener
![image-20220407200553642](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220407200553642.png)

### 3、注意

理解维吉尼亚密码的加密方式，和密钥的猜测

## 十四、RSA_gcd

> 题目:解压后时两个attach，有两个nce,且e相同

### 1、知识补充

暂无

### 2、解答

正常的RSA解密

```python
import gmpy2


def get_p(n1, n2):
    p = gmpy2.gcd(n1, n2)
    assert gmpy2.is_prime(p) == True
    return p

def int_str(data):
    flag = ''
    while data:
        flag += chr(data & 0xff)
        data >>= 8
    return flag[::-1]

if __name__ == "__main__":
    n1 = 23220619839642624127208804329329079289273497927351564011985292026254914394833691542552890810511751239656361686073628273309390314881604580204429708461587512500636158161303419916259271078173864800267063540526943181173708108324471815782985626723198144643256432774984884880698594364583949485749575467318173034467846143380574145455195152793742611717169602237969286580028662721065495380192815175057945420182742366791661416822623915523868590710387635935179876275147056396018527260488459333051132720558953142984038635223793992651637708150494964785475065404568844039983381403909341302098773533325080910057845573898984314246089
    n2 = 22642739016943309717184794898017950186520467348317322177556419830195164079827782890660385734113396507640392461790899249329899658620250506845740531699023854206947331021605746078358967885852989786535093914459120629747240179425838485974008209140597947135295304382318570454491064938082423309363452665886141604328435366646426917928023608108470382196753292656828513681562077468846105122812084765257799070754405638149508107463233633350462138751758913036373169668828888213323429656344812014480962916088695910177763839393954730732312224100718431146133548897031060554005592930347226526561939922660855047026581292571487960929911
    c1 = 9700614748413503291260966231863562117502096284616216707445276355274869086619796527618473213422509996843430296526594113572675840559345077344419098900818709577642324900405582499683604786981144099878021784567540654040833912063141709913653416394888766281465200682852378794478801329251224801006820925858507273130504236563822120838520746270280731121442839412258397191963036040553539697846535038841541209050503061001070909725806574230090246041891486506980939294245537252610944799573920844235221096956391095716111629998594075762507345430945523492775915790828078000453705320783486744734994213028476446922815870053311973844961
    c2 = 20513108670823938405207629835395350087127287494963553421797351726233221750526355985253069487753150978011340115173042210284965521215128799369083065796356395285905154260709263197195828765397189267866348946188652752076472172155755940282615212228370367042435203584159326078238921502151083768908742480756781277358357734545694917591921150127540286087770229112383605858821811640935475859936319249757754722093551370392083736485637225052738864742947137890363135709796410008845576985297696922681043649916650599349320818901512835007050425460872675857974069927846620905981374869166202896905600343223640296138423898703137236463508
    e = 65537
    p = get_p(n1, n2)
    q1 = n1 // p
    q2 = n2 // p
    d1 = gmpy2.invert(e, (p - 1) * (q1 - 1))
    d2 = gmpy2.invert(e, (p - 1) * (q2 - 1))
    m1 = gmpy2.powmod(c1, d1, n1)
    m2 = gmpy2.powmod(c2, d2, n2)
    print(int_str(m1) + int_str(m2))
```

### 3、注意

暂无

## 十五、equation-2

> 题目：Here is a RSA private key with its upper part masked. Can your recover the private key and decrypt the file?

### 1、知识补充

私钥信息按如下顺序排列：
version | pad | n | pad | e | pad | d | pad | p | pad | q | pad | x1 | pad | x2 | pad | x3
其中，pad是填充信息，各pad并不同，x1=d mod (p−1),x2=d mod (q−1),x3=p−1 mod qx1=d mod (p−1),x2=d mod (q−1),x3=p−1 mod q，填充pad用来注释接下来的大数的(字节)长度，\x02为pad开头的标记，有时后面接\x81或\x82，这用来标记长度值所占用的字节(\x81代表占用1个字节，\x82代表占用2个字节)，有时后面不接\x81或\x82而直接放置长度；
例：\x02\x03代表接下来的大数的字节长度为3个字节；\x02\x81\x80，首先，\x81代表长度占用1个字节，因此\x80就是长度值，即128，表明接下来的大数的字节长度为128个字节。

参考：[使用openssl命令剖析RSA私钥文件格式_Zhymax的博客-CSDN博客_rsa私钥格式](https://blog.csdn.net/Zhymax/article/details/7683925?ops_request_misc=%7B%22request%5Fid%22%3A%22164933609516782246494414%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=164933609516782246494414&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-1-7683925.142^v7^article_score_rank,157^v4^control&utm_term=OpenSSL私钥结构&spm=1018.2226.3001.4187)

### 2、解答

截图可见编码为（可用qq识字）

```Bash
Os9mhOQRdqW2cwVrnNI72DLcAXpXUJ1HGwJBANWiJcDUGxZpnERxVw7s0913WXNtV4GqdxCzG0pG5EHThtoTRbyX0aqRP4U/hQ9tRoSoDmBn+3HPITsnbCy67VkCQBM4xZPTtUKM6Xi+16VTUnFVs9E4rqwIQCDAxn9UuVMBXlX2Cl0xOGUF4C5hItrX2woF7LVS5EizR63CyRcPovMCQQDVyNbcWD7N88MhZjujKuSrHJot7WcCaRmTGEIJ6TkU8NWt9BVjR4jVkZ2EqNd0KZWdQPukeynPcLlDEkIXyaQx
```

base64脚本解码后解出x1,x2,x3

```python
import gmpy2
import base64
import sys

from Crypto.Util.number import isPrime, inverse
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_v1_5

s ='Os9mhOQRdqW2cwVrnNI72DLcAXpXUJ1HGwJBANWiJcDUGxZpnERxVw7s0913WXNtV4GqdxCzG0pG5EHThtoTRbyX0aqRP4U/hQ9tRoSoDmBn+3HPITsnbCy67VkCQBM4xZPTtUKM6Xi+16VTUnFVs9E4rqwIQCDAxn9UuVMBXlX2Cl0xOGUF4C5hItrX2woF7LVS5EizR63CyRcPovMCQQDVyNbcWD7N88MhZjujKuSrHJot7WcCaRmTGEIJ6TkU8NWt9BVjR4jVkZ2EqNd0KZWdQPukeynPcLlDEkIXyaQx'
print(base64.b64decode(s.encode('utf8')))
```

```
\xcff\x84\xe4\x11v\xa5\xb6s\x05k\x9c\xd2;\xd82\xdc\x01zWP\x9dG\x1b
\x02A\x00\xd5\xa2%\xc0\xd4\x1b\x16i\x9cDqW\x0e\xec\xd3\xddwYsmW\x81\xaaw\x10\xb3\x1bJF\xe4A\xd3\x86\xda\x13E\xbc\x97\xd1\xaa\x91?\x85?\x85\x0fmF\x84\xa8\x0e`g\xfbq\xcf!;\'l,\xba\xedY
\x02@\x138\xc5\x93\xd3\xb5B\x8c\xe9x\xbe\xd7\xa5SRqU\xb3\xd18\xae\xac\x08@ \xc0\xc6\x7fT\xb9S\x01^U\xf6\n]18e\x05\xe0.a"\xda\xd7\xdb\n\x05\xec\xb5R\xe4H\xb3G\xad\xc2\xc9\x17\x0f\xa2\xf3
\x02A\x00\xd5\xc8\xd6\xdcX>\xcd\xf3\xc3!f;\xa3*\xe4\xab\x1c\x9a-\xedg\x02i\x19\x93\x18B\t\xe99\x14\xf0\xd5\xad\xf4\x15cG\x88\xd5\x91\x9d\x84\xa8\xd7t)\x95\x9d@\xfb\xa4{)\xcfp\xb9C\x12B\x17\xc9\xa41
```

解码后结合OpenSSL私钥结构分析可得：x1,x2,x3为已知；但是仅有x1,x2,x3并不能恢复出p,q与d，若我们假设e为常用的指数3,65537等等，则可试出p与q：

d⋅e≡1 mod (p−1)(q−1)d⋅e≡1 mod (p−1)(q−1)
则有d⋅e≡1 mod (p−1)d⋅e≡1 mod (p−1)与d⋅e≡1 mod (q−1)d⋅e≡1 mod (q−1)；
由x1x1与x2x2的定义可得x1⋅e≡1 mod (p−1)x1⋅e≡1 mod (p−1)，x2⋅e≡1 mod (q−1)x2⋅e≡1 mod (q−1)；
因此(p−1)|(x1⋅e−1)(p−1)|(x1⋅e−1)；
记x1⋅e−1=r1⋅(p−1)x1⋅e−1=r1⋅(p−1)；
由于x1=d mod (p−1)x1=d mod (p−1)，则x1<(p−1)x1<(p−1)；
几乎可以看做x1⋅e=r1⋅(p−1)x1⋅e=r1⋅(p−1)，那么必有r1<er1<e；
同理可得r2<er2<e，其中x2⋅e−1=r2⋅(q−1)x2⋅e−1=r2⋅(q−1)
可以看到，ri<e,i=1,2ri<e,i=1,2，从而可使用试除法求出ri,i=1,2ri,i=1,2；
则p=(x1⋅e−1)/r1+1,q=(x2⋅e−1)/r2+1p=(x1⋅e−1)/r1+1,q=(x2⋅e−1)/r2+1；

解答脚本:

```python
import gmpy2
import base64
import sys

from Crypto.Util.number import isPrime, inverse
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_v1_5

def bytes_to_int(x):
    ans = 0
    for data in x:
        ans <<= 8
        ans += ord(data)
    return ans

x1 = bytes_to_int('\xd5\xa2%\xc0\xd4\x1b\x16i\x9cDqW\x0e\xec\xd3\xddwYsmW\x81\xaaw\x10\xb3\x1bJF\xe4A\xd3\x86\xda\x13E\xbc\x97\xd1\xaa\x91?\x85?\x85\x0fmF\x84\xa8\x0e`g\xfbq\xcf!;\'l,\xba\xedY')
x2 = bytes_to_int('\x138\xc5\x93\xd3\xb5B\x8c\xe9x\xbe\xd7\xa5SRqU\xb3\xd18\xae\xac\x08@ \xc0\xc6\x7fT\xb9S\x01^U\xf6\n]18e\x05\xe0.a"\xda\xd7\xdb\n\x05\xec\xb5R\xe4H\xb3G\xad\xc2\xc9\x17\x0f\xa2\xf3')
x3 = bytes_to_int('\xd5\xc8\xd6\xdcX>\xcd\xf3\xc3!f;\xa3*\xe4\xab\x1c\x9a-\xedg\x02i\x19\x93\x18B\t\xe99\x14\xf0\xd5\xad\xf4\x15cG\x88\xd5\x91\x9d\x84\xa8\xd7t)\x95\x9d@\xfb\xa4{)\xcfp\xb9C\x12B\x17\xc9\xa41')

def genKey(x1, x2, x3):
    e = 65537
    n1 = x1 * e - 1
    n2 = x2 * e - 1
    p = 0; q = 0
    # 尝试求 r1
    for r in range(e - 1, 0, -1):
        if n1 % r == 0:
            p = (n1 // r) + 1
            if gmpy2.is_prime(p):
                break
    # 尝试求 r2
    for r in range(e - 1, 0, -1):
        if n2 % r == 0:
            q = (n2 // r) + 1
            if gmpy2.is_prime(q):
                break
    print(p)
    print(q)
    n = p * q
    phi = (p - 1) * (q - 1)
    d = inverse(e, phi)
    assert inverse(q, p) == x3
    return RSA.construct((n, e, int(d), p, q))

def solve():
    rsa_key = genKey(x1, x2, x3)
    key = PKCS1_v1_5.new(rsa_key)
    with open('flag.enc', 'rb') as fp:
        return key.decrypt(fp.read(), '')
    
if __name__ == "__main__":
    print(solve()) 
```

### 3、注意

OpenSSL私钥结构分析！！！！

## 十六、streamgame2

> 题目：解压后一个key，一个.py文件
>
> ```python
> from flag import flag
> assert flag.startswith("flag{")
> assert flag.endswith("}")
> assert len(flag)==27
> 
> def lfsr(R,mask):
>     output = (R << 1) & 0xffffff
>     i=(R&mask)&0xffffff
>     lastbit=0
>     while i!=0:
>         lastbit^=(i&1)
>         i=i>>1
>     output^=lastbit
>     return (output,lastbit)
> 
> 
> 
> R=int(flag[5:-1],2)
> mask=0x100002
> 
> f=open("key","ab")
> for i in range(12):
>     tmp=0
>     for j in range(8):
>         (R,out)=lfsr(R,mask)
>         tmp=(tmp << 1)^out
>     f.write(chr(tmp))
> f.close()
> ```
>
> 

### 1、知识补充

线性反馈移位寄存器（LFSR）归属于移位寄存器（FSR）,除此之外还有非线性移位寄存器（NFSR）。移位寄存器是流密码产生密钥流的一个主要组成部分。

上一个n级反馈移位寄存器由n个二元存储器与一个反馈函数组成，如下图所示。

![img](https://img-blog.csdnimg.cn/img_convert/888b888831348fbde2bfc4d4e21b9e9a.png)

移位寄存器的三要素：

- 初始状态：由用户确定

- 反馈函数：是n元布尔函数，即函数的自变量和因变量只取0和1这两个可能值

- 输出序列


如果反馈函数是线性的，那么我们称其为 LFSR,如下图所示：

![img](https://img-blog.csdnimg.cn/img_convert/ca42f81f7acca6af8ded4e2d41e5a828.png)

LFSR的输出序列{ }满足:

.....

(i = 1,2,3,...)

举例：

下面是一个5级的线性反馈移位寄存器，其初始状态为

![img](https://img-blog.csdnimg.cn/img_convert/48e18970b863e34cd7062ac6866ef82a.png)

反馈函数为：，(i = 1,2,...) 可以得到输出序列为：

1001101001000010101110110001111 100110…

周期为31。

对于 n 级线性反馈移位寄存器，最长周期为（排除全零）。达到最长周期的序列一般称为 m 序列

参考：[CTF竞赛密码学 之 LFSR_合天网安实验室的博客-CSDN博客](https://blog.csdn.net/qq_38154820/article/details/115222774?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0.pc_relevant_default&spm=1001.2101.3001.4242.1&utm_relevant_index=3)

[CTF中的LFSR考点(一)_沐一 · 林的博客-CSDN博客](https://blog.csdn.net/xiao__1bai/article/details/120392307?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1.pc_relevant_default&utm_relevant_index=1)

[攻防世界streamgame1_I still …的博客-CSDN博客](https://blog.csdn.net/qq_44370676/article/details/109067035?ops_request_misc=%7B%22request%5Fid%22%3A%22164942102316782089373033%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=164942102316782089373033&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-109067035.142^v7^article_score_rank,157^v4^control&utm_term=streamgame&spm=1018.2226.3001.4187)

### 2、解答

爆破

```python
from Crypto.Util.number import*
bin_out = open('key','rb').read()
key = bin(bytes_to_long(bin_out))[2:]
# print(key[0:21])
# print(bin(int('0x100002',16)))
key = '101100101110100100001'
mask= '100000000000000000010'

tmp = key
R = ''
for i in range(21):
    output = '?' + key[:20]
    ans = int(tmp[-1-i]) ^ int(output[-2])
    R += str(ans)
    key = str(ans) + key[:20]

print(R[::-1])
```

### 3、注意

爆破和逆运算2种思路，还**未全部理解**

## 十七、streamgame1

> 题目：解压后一个key，一个.py文件
>
> ```python
> from flag import flag
> assert flag.startswith("flag{")
> # 作用：判断字符串是否以指定字符或子字符串开头flag{
> assert flag.endswith("}")
> # 作用：判断字符串是否以指定字符或子字符串结尾}，flag{}，6个字节
> assert len(flag)==25
> # flag的长度为25字节，25-6=19个字节
> #3<<2可以这么算，bin(3)=0b11向左移动2位变成1100，0b1100=12(十进制)
> def lfsr(R,mask):
>     output = (R << 1) & 0xffffff    #将R向左移动1位，bin(0xffffff)='0b111111111111111111111111'=0xffffff的二进制补码
>     i=(R&mask)&0xffffff             #按位与运算符&：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0
>     lastbit=0
>     while i!=0:
>         lastbit^=(i&1)    #按位异或运算符：当两对应的二进位相异时，结果为1
>         i=i>>1
>     output^=lastbit
>     return (output,lastbit)
> 
> 
> 
> R=int(flag[5:-1],2)
> mask    =   0b1010011000100011100
> 
> f=open("key","ab")   #以二进制追加模式打开
> for i in range(12):
>     tmp=0
>     for j in range(8):
>         (R,out)=lfsr(R,mask)
>         tmp=(tmp << 1)^out   #按位异或运算符：当两对应的二进位相异时，结果为1
>     f.write(chr(tmp))  #chr() 用一个范围在 range（256）内的（就是0～255）整数作参数，返回一个对应的字符。
> f.close()
> ```
>
> 

### 1、知识补充

见streamgame2

### 2、解答

```python
def lfsr(R,mask):
    output = (R << 1) &0xffffff
    i=(R&mask)&0xffffff
    lastbit=0
    while i!=0:
        lastbit^=(i&1)
        i=i>>1
    output^=lastbit
    return (output,lastbit)
 
key=[85,56,247,66,193,13,178,199,237,224,36,58]
mask=0b1010011000100011100
 
for k in range(2**19):
    R=k;
    a=''
    judge=1
    for i in range(12):
        tmp = 0
        for j in range(8):
            (k, out) = lfsr(k, mask)
            tmp = (tmp << 1) ^ out
        if(key[i]!=tmp):
           judge=0
           break
    if(judge==1):
        print ('flag{'+bin(R)[2:]+'}')
        break
```

### 3、注意

注意原理理解

## 十八、wtc_rsa_bbq

> 题目：解压后，一个cipher.bin、一个key.pem文件

### 1、知识补充

JPEG (jpg)，文件头：FFD8FF
PNG (png)，文件头：89504E47
GIF (gif)，文件头：47494638
TIFF (tif)，文件头：49492A00
Windows Bitmap (bmp)，文件头：424D
CAD (dwg)，文件头：41433130
Adobe Photoshop (psd)，文件头：38425053
Rich Text Format (rtf)，文件头：7B5C727466
XML (xml)，文件头：3C3F786D6C
HTML (html)，文件头：68746D6C3E
Email [thorough only] (eml)，文件头：44656C69766572792D646174653A
Outlook Express (dbx)，文件头：CFAD12FEC5FD746F
Outlook (pst)，文件头：2142444E
MS Word/Excel (xls.or.doc)，文件头：D0CF11E0
MS Access (mdb)，文件头：5374616E64617264204A
WordPerfect (wpd)，文件头：FF575043
Postscript (eps.or.ps)，文件头：252150532D41646F6265
Adobe Acrobat (pdf)，文件头：255044462D312E
Quicken (qdf)，文件头：AC9EBD8F
Windows Password (pwl)，文件头：E3828596
ZIP Archive (zip)，文件头：504B0304
RAR Archive (rar)，文件头：52617221
Wave (wav)，文件头：57415645
AVI (avi)，文件头：41564920
Real Audio (ram)，文件头：2E7261FD
Real Media (rm)，文件头：2E524D46
MPEG (mpg)，文件头：000001BA
MPEG (mpg)，文件头：000001B3
Quicktime (mov)，文件头：6D6F6F76
Windows Media (asf)，文件头：3026B2758E66CF11
MIDI (mid)，文件头：4D546864

参考：[根据文件头数据判断文件类型 - jack_Meng - 博客园 (cnblogs.com)](https://www.cnblogs.com/mq0036/p/3912355.html)

### 2、解答

一开始不知道是啥文件，放到winhex中看，是504B03开头（PK开头），得知是压缩文件，改后缀后解压，一个cipher.bin、一个key.pem文件

使用openssl查看公钥信息：

```
openssl rsa -pubin -in key.pem -text -modulus
```

发现模数很大，8587位；本来分解模数丢到yafu里面分解就行，但是几个小时都没有分解出来，去[factordb](http://factordb.com/)也分解不出来；回顾针对RSA的各种攻击，对本题可以使用的剩下Small q,费马分解(p与q接近)，试着用费马分解时分解成功。

使用 RSACTFTOOL，将key.pem与cipher.bin移到与RsaCtfTool.py同目录下：

```
sudo python3 RsaCtfTool.py --publickey key.pem --uncipherfile cipher.bin --attack fermat
```

![image-20220408210456005](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220408210456005.png)

### 3、注意

善用linux中的ctf工具

