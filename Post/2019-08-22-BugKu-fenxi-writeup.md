---
layout: post
title: "BugkuCTF-分析-WriteUp"
date: 2019-08-22 01:01:01
share: true
toc: true
tags: 
 - CTF
---


BugkuCTF-分析-WriteUp

## flag被盗
下载得key.pcapng
- 用wireshark打开分析tcp流
- 看着看着就看到了flag
- flag{This_is_a_f10g}

## 中国菜刀
下载解压得caidao.pcapng
- 丢进wireshark分析 追踪流tcp发现含有`flag.tar.gz`
- 傻了pcapng也会有隐藏文件 丢进binwalk
- 分离tar文件解压得flag.txt
- key{8769fe393f2b998fa6a11afe2bfcd65e}

## 这么多数据包
题目提醒先找到getshell的流 
- 经大佬提示，一般getshell流的TCP的报文中很可能包含`command`这个字段,我们可以通过`协议 contains “内容”`来查找 getshell 流
- 选中最后一个查看tcp流 看到base编码`Q0NURntkb195b3VfbGlrZV9zbmlmZmVyfQ==`
- CCTF{do_you_like_sniffer}

## 手机热点
得到Blatand_1.pcapng 
题目：有一天皓宝宝没了流量只好手机来共享，顺便又从手机发了点小秘密到电脑，你能找到它吗？
- wireshark看来不会
- 既然传了东西 记住了试试binwalk
- 分离时间挺长 得到含有flag得gif
- SYC{this_is_bluetooth}

