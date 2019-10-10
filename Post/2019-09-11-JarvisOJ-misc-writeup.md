---
layout: post
title: "Jarvis OJ-MISC-WriteUp"
date: 2019-09-11 01:01:01
share: true
toc: true
tags: 
 - CTF
---

Jarvis OJ-MISC-WriteUp
采集猜忌菜鸡

## FLAG
一张写着教练我想打ctf的图片
- winhex和binwalk无果
- 丢进stegsolve查看data extract 发现504B0304显然zip
- 保存打开含Linux文件 在win下解压报错 在kali下解压 
- 提升权限`chmod 777 1` 执行`./1`
- 得到flag

## shell流量分析
下载解压得pcapng
- 小白扫描式分析 看到shell.php
- 在某tcp流中 打印了function.py 略读式一段py加密代码
  
```python
#!/usr/bin/env python
# coding:utf-8
__author__ = 'Aklis'
from Crypto import Random
from Crypto.Cipher import AES
import sys
import base64

def decrypt(encrypted, passphrase):
  IV = encrypted[:16]
  aes = AES.new(passphrase, AES.MODE_CBC, IV)
  return aes.decrypt(encrypted[16:])

def encrypt(message, passphrase):
  IV = message[:16]
  length = 16
  count = len(message)
  padding = length - (count % length)
  message = message + '\0' * padding
  aes = AES.new(passphrase, AES.MODE_CBC, IV)
  return aes.encrypt(message)

IV = 'YUFHJKVWEASDGQDH'
message = IV + 'flag is hctf{xxxxxxxxxxxxxxx}'

print len(message)

example = encrypt(message, 'Qq4wdrhhyEWe4qBF')
print example
example = decrypt(example, 'Qq4wdrhhyEWe4qBF') 
print example
```

- py中flag与IV组合经过encrypt函数加密 
- 继续查看tcp流

```
<mething/welcome/secret/not_important_secret/trash$ cat fl	
cat flag 
mbZoEMrhAO0WWeugNjqNw3U6Tt2C+rwpgpbdWRZgfQI3MAh0sZ9qjnziUKkV90XhAOkIs/OXoYVw5uQDjVvgNA==<mething/welcome/secret
```
- `mbZoEMrhAO0WWeugNjqNw3U6Tt2C+rwpgpbdWRZgfQI3MAh0sZ9qjnziUKkV90XhAOkIs/OXoYVw5uQDjVvgNA==`显然式flag且式base64编码
- flag解码在用给好得decrypt解密即可

```python
#!/usr/bin/env python
# coding:utf-8
__author__ = 'Aklis'
from Crypto import Random
from Crypto.Cipher import AES
import sys
import base64

def decrypt(encrypted, passphrase):
  IV = encrypted[:16]
  aes = AES.new(passphrase, AES.MODE_CBC, IV)
  return aes.decrypt(encrypted[16:])

def encrypt(message, passphrase):
  IV = message[:16]
  length = 16
  count = len(message)
  padding = length - (count % length)
  message = message + '\0' * padding
  aes = AES.new(passphrase, AES.MODE_CBC, IV)
  return aes.encrypt(message)

string='mbZoEMrhAO0WWeugNjqNw3U6Tt2C+rwpgpbdWRZgfQI3MAh0sZ9qjnziUKkV90XhAOkIs/OXoYVw5uQDjVvgNA=='
string64=base64.b64decode(string)
print string64
print decrypt(string64,'Qq4wdrhhyEWe4qBF')
```
- hctf{n0w_U_w111_n0t_f1nd_me}

## 远程登录协议
下载解压得pcapng hint：telnet
- 查看过滤telnet
- 查找flag 好几个一个个试

## 炫酷得战队logo
下载得phrack.bmp
- 图片无法显示
- 修复不成 查了以下`89504E47`存在藏着一个png
- 创建复制导出png 打开也无法显示
- 改一下宽高 图片有内容非常模糊
- 图片由crc校验值（看不出）用此值反推宽高
```python
    for i in range(16,256):
        print hex(i)[2:]
        b=hex(i)[2:]
        a=('89504E470D0A1A0A0000000D49484452000001'+b+'000001000802000000F37A5E12000000017352474200AECE1CE9000000046741......A11F3FFE0B3B73B0698B976EA80000000049454E44AE426082').decode("hex")
        f=open('1\\'+b+'.png',"wb")
        f.write(a)
        f.close() 
```
- 得出宽高改 
- 得flag

## 简单网管协议
- 直接notepad++打开搜flag
- 傻了得去掉flag{}
- 077149a68b9d4f25f52bb11530f44028

## SCAN
题目：有人在内网发起了大量扫描，而且扫描次数不止一次，请你从capture日志分析一下对方第4次发起扫描时什么时候开始的，请提交你发现包编号的sha256值(小写)
- Wireshark打开 发现开头是个icmp 猜测每次扫描icmp 因此过滤icmp
- 第四次扫描包编号 从后往前一个个猜吧 是`155989` sha256加密
- PCTF{0be2407512cc2a40bfb570464757fd56cd0a1d33f0bf3824dfed4f0119133c12}



