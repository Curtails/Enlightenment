---
layout: post
title: "BugkuCTF-加密-WriteUp"
date: 2019-08-23 01:01:01
share: true
toc: true
tags: 
 - CTF
---


BugkuCTF-加密-WriteUp

## 滴答~滴 
- 摩斯电码
- KEY{bkctfmisc}

## 聪明的小羊
一只小羊翻过了2个栅栏 KYsd3js2E{a2jda}
- 栅栏密码 栏数为2
- KEY{sad23jjdsa2}

## ok
- Ook!
- flag{ok-ctf-1234-admin}

## 这不是摩斯密码
- Brainfuck
- flag{ok-c2tf-3389-admin}

## easy_crypto
一长串二进制 长短不一 是morse可以转换ASCII
- py：https://github.com/houhuiting/bugku-python/blob/master/binary%20morse_to_ascii.py
- flag{morse_code_1s_interest1n9!}

## 简单加密
`e6Z9i~]8R~U~QHE{RnY{QXg~QnQ{^XVlRXlp^XI5Q6Q6SKY8jUAA`末尾AA形式很像==
- 转换成ascii
- 在前移4位`a 2 V 5 e z Y 4 N z Q z M D A w N j U w M T c z M j M  w Z T R h N T h l Z T E 1 M 2 M 2 O G U 4 f Q = =`
- 解码
- key{68743000650173230e4a58ee153c68e8}

## 散乱的密文
lf5{ag024c483549d7fd@@1}
一张纸条上凌乱的写着2 1 6 5 3 4
- 这个密码给了key 字符串仔细看有flag字符还有填充字符@
- 字符串六行六列排列
- 按照key顺序从小到大 对照字符串从上到下读`f25dl03fa4d1g87}{c9@544@`
- 栅栏解码 栏数6
- flag{52048c453d794df1}

## 凯撒部长的奖励
凯撒密码
- SYC{here_Is_yOur_rEwArd_enjOy_It_Caesar_or_call_him_vIctOr_is_a_Excellent_man_if_you_want_to_get_his_informations_you_can_join_us}

## base64
不仅仅是base64
- base64 得到\ 数字组合
- unsapce 得到\x 数字组合
- hex 得到\u 数字组合
- unspace 得到可见字符串和数字
- dec to text 得到& # x 数字组合
- html 
`&#102;&#108;&#97;&#103;&#37;&#55;&#66;&#99;&#116;&#102;&#95;&#116;&#102;&#99;&#50;&#48;&#49;&#55;&#49;&#55;&#113;&#119;&#101;&#37;&#55;&#68;`
- unicode编码转ASCII
- flag

## .!?
Brainfuck/Ook!
- flag{bugku_jiami}

## +[]-
同上
- flag{bugku_jiami_23}

## 奇怪的密码
gndk€rlqhmtkwwp}z 类似异变的凯撒
```
gndk的10进制的ASCII码分别是：103 110 100 107
flag的10进制的ASCII码分别是  ：102 108  97  103
```
- 规律为加1.2.3.4...
- `102 108 97 103 8359 108 101 105 95 99 105 95 106 105 97 109 105`
- 转换ascii
- flag{lei_ci_jiami}

## 托马斯.杰斐逊
转盘加密 好绕
```
1： <ZWAXJGDLUBVIQHKYPNTCRMOSFE <
2： <KPBELNACZDTRXMJQOYHGVSFUWI <
3： <BDMAIZVRNSJUWFHTEQGYXPLOCK <
4： <RPLNDVHGFCUKTEBSXQYIZMJWAO <
5： <IHFRLABEUOTSGJVDKCPMNZQWXY <
6： <AMKGHIWPNYCJBFZDRUSLOQXVET <
7： <GWTHSPYBXIZULVKMRAFDCEONJQ <
8： <NOZUTWDCVRJLXKISEFAPMYGHBQ <
9： <QWATDSRFHENYVUBMCOIKZGJXPL <
10： <WABMCXPLTDSRJQZGOIKFHENYVU <
11： <XPLTDAOIKFZGHENYSRUBMCQWVJ <
12： <TDSWAYXPLVUBOIKZGJRFHENMCQ <
13： <BMCSRFHLTDENQWAOXPYVUIKZGJ <
14： <XPHKZGJTDSENYVUBMLAOIRFCQW <

密钥： 2,5,1,3,6,4,9,7,8,14,10,13,11,12

密文：HCBTSXWCRQGLES
```
- 根据对应关系2 H 第2行字符串末尾H到结尾部分放到前面
- 以下同理
```
2：<HGVSFUWIKPBELNACZDTRXMJQOY<
5：<CPMNZQWXYIHFRLABEUOTSGJVDK<
1：<BVIQHKYPNTCRMOSFEZWAXJGDLU〈
3：〈TEQGYXPLOCKBDMAIZVRNSJUWFH<
6：〈SLOQXVETAMKGHIWPNYCJBFZDRU<
4：〈XQYIZMJWAORPLNDVHGFCUKTEBS<
9：〈WATDSRFHENYVUBMCOIKZGJXPLQ<
7：〈CEONJQGWTHSPYBXIZULVKMRAFD<
8：〈RJLXKISEFAPMYGHBQNOZUTWDCV<
14：〈QWXPHKZGJTDSENYVUBMLAOIRFC<
10：〈GOIKFHENYVUWABMCXPLTDSRJQZ<
13：〈LTDENQWAOXPYVUIKZGJBMCSRFH<
11：<ENYSRUBMCQWVJXPLTDAOIKFZCGH〈
12：〈SWAYXPLVUBOIKZGJRFHEN体QTD<
```
- 倒数第六列含有bugku 为flag内容
- flag{xsxsbugkuadmin}

## zip伪加密
 - 伪加密找到504B0102 后4byte 09改成00
 - flag{Adm1N-B2G-kU-SZIP}

## 告诉你个秘密(ISCCCTF)
```
636A56355279427363446C4A49454A7154534230526D6843
56445A31614342354E326C4B4946467A5769426961453067
```
- dec to ASCII
- base64
- 键盘密码包围
- flag{ae73587ba56baef5}

## 这不是MD5
以为多难 是hex
- 直接hex to ASCII
- flag{ae73587ba56baef5}

## 贝斯家族
- base16，32，64，36，56，62，91都试试
- base91
- flag{554a5058c9021c76}

## 富强民主
搞笑题
- 核心价值观编码 
- flag{90025f7fb1959936}

## python(N1CTF)

## 进制转换

## affine

## crack it

## rsa

## 来自宇宙的信号
搜索银河语言
- flag{nopqrst}