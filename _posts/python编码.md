title: python字符编码问题
date: 2015-03-16
tags:
- python
categories: 技术记录
---

               Python字符串编码相关知识

-----------------------------------

<!-- more -->
### Python字符串编码

字符串在Python内部的表示是***unicode***编码，因此，在做编码转换时，通常需要以**unicode作为中间编码**，即先将其他编码的字符串解码（decode）成unicode，再从unicode编码（encode）成另一种编码。

 * decode的作用是将其他编码的字符串转换成unicode编码，如str1.decode('gb2312')，表示将gb2312编码的字符串str1转换成unicode编码。

 * encode的作用是将unicode编码转换成其他编码的字符串，如str2.encode('gb2312')，表示将unicode编码的字符串str2转换成gb2312编码。
 
因此，转码的时候一定要先搞明白，字符串str是什么编码，然后decode成unicode，然后再encode成其他编码代码中字符串的默认编码与代码文件本身的编码一致。
下面例子困扰很久，在做一个爬虫某网站的例子。一般网页编码是**utf-8**，windows终端是**gbk**?

    if platform.system() == "Windows":
        kw = raw_input("请输入关键字（多个关键字请以空格隔开）:".decode("utf-8").encode("gbk"))
        kw = kw.decode("gbk").encode("utf-8")

注意：kw为中文的输入关键字的话，是要提交至你要爬的网页，所以要转换成**utf-8**编码；上面先将已经是**gbk**编码的kw**decode**成Python内部***unicode***编码，然后再将**unicode**编码**encode**成网页**utf-8**编码的字符串。

### 字符编码知识梳理
UTF-8就是在互联网上使用最广的一种Unicode的实现方式;以下两点是UTF-8的编码规则


- 1）对于单字节的符号，字节的第一位设为0，后面7位为这个符号的unicode码。因此对于英语字母，UTF-8编码和ASCII码是相同的。


- 2) 对于n字节的符号（n>1），第一个字节的前n位都设为1，第n+1位设为0，后面字节的前两位一律设为10。剩下的没有提及的二进制位，全部为这个符号的unicode码。

综上：解读UTF-8编码非常简单。如果一个字节的第一位是0，则这个字节单独就是一个字符；如果第一位是1，则连续有多少个1，就表示当前字符占用多少个字节。