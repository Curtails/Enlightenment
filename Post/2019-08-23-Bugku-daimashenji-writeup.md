---
layout: post
title: "BugkuCTF-代码审计-WriteUp"
date: 2019-08-23 01:01:01
share: true
toc: true
tags: 
 - CTF
---

BugkuCTF-代码审计-WriteUp

## extract变量覆盖
```php
<?php
$flag='xxx';
extract($_GET);
if(isset($shiyan))
{
    $content=trim(file_get_contents($flag));
    if($shiyan==$content)
    {
        echo'flag{xxx}';
    }
else
{
    echo'Oh.no';
    }
}
?>
```
- `extract($_GET)`相当于
```
$shiyan = $_GET['shiyan']
$flag = $_GET['flag']。
```
- 输出flag满足两个条件
  - `isset`为真 这个get`shiyan`参数即可 变量值为null亦可
  - `shiyan==flag`
- payload`?shiyan=&flag=`
- flag{bugku-dmsj-p2sm3N}


## strcmp比较字符串
```php
<?php
$flag = "flag{xxxxx}";
if (isset($_GET['a'])) {
if (strcmp($_GET['a'], $flag) == 0) //如果 str1 小于 str2 返回 < 0； 如果 str1大于 str2返回 > 0；如果两者相等，返回 0。
//比较两个字符串（区分大小写）
die('Flag: '.$flag);
else
print 'No';
}
?>
```
- strcmp无法判别数组，出错显示警告信息后后并return 0
- payload`?a[]=anything`
- flag{bugku_dmsj_912k}

## urldecode二次编码绕过
```php
<?php
if(eregi("hackerDJ",$_GET[id])) {
    echo("

    not allowed!
    ");
    exit();
    }
$_GET[id] = urldecode($_GET[id]);
if($_GET[id] == "hackerDJ")
{
    echo "

    Access granted!
    ";
    echo "

    flag
    ";
    }
?>
```
- 浏览器默认对参数进行一次url编码
- eregi会搜索指定字符串 url解码一次 所以无法直接`id=hackerDJ`
- urldecode()会将$_GET[id]从二次URL编码变成一次URL编码，赋值给$_GET[id]，当$_GET[id]与“hackerDJ”比较时，$_GET[id]再从一次URL编码解码，最后比较相等得到flag
- 将`hackerDJ`进行两次url编码`%25%36%38%25%36%31%25%36%33%25%36%62%25%36%35%25%37%32%25%34%34%25%34%61`
- payload`?id=%25%36%38%25%36%31%25%36%33%25%36%62%25%36%35%25%37%32%25%34%34%25%34%61`
- flag{bugku__daimasj-1t2} 

## md5()函数
```php
<?php
error_reporting(0);
$flag = 'flag{test}';
if (isset($_GET['username']) and isset($_GET['password'])) {
    if ($_GET['username'] == $_GET['password'])
        print 'Your password can not be your username.';
    else if (md5($_GET['username']) === md5($_GET['password']))
        die('Flag: '.$flag);
    else
        print 'Invalid password';
    }
?>
```
- 读源码得知 username不等于password且md5二者值相等输出flag
- md5不支持处理数组返回null 所以`?username[]=1&password[]=2`
- 传入以0e开头的字符串行吗？不行 因为是强类型`===`
- flag{bugk1u-ad8-3dsa-2}

## 数组返回NULL绕过
```php
<?php
$flag = "flag";
if (isset ($_GET['password'])){
if (ereg ("^[a-zA-Z0-9]+$", $_GET['password']) === FALSE)
    echo 'You password must be alphanumeric';
else if (strpos ($_GET['password'], '--') !== FALSE)
    die('Flag: ' . $flag);
else
    echo 'Invalid password';
    }
?>
```
- strpos()函数不能处理数组的漏洞构造
- payload`?password[]=`
- flag{ctf-bugku-ad-2131212}

## 弱类型整数大小比较绕过
```php
$temp = $_GET['password'];
is_numeric($temp)?die("no numeric"):NULL;
if($temp>1336){
echo $flag;
```
- is_numeric — 检测变量是否为数字或数字字符串;bool is_numeric( mixed $var);如果 var 是数字和数字字符串则返回 TRUE，否则返回 FALSE。
- payload`?pwssword=1337a`
- flag{bugku_null_numeric}

## sha()函数比较绕过
```php
<?php
$flag = "flag";
if (isset($_GET['name']) and isset($_GET['password']))
{
    var_dump($_GET['name']);
    echo "
    ";
    var_dump($_GET['password']);
    var_dump(sha1($_GET['name']));
    var_dump(sha1($_GET['password']));
    if ($_GET['name'] == $_GET['password'])
        echo '
        Your password can not be your name!
        ';
    else if (sha1($_GET['name']) === sha1($_GET['password']))
    die('Flag: '.$flag);
    else
    echo '

    Invalid password.
    ';
    }
else
    echo '
    Login first!
    ';
?>
```
- 利用sha1函数不能处理数组进行构造payload
- payload`?name[]=a&password[]=b`
- flag{bugku--daimasj-a2}

