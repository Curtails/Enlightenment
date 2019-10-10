---
layout: post
title: "BugkuCTF-Reverse-WriteUp"
date: 2019-08-24 01:01:01
share: true
toc: true
tags: 
 - CTF
---

BugkuCTF-Reverse-WriteUp

## 入门逆向
下载解压得baby.exe cmd打开输出`Hi~ this is a babyre`
- 先丢进PEID查查壳unknown
- 丢进ida看看 查看main函数 发现输出上述语句后 一个个将mov的hex代码转化为字符（R键）
```
mov     byte ptr [esp+2Fh], 'f'
mov     byte ptr [esp+2Eh], 'l'
mov     byte ptr [esp+2Dh], 'a'
mov     byte ptr [esp+2Ch], 'g'
mov     byte ptr [esp+2Bh], '{'
mov     byte ptr [esp+2Ah], 'R'
mov     byte ptr [esp+29h], 'e'
mov     byte ptr [esp+28h], '_'
mov     byte ptr [esp+27h], '1'
mov     byte ptr [esp+26h], 's'
mov     byte ptr [esp+25h], '_'
mov     byte ptr [esp+24h], 'S'
mov     byte ptr [esp+23h], '0'
mov     byte ptr [esp+22h], '_'
mov     byte ptr [esp+21h], 'C'
mov     byte ptr [esp+20h], '0'
mov     byte ptr [esp+1Fh], 'O'
mov     byte ptr [esp+1Eh], 'L'
mov     byte ptr [esp+1Dh], '}'
```
- 得flag

## Easy_vb
打开 可以调整八个数字 确定没反应
- 查壳 无
- 丢进OD 在反汇编界面右键-中文搜索-智能搜索
  - `004023A9` 看见MCTF
- 或者丢进ida 也能看见
- 或者专门的vb反汇编VB Decompiler Pro 在click的code中藏有key
- MCTF{_N3t_Rev_1s_E4ay_}

## Easy_re
hint: IDA OD 跟没提示
打开
```
欢迎来到DUTCTF呦
这是一道很可爱很简单的逆向题呦
输入flag吧:1515
flag不太对呦，再试试呗，加油呦
请按任意键继续. . .
```
- 查壳 无 c++
- 先丢进OD吧 右键-中文搜索-ASCII 能看到flag字符串 点击跳转
  - flag get 上一条命令含有jnz `0032108F`可见是判断 f2在此设置断点
  - 网上找 在输入flah添加flag对应的add的命令`0032105F`设置断点
  - debug-run 输入数据 有回显在add断点出 f8调试运行可以在reg看到DUTCTF
  - 实际上第二部如果智能搜索直接能查看flag
- 丢进ida 字符串查找 找出flag出现位置-f5反编译
  - `rdata:00413E34`发现长数字串 f5转换是flag的倒序
- DUTCTF{We1c0met0DUTCTF}

## 