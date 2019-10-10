---
layout: post
title: "HTML学习笔记"
date: 2019-08-06 01:01:01
share: true
toc: true
tags: 
 - HTML
---

参考菜鸟教程的：[HTML教程](https://www.runoob.com/html/html-tutorial.html) 学习下基本知识顺便整理笔记。

# HTML教程(HTML5)

## HTML教程
### 实例
一个标准的HTML实例：
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
    <h1>我的第一个标题</h1>
    <p>我的第一个段落。</p>
</body>
</html>
```
注意：对于有些中文网页需要声明编码`<meta charset="utf-8">`
### HTML后缀名
- html
- htm
### 补充
-  utf8、utf-8及UTF-8
三者的区别是应用在PHP、HTML和MySQL的区别。总的来说，在MySQL中可以使用uft8，其他地方一律使用UTF-8即可。
- HTML中不支持直接用空格、回车及制表符进行格式化输出，HTML中有相应的标签来表示空格及回车。数量大于1的空格只会被解析成一个空格。

```html
<!--html代码-->
<p>
  菜     鸟
  教程
</p>
```
```
//输出
菜 鸟教程
```

## HTML简介
### 实例
再一次标准的HTML实例
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
</head>
<body>
    <h1>我的第一个标题</h1>
    <p>我的第一个段落。</p>
</body>
</html>
```
- `<!DOCTYPE html>`声明此文档为HTML5文档
- `<html>`为HTML的根元素
- `<head>`为HTML的头部标签，包含了元数据，不可见
- `<title>`描述了文档的标签，显示在浏览器标签页上
- `<body>`包含的HTML的可见内容
- `<h1>`定义一个大标题
- `<p>`定义一个段落

### 什么是HTML
HTML就是一种标记语言；不同于编程语言，使用各种标签/元素<>来描述页面。显而易见一个HTML文档（web页面）包含了标签和文本。
### 什么是HTML元素
广义下，HTML元素就是HTML标签；狭义下，HTML元素包含了<mark>开始标签</mark>和<mark>结束标签</mark>。
```html
 <p>这是一个段落。</p>
```
### 如何显示一个HTML页面
使用Web浏览器打开HTML文档即可。Web浏览器并不是显示全部文档，而是根据标签有选择的显示文本。
### HTML的结果
```html
<!--只有<body>与</body包含的内容才能显示>-->
<html>
<head>
    <title>页面标题</title>
</head>
<body>
    <h1>这是一个标题</h1>
    <p>这是一个段落。</p>
    <p>这是另外一个段落。</p>
</body>
</html> 
```
### 补充
- `<!DOCTYPE> 声明`
  ```html
    <!DOCTYPE html>
    <!DOCTYPE HTML>
    <!doctype html>
    <!Doctype Html>
  ```
  以上方式皆可不区分大小写。

## HTML编辑器
### 选择编辑器
- Notepad++
- Visual Studio Code
- 记事本
### 如何编写HTML
创建一个以后缀名.html的文件，打开输入代码即可。显示效果可由浏览器打开观看。


## HTML基础
介绍标题、段落、链接及图像。
### 标题
标题一个六个不同等级标签`<h1>`最大`<h6>`最小。
```html
<!--完整的HTML代码-->
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
</head>
<body>
    <h1>这是标题 1</h1>
    <h2>这是标题 2</h2>
    <h3>这是标题 3</h3>
    <h4>这是标题 4</h4>
    <h5>这是标题 5</h5>
    <h6>这是标题 6</h6>
</body>
</html>
```
### 段落
使用`<p>`标签定义。
```html
<p>这是一个段落。</p>
<p>这是另外一个段落。</p>
```
`<p>`标签自带换行。

### 链接
使用`<a>`标签定义。
```html
<a href="http://www.runoob.com">这是一个链接</a>
```
### 图像
使用`<img>`标签定义。
```html
<img src="/images/logo.png" width="258" height="39" />
```
widt和height是img标签的属性，用来调整图像的宽和高。

### 补充
- href与src区别：
  简单来说href是引用表示此页面和链接中的页面有关联；src是引入，在当前页面显示了其他元素。
- href与src的路径：
  - 绝对路径
  - 相对路径

## HTML元素
HTML元素与HTML标签意义大致相同；HTML元素含有起始标签及闭合标签，成对出现。
### HTML元素的语法
- HTML元素以起始标签开始、以闭合标签结束。
- 元素的内容是开始标签与结束标签之间的内容。
- 有些HTML元素可以具有空内容
- 绝大多数元素含有属性

### 实例
```html
<!DOCTYPE html>
<html>
<body>
    <p>这是第一个段落。</p>
</body>
</html> 
```
以上实例中含有三个元素`<html><body><p>`，注意不要忘记结束标签。

### HTML空元素
没有内容（空内容）的元素即空元素，空元素的关闭在开始标签（因为是单个标签）。例如`<br>`表示换行没有结束标签，但更严格的写法是`<br/>`。书写后者更好。
### 补充
HTML对大小写不严格，但推荐小写更好更长远。

## HTML属性
属性是元素的附加信息。
- 属性可以为元素添加附加信息
- 属性出现于开始标签
- 属性总是名称和键值成对出现，如name="liming"

### 实例
`<a>`标签的属性href表示超链接。
```html
<a href="http://www.runoob.com">这是一个链接</a>
```
### 补充
- [HTML标签参考](https://www.runoob.com/tags/html-reference.html)
- [HTML标签属性参考](https://www.runoob.com/tags/ref-standardattributes.html)


## HTML标题
标题很重要，务必在标题标签中写入的是标题相关信息。
标题显示为粗体。
### 实例

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
</head>
<body>
    <h1>这是标题 1</h1>
    <h2>这是标题 2</h2>
    <h3>这是标题 3</h3>
    <h4>这是标题 4</h4>
    <h5>这是标题 5</h5>
    <h6>这是标题 6</h6>
</body>
</html>
```
### 补充
- 水平线`<hr>`
- 注释`<!--内容-->`

## HTML段落
使用`<p>`标签定义。
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
</head>
<body>
    <p>这是一个段落。</p>
    <p>这是一个段落。</p>
    <p>这是一个段落。</p>
</body>
</html>
```
注意不要忘记`</p>`。
### 补充
- `<br>`换行


## HTML文本格式化
### 实例
```html
<!DOCTYPE html>
<html>
<head> 
    <meta charset="utf-8"> 
    <title>菜鸟教程(runoob.com)</title> 
</head> 
<body>

    <b>加粗文本</b><br><br>
    <i>斜体文本</i><br><br>
    <code>电脑自动输出</code><br><br>
    这是 <sub> 下标</sub> 和 <sup> 上标</sup>

</body>
</html>
```
注意：
`<strong>` 与标签 `<b>` 显示效果相同, `<em> `与 `<i>`标签显示效果相同，但是如果需要显示粗体和斜体最好使用`<br> <i>`，因为只是到目前为止`<strong> <em>`渲染结果相同罢了。搜索爬虫会根据标签抓取。

### 补充
- 实现缩写效果
  
```html
<!DOCTYPE html> 
<html>
<head> 
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
</head>
<body>
<abbr title="etcetera">etc.</abbr>
<br />
<acronym title="World Wide Web">WWW</acronym>
<p>在某些浏览器中,当您把鼠标移至缩略词语上时，title 可用于展示表达的完整版本。</p>
<p>仅对于 IE 5 中的 acronym 元素有效。</p>
<p>对于 Netscape 6.2 中的 abbr 和 acronym 元素都有效。</p>
</body>
</html>
```

- 改变文字方向
  
```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
</head> 
<body>
<p>该段落文字从左到右显示。</p>  
<p><bdo dir="rtl">该段落文字从右到左显示。</bdo></p>  
</body>
</html>
```

- 块引用
  
```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
</head>
<body>
<p>WWF's goal is to: 
<q>Build a future where people live in harmony with nature.</q>
We hope they succeed.</p>
</body>
</html>
```

- 实现删除线及下划线
  
```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
</head>
<body>
<p>My favorite color is <del>blue</del> <ins>red</ins>!</p>
</body>
</html>
```

## HTML链接
### 实例
标签所含的文字内容不一定是文本，也可以是图像或其他HTML元素。
```html
<a href="https://www.runoob.com/">访问菜鸟教程</a> 
```
使用 target 属性，你可以定义被链接的文档在何处显示。
下面的这行会在新窗口打开文档：
```html
<a href="https://www.runoob.com/" target="_blank" rel="noopener noreferrer">访问菜鸟教程!</a>
```
### id属性
```html
<a id="tips">有用的提示部分</a> 
```
在HTML文档中创建一个链接到"有用的提示部分(id="tips"）"
```html
<a href="#tips">访问有用的提示部分</a> 
```


## HTML头部
`<head>` 元素包含了所有的头部标签元素。在`<head>`元素中你可以插入脚本（scripts）, 样式文件（CSS），及各种meta信息。
可以添加在头部区域的元素标签为: `<title>`, `<style>`, `<meta>`, `<link>`, `<script>`, `<noscript>`, and `<base>`.

`<title>` 元素:

`<title>` 标签定义了不同文档的标题。
`<title>` 在 HTML/XHTML 文档中是必须的。
`<title>` 元素:
- 定义了浏览器工具栏的标题
- 当网页添加到收藏夹时，显示在收藏夹中的标题
- 显示在搜索引擎结果页面的标题

`<base>` 元素：

`<base>` 标签描述了基本的链接地址/链接目标，该标签作为HTML文档中所有的链接标签的默认链接:
```html
<head>
<base href="http://www.runoob.com/images/" target="_blank">
</head>
```
 `<link>` 元素:

`<link>` 标签定义了文档与外部资源之间的关系。
`<link>` 标签通常用于链接到样式表:
```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

`<style>` 元素:

`<style>` 标签定义了HTML文档的样式文件引用地址.
在`<style>` 元素中你也可以直接添加样式来渲染 HTML 文档:
```html
<head>
<style type="text/css">
body {background-color:yellow}
p {color:blue}
</style>
</head>
```
`<meta>` 元素:

meta标签描述了一些基本的元数据。
`<meta>` 标签提供了元数据.元数据也不显示在页面上，但会被浏览器解析。
META 元素通常用于指定网页的描述，关键词，文件的最后修改时间，作者，和其他元数据。
元数据可以使用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他Web服务。
`<meta>` 一般放置于 `<head>` 区域
```html
<meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">
<meta name="description" content="免费 Web & 编程 教程">
<meta name="author" content="Runoob">
```
`<script>` 元素:

`<script>`标签用于加载脚本文件，如： JavaScript。
```html
<script src="https://gist.github.com/mmistakes/43a355923921d22cd993.js"></script>
```

## HTML字符实体
HTML 中的预留字符必须被替换为字符实体。
HTML无法使用 < 和 > 因为会被浏览器当作标签，这时就需要使用字符实体显示出大于小于号。
如需显示小于号，我们必须这样写：`&lt`; 或 `&#60`; 或 `&#060`

不间断空格使用 `&nbsp`

也可以使用字符实体显示出发音音标。
- [HTML实体参考手册](https://www.runoob.com/tags/ref-entities.html)



## HTML URL
URL - 统一资源定位器。
```html
scheme://host.domain:port/path/filename
```

- scheme - 定义因特网服务的类型。最常见的类型是 http
- host - 定义域主机（http 的默认主机是 www）
- domain - 定义因特网域名，比如 runoob.com
- :port - 定义主机上的端口号（http 的默认端口号是 80）
- path - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
- filename - 定义文档/资源的名称
### 补充
URL 只能使用 ASCII 字符集.
来通过因特网进行发送。由于 URL 常常会包含 ASCII 集合之外的字符，URL 必须转换为有效的 ASCII 格式。
URL 编码使用 "%" 其后跟随两位的十六进制数来替换非 ASCII 字符。
URL 不能包含空格。URL 编码通常使用 + 来替换空格。
