---
layout: post
title: "BugkuCTF-安卓-WriteUp"
date: 2019-08-25 01:01:01
share: true
toc: true
tags: 
 - CTF
---


BugkuCTF-安卓-WriteUp

## signin
下载得zip解压得Sign_in.apk
- jadx打开，找到关键比较点checkPassword，就是将flag base64后再翻转后与getflag的字符串进行比较
- strig是保存在values下面的string.xml中
- 找到base64按照源码先翻转在解码
- `991YiZWOz81ZhFjZfJXdwk3X1k2XzIXZIt3ZhxmZ`to`ZmxhZ3tIZXIzX2k1X3kwdXJfZjFhZ18zOWZiY199`解码
- flag{Her3_i5_y0ur_f1ag_39fbc_}

