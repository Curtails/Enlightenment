---
layout: post
title: "2019-秋季-校-CTF-WriteUp"
date: 2019-08-28 01:01:01
share: true
toc: true
tags: 
 - CTF
---

2019-秋季-校-CTF-WriteUp.
记录一次真正意义上的CTF比赛；吸取教训，总结经验。
- 教训：远远不够仔细 不够熟练
- 经验：第一次知识在实战中磨合 有了印象

# 加密
## <mark>Easycrypto</mark>
下载解压得lookcarefully.txt 打开显示
```Markdown
WXAD 3dwr G_VN qz_s RVDG 8kuo -'p] !A_W wxad h_bm rvdg h_bm ECSF WXAD wxad =_[\
```
这题没做出来的人是真的蠢 比如我 
- 键盘密码 四个键位两两包围一个键位 拼起来即可
- SeBaFi{QsnfnDSs}

## <mark>Warm up</mark> 
打开所给网址 显示以下信息
```php
$flag="SeBaFi(*}"; echo base64encode(gzcompress(hex2bin(strrev(urlencode(bin2hex($flag))))
eJy7btoSfK20uWRbsJvxEfPIbUuWLCteli7qnnJsi2lYacuxtO3TUsRUwkwBjV4STA==
```
比赛时 字符串给的是错的？！现在的也是？？
- 按照代码的编码逆序解码即可
```php
<?php
$s=eJy7btoSfK20uWRbsJvxEfPIbUuWLCteli7qnnJsi2lYacuxtO3TUsRUwkwBjV4STA==;
echo hex2bin(urldecode(strrev(bin2hex(gzuncompress(base64 decode($s))))));
?>
```
- SeBaFi{flHWeSKlFtQqJ7jJJhzsL3d5kG8Wm5HS}

## <mark>read me</mark>
下载的压缩包含四个文件`1.txt 2.txt 3.txt flag.txt`
Hint:小小小
- 1 2 3文件小所以采用CRC碰撞绕过zip密码

```python
#coding:utf-8
import zipfile
import string
import binascii
 
def CrackCrc(crc):
    for i in dic :
        for j in dic:
            for p in dic:
                #for q in dic:
                    s=i+j+p+q
                    if crc == (binascii.crc32(s) & 0xffffffff):
                        #print s  
                        f.write(s+"\n")
                        return  
 
def CrackZip(): 
    for I in range(54):
        file = 'chunk' + str(I) + '.zip'
        f = zipfile.ZipFile(file, 'r')
        GetCrc = f.getinfo('data.txt')
        crc = GetCrc.CRC
        #以上3行为获取压缩包CRC32值的步骤
        CrackCrc(crc)

dic = string.ascii_letters + string.digits + '+/='
f=open('out.txt','w')
CrackZip()
f.close()
```

- 分别执行三个txt文件的crc值 找出有规律的字符串
- `keyisc rc32ue nit!@#`拼一起`keyiscrc32uenit!@#`为解压密码
- 解压得flag
- SeBaFi{anheipo_huai_shen_three}

## <mark>又是维吉尼亚</mark>
打开txt
```markdown
cmzzwtcdlimzydhphdelohroipptlwetydtchvadozstwdcmznyzvdqomiwzwivacmznyzv
rhzwtcltmawvtvzvjphwopivjyijzdzgdwimzwyqqtmdzahdipwtrtyvdwvyskzmtcltmawroimirdzmwwzvdz
vrzwivaweppikpzwipwtriprypidzwpzghripazvwhdeivadozfzehwuhmjhvhi 

NmSgNv{m09f718v9kr8gk7p66ncv38nr0i44640}
```
- 注意题目无密钥 密码描述为一长串的字符串 猜测词频分析
- 访问https://quipqiup.com/ 模式选择`statistics`进行词频分析
- 提取密钥` virginia`
- 利用密钥解密`NmSgNv{m09f718v9kr8gk7p66ncv38nr0i44640}`
- SeBaFi{e09f718a9ca8ac7c66fca38fa0c44640}

## <mark>rsa</mark>
hint：常规rsa
rsa不懂 留坑


