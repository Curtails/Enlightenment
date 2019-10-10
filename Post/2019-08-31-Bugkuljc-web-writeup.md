---
layout: post
title: "BugKuCTF-论剑场-Web-WriteUp"
date: 2019-08-31 01:01:01
share: true
toc: true
tags: 
 - CTF
---

BugKuCTF-论剑场-Web-WriteUp

## web26
```php
<?php
$num=$_GET['num'];
$str=$_GET['str'];
show_source(__FILE__);
if (isset($num)&&isset($str)) {
    if (preg_match('/\d+/sD',$str)) {
        echo "vagetable hhhh";
        exit();
    }
    $result=is_numeric($num) and is_numeric($str);
    if ($result) {
        include "flag.php";
        echo "$flag";
    }
    else{
        echo "vagetablessssss";
    }
} 
```
- 看到正则傻了 直接用GLOBALS
- payload`?str=GLOBALS&num=1`
- flag{f0058a1d652f13d6}

## web1
打开网址是一张有代码图片 一道代码审计题 涉及extract变量覆盖
- payload`?a=&b=`
- flag{c3fd1661da5efb989c72b91f3c378759} 

## web9
打开显示`put me a message bugku then you can get the flag `
- 打开bp抓包 传参方式GET改成PUT 空一行加上`bugku` -go
- 得`ZmxhZ3tUN2w4eHM5ZmMxbmN0OE52aVBUYm4zZkcwZHpYOVZ9`bsae64解码
- flag{T7l8xs9fc1nct8NviPTbn3fG0dzX9V}

## 流量分析
下载得bugku.pcapng
- 追踪流tcp 看到password为flag
- flag{bugku123456}

## web2
这种几秒的计算题然后提交 需要写py
留坑

## web5
hint:injection 题目好像挂了

## web6
管理员系统 bugkuctf一样的题
- 源代码注释base64解码test123
- 随便输 `IP禁止访问，请联系本地管理员登陆，IP已被记录. `
- bp抓包 账户admin 密码test123
- 加上X-Forwarded-For: 127.0.0.1
- flag{85ff2ee4171396724bae20c0bd851f6b}

## web11
需要py

## web13
需要py