## md5加密相等绕过
```php
<?php
$md51 = md5('QNKCDZO');
$a = @$_GET['a'];
$md52 = @md5($a);
if(isset($a)){
    if ($a != 'QNKCDZO' && $md51 == $md52) {
    echo "flag{*}";
    }else {
        echo "false!!!";
        }
}
else{echo "please input a";}
?>
```
- 利用MD5函数处理的特殊字符串进行绕过构造payload

```php
//下面的特殊字符串经过MD5函数处理过之后相等
QNKCDZO
0e830400451993494058024219903391

s878926199a
0e545993274517709034328855841020
  
s155964671a
0e342768416822451524974117254469
  
s214587387a
0e848240448830537924465865611904
  
s214587387a
0e848240448830537924465865611904
  
s878926199a
0e545993274517709034328855841020
  
s1091221200a
0e940624217856561557816327384675
  
s1885207154a
0e509367213418206700842008763514
```
- flag{bugku-dmsj-am9ls} 


## 十六进制与数字比较
阅读源码
```php
<?php
error_reporting(0);
function noother_says_correct($temp)
{
    $flag = 'flag{test}';
    $one = ord('1'); //ord — 返回字符的 ASCII 码值
    $nine = ord('9'); //ord — 返回字符的 ASCII 码值
    $number = '3735929054';
    // Check all the input characters!
    for ($i = 0; $i < strlen($number); $i++)
    {
        // Disallow all the digits!
        $digit = ord($temp{$i});
        if ( ($digit >= $one) && ($digit <= $nine) )
        {
        // Aha, digit not allowed!
        return "flase";
        }
    }
    if($number == $temp)
    return $flag;
}
$temp = $_GET['password'];
echo noother_says_correct($temp);
?>
```

- 满足两个条件 password不能含有数字1-9 number==temp
- 恰巧题目给我提供了`3735929054`它的hex不含1-9`0xdeadc0de` 满足上述条件
- payload`?password=0xdeadc0de`
- flag{Bugku-admin-ctfdaimash}

## 变量覆盖
挂了

## ereg正则%00截断
```php
<?php
if (isset ($_GET['password'])) {
    if (ereg ("^[a-zA-Z0-9]+$", $_GET['password']) === FALSE)
    {
        echo '<p>You password must be alphanumeric</p>';
    }
    else if (strlen($_GET['password']) < 8 && $_GET['password'] > 9999999)
    {
        if (strpos ($_GET['password'], '*-*') !== FALSE)
        {
            die('Flag: ' . $flag);
        }
        else
        {
            echo('<p>*-* have not been found</p>');
        }
    }
    else
    {
        echo '<p>Invalid password</p>';
    }
```
- 利用strlen()函数和strpos()函数不能处理数组进行构造payload
- payload`?password[]=`
- flag{bugku-dm-sj-a12JH8}

## strpos数组绕过
```php
<?
php$flag = "flag"; 
if (isset ($_GET['ctf'])) 
{ 
    if (@ereg ("^[1-9]+$", $_GET['ctf']) === FALSE) 
        echo '必须输入数字才行';
        else if (strpos ($_GET['ctf'], '#biubiubiu') !== FALSE) 
            die('Flag: '.$flag); 
        else echo '骚年，继续努力吧啊~'; 
        } 
?>
```
- 利用strpos()函数不能处理数组进行构造payload
- payload`?ctf[]=`
- flag{Bugku-D-M-S-J572}

## 数字验证正则绕过
```php
<?php
error_reporting(0);
$flag = 'flag{test}';
if ("POST" == $_SERVER['REQUEST_METHOD'])
{
$password = $_POST['password'];
if (0 >= preg_match('/^[[:graph:]]{12,}$/', $password)) //preg_match — 执行一个正则表达式匹配
{
echo 'flag';
exit;
}
while (TRUE)
{
$reg = '/([[:punct:]]+|[[:digit:]]+|[[:upper:]]+|[[:lower:]]+)/';
if (6 > preg_match_all($reg, $password, $arr))
break;
$c = 0;
$ps = array('punct', 'digit', 'upper', 'lower'); //[[:punct:]] 任何标点符号 [[:digit:]] 任何数字 [[:upper:]] 任何大写字母 [[:lower:]] 任何小写字母
foreach ($ps as $pt)
{
if (preg_match("/[[:$pt:]]+/", $password))
$c += 1;
}
if ($c < 3) break;
//>=3，必须包含四种类型三种与三种以上
if ("42" == $password) echo $flag;
else echo 'Wrong password';
exit;
}
}
?>
```
- 做傻了 都可以用数组绕过
- preg_match()函数不能处理数组进行构造payload
- get不行 post:`password[]=`
- flag{Bugku_preg_match}

## 简单的waf
挂了