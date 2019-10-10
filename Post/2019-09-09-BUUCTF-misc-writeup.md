---
layout: post
title: "BUUCTF-MISC-WriteUp"
date: 2019-09-09 01:01:01
share: true
toc: true
tags: 
 - CTF
---

BUUCTF-MISC-WriteUp

## 签到
## 二维码
## 金三胖
## N种方法解决
## 大白
...重复题太多
## 后门查杀
- 用d盾扫一下得木马
- 查找password
- 加上flag{}

## 另外一个世界
- 丢进winhex得一堆二进制
- 直接Converter.exe转字符串
- 加上flag{}

## snake
- 丢进winhex末尾发现`V2hhdCBpcyBOaWNraSBNaW5haidzIGZhdm9yaXRlIHNvbmcgdGhhdCByZWZlcnMgdG8gc25ha2VzPwo=`
- 解码得`What is Nicki Minaj's favorite song that refers to snakes?` wtf？？
- 搜索这个歌手是这首歌`Anaconda `意思为大蟒蛇
- 丢进binwalk分离pk解压得cipher和key key得内容就是上述的base64编码 cipher意思为暗号
- http://serpent.online-domain-tools.com/ 可以在线解密 猜测加密方式为Serpent key为`anaconda`
- 得flag

## 九连环
拿到图片
- 丢进binwalk 有zip foremost出来
- 这个压缩包是伪加密 用winhex改或者直接binwalk -e(学到了)
- 得图片和一压缩包有密码（真压缩） 
- 这个图片binwalk没东西其实是有东西的 用工具`steghide`
```
steghide info good.jpg
steghide extract -sf good.jpg
```
- 没密码直接回车即可 得ko.txt这是压缩文件密码
- 解压得flag

## 面具下的flag
- 丢进binwalk有东西foremost
- 得flag.vmdk 这玩意是vm的文件但是可以用7z解压（学到了）
- 在kali解压`7z x filename.7z`在win下用7z解压不完整（不知原因）
- 得一堆文件其中`where_is_flag_part_two.txt:flag_part_two_is_here.txt`以及`_NUL`文件中含有Ook及brainfuck
- 解码拼起来得flag
- flag{N7F5_AD5_i5_funny!}

## Mysterious
这是一道逆向题
- 丢进od能查找出flag但是不对 因为缺少了一项
- 丢进ida看看定位到flag相关函数
```c
if ( v10 == 123 && v12 == 120 && v14 == 122 && v13 == 121 )
      {
        strcpy(Text, "flag");
        memset(&v7, 0, 0xFCu);
        v8 = 0;
        v9 = 0;
        _itoa(v10, &v5, 10);
        strcat(Text, "{");
        strcat(Text, &v5);
        strcat(Text, "_");
        strcat(Text, "Buff3r_0v3rf|0w");
        strcat(Text, "}");
        MessageBoxA(0, Text, "well done", 0);
      }
```
- 先输出{ 其次v5 然后_ 最后Buff3r_0v3rf|0w}
- itoa(v10, &v5, 10)是将v10字符串以十进制保存在v5中 v5=123
- flag{123_Buff3r_0v3rf|0w}

## 数据包中的线索
- 打开查看tcp头毫无所获
- /9j/为jpg头标识 加上`data:image/jpeg;base64`
- 查找http头发现一大堆字符串
- `/9j/`经base64解码后结果为“\xff \xd8 \xff”，该三字节为jpg文件的开头三字节
```
data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAYABgAAD.......
```
- base64转图片得到含有flag得路飞得图片
- flag{209acebf6324a09671abc31c869de72c}

## 被劫持的神秘礼物
下载得文件gift.pcapnggift.pcapng
- 打开进行分析 题目说是账号密码 一般跟登录有关
```
4	0.003591	192.168.78.134	192.168.60.123	HTTP	704	POST /index.php?r=member/index/login HTTP/1.1  (application/x-www-form-urlencoded)
```
- post传参 以及网址是index/login 查看流
- 找到name及word`adminaadminb`
```python
import hashlib
date='adminaadminb'
m=hashlib.md5(date.encode('utf-8'))
print(m.hexdigest())
```
- flag{1d240aafe21a86afc11f38a45b541a49}

## 菜刀666

## 刷新过的图片
F5隐写 下载F5-steganography 进入目录
- `java Extract Misc.jpg（图片的绝对路径） -e res.zip`
- 压缩包伪加密
- 解压打开txt得flag
- flag{96efd0a2037d06f34199e921079778ee}

## 二维码
被撕成九份的二维码？？有啥意思考验我ps水平？
- 上ps套索然后拼在一起
- 尽力了 [图片](https://i.loli.net/2019/09/10/2Vxho6rPFtzBQZw.png)
- 有那么一瞬间可以扫
- flag{7bf116c8ec2545708781fd4a0dda44e5}

## 弱口令
得一压缩包有密码 提示弱口令
- 我还真以为弱口令 换了俩个字典无果
- 压缩包里注释有东西 是一大堆不可见字符
```
    
 
 	  
 	  
					
  	 
			
 	 
  	
		
```
- 这些字符串放到sublime里能看见是由点和横组成的 像摩斯电码
- 可惜我手上没有sublime 只有vscode和notepad++ 放到notepad++里右键style token在一步步按键盘右键 也能比较方便写出莫斯电码
- `.... . .-.. .-.. ----- ..-. --- .-. ..- --` to`HELL0FORUM`
- 解压得png
- winhex无果由于png考虑lsb隐写无果 可能是加密的lsb
- 使用`cloacked-pixel`在kali下 因为是弱口令猜测123456`python lsb.py extract nvshen.png res.txt 123456` 
- 得res.txt打开为flag
- flag{jsy09-wytg5-wius8}