# MISC
## <mark>hiddenbears</mark> 
下载解压得到一张显示四头熊的图片
- 看属性 无
- 丢进winhex 无果
- 丢进binwalk 无果
- 丢进StegSolve 四周有白边
- 切换几次颜色通道 能看到最上边有字符串 加上格式即可
- SeBaFi{Ao39gPDEzwrkojhEqNmtuDKc} 

## wakaka 
下载得压缩包 有密码 压缩里面是flag.txt
hint：密码为wakaka+五位数字
- 上工具直接爆破 得密码`wakaka21051`

## Hidden91 
下载得图片
- binwalk得压缩包解压得txt
- 打开txt`7E4F66637478532424313A28352A24533E31514A255F245938216A7B420A`
- base16解码得`~OfctxS$$1:(5*$S>1QJ%_$Y8!j{B`
- 结合题目91 猜测base91解码
- SeBaFi{170065%shtxdddk}

## 二维码动图 
下载得一gif
- 没啥好说的逐帧分离gif 一个个就成
- SeBaFi{mAr10_i5_a_br0} 

## <mark>泰加熊</mark>
很恶心的题
下载解压得七张图片
- binwalk一个个试 第六张图片有点东西 分离出zip
- 解压得名字为msg文件
- 在linux下执行`./msg`可打开此文件
- Flag: B3znJluppFPJnNG7PAg

## <mark>mmmmmm</mark>
下载得一图片
- binwalk 分离出zip 
- 解压得readme.txt和另一个zip 此zip中含readme.txt及flag.txt
- 这是明文攻击
- 使用 AZPR 工具，选择文本攻击/AAPR明文竟然没用
- SeBaFif{readme_64%_jok}

# PWN
## <mark>简单的溢出?</mark>
确实简单 只有蠢人不会做 比如我
- PEiD 分析发现不是有效的PE文件 可能试dos16位
- 丢进ida32 查找字符串即可
- SebaFi{4cc09188c005dc1a5fad8c6e2551903}

## <mark>拼接成 shell</mark>
留坑


# Reverse
## <mark>安卓签到 </mark>
- 使用 jadx 工具反编译 apk
- 查看res/layput/activity_main.xml
- SeBaFi{ee2faeed038501c1deab01c7b54f2fa9}

## <mark>4 位数</mark>
下载得re3.ppp
- 丢进ida32 选中main反编译 得
```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
  int result; // eax
  int v4; // [esp+24h] [ebp-84h]
  int v5; // [esp+30h] [ebp-78h]
  char nptr; // [esp+38h] [ebp-70h]
  unsigned int v7; // [esp+9Ch] [ebp-Ch]

  v7 = __readgsdword(0x14u);
  printf("please input the key:");
  memset(&nptr, 0, 0x64u);
  __isoc99_scanf("%s", &nptr);
  if ( strlen(&nptr) != 4
    || (v4 = atoi(&nptr), v5 = v4 % 100 / 10, v4 % 10 + v5 + v4 / 1000 + v4 % 1000 / 100 != 23)
    || v5 / (v4 % 10) != 2
    || v4 % 1000 / 100 - v5 != -1
    || v4 / 1000 % v5 != 3 )
  {
    puts("wrong!");
    result = 1;
  }
  else
  {
    puts("correct!");
    result = 1;
  }
  return result;
}
```
- 根据功能 写payload
- SeBaFi{9563} SeBaFi{9563} 

## <mark>vvv </mark>
留坑


# Web
## 签到
白给题 查看源代码

## easy
打开网页显示 “Only allowed access by local address
- 明显xff
- 抓包加上`X-Forwarded-For: 127.0.0.1` go 显示信息提示我们access admin
- 找到cookie`user=Z3Vlc3Q%3D` 试guest的base64 把admin的base64替换它 go
- SeBaFi{a5717a649d346ed0c51be68888c130cd}

## 相同的 MD5 
打开网页找到最终网页
- 啥也不说了 直接数组走起

## <mark>序列化 </mark>
留坑

## <mark>过四关</mark>
留坑

