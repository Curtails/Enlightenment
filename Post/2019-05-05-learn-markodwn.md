---
layout: post
title: "学习Markdown"
date: 2019-05-05 01:01:01
share: true
toc: true
tags: 
 - Markdown
---

Markdown是一种高效的标记语言，写下此篇关于学习Markdown的文章方便日后复习Markdown。

## 1.什么是Markdown

> Markdown是一种高效的标记语言，采用标记符号的方式实现Word的关于文字排版、文字样式等功能。因为Markdown是纯文本格式，所以我们可以更好的专注于文字内容。

## 2.为什么学习Markdown

从四个方面解释我学习Markdown的原因。

- Markdown的优点：
  - 专注文字内容而不是文字排版
  - 纯文本跨平台
  - 可以导出html、pdf、.md等格式
  - 简洁高效

- Markdown的缺点：
  - 与Word这种富文本编辑器相比，排版性很差
  - 扩展语法多种多样比较混乱
  - 需要网站、软件支持Markdown语法

- 个人习惯：

  跟Word这种需要边编辑文字边进行图形化的排版操作相比，Markdown只需要键盘打字就够了，正是这种纯文本方式吸引了我。尤其对于拥有Thinkpad的人，加上小红点的辅助真正解放了鼠标。

- Blog：

  我通过[Gridea](<https://gridea.dev/>)成功搭建了Github Pages。

  Gridea是一个强大的静态blog写作客户端，它外观非常好看，支持多平台、Katex 公式、以及Markdown。

## 3.如何学习Markdown

多参考Markdown语法，多练习。

随着Markdown的普及，Markdown的语法功能也不断的扩展，不同的编辑器语法支持可能会有偏差。

- Markdown语法标准：
  - [Github Flavored Markdown](https://help.github.com/en/articles/basic-writing-and-formatting-syntax#section-links)（由Github推出的版本）
  - [Typora Markdown Reference](http://support.typora.io/Markdown-Reference/) （我使用的编辑器参考）

- 练习：

  没什么好说的，多用Markdwon写文章就熟能生巧了吧。

## 4.Markdown基本语法

语法在Github Flavored Markdown中介绍的很清楚，总结一些简单的。

- 标题：

  在标题名前加 #，标题和符号之间要有空格，#数量越多标题就越小，#数量最多6个。

  ```
  # 标题
  ## 小标题
  ### 小小标题
  #### 小小小标题
  ......
  ```

  # 标题
  ## 小标题
  ### 小小标题
  #### 小小小标题

  ......

- 文字样式：

  符号与文字之间没有空格。

  | 样式             | 格式               | 快捷键              | 举例                                     | 输出                                |
  | :--------------- | :----------------- | :------------------ | :--------------------------------------- | :---------------------------------- |
  | 加粗             | `** **` or `__ __` | command/control + b | `**This is bold text**`                  | **This is bold text**               |
  | 斜体             | `* *` or `_ _`     | command/control + i | `*This text is italicized*`              | *This text is italicized*           |
  | 删除线           | `~~ ~~`            |                     | `~~This was mistaken text~~`             | ~~This was mistaken text~~          |
  | 加粗和斜体一起用 | `** **` and `_ _`  |                     | `**This text is _extremely_ important**` | **This text is extremelyimportant** |



- 引用：

  符号与文字之间有空格。

  ```
  乔布斯在斯坦福大学演讲中给年轻人一个建议：
  > Stay hungry Stay foolish
  ```

  乔布斯在斯坦福大学演讲中给年轻人一个建议：

  > Stay hungry Stay foolish

- 代码段：

  ```
  ​```c++		//c++代码高亮可替换其他编程语言
  int main(){
  	cout<<"Hello World"<<endl;
  	return 0;
  }
  ​```
  ```

  以下是代码段输出效果

  ```c++
  int main(){
  	cout<<"Hello World"<<endl;
  	return 0;
  }
  ```

- 超链接

  ```
  [乔布斯在斯坦福大学演讲视频](https://www.bilibili.com/video/av8287999)
  ```

  [乔布斯在斯坦福大学演讲视频](https://www.bilibili.com/video/av8287999)

- 插入图片

  ```
  ![](http://imglf4.nosdn0.126.net/img/SmlBNVNYWEwrN0VKeGkrbDFKb2xCREx1UnFabzMxRUZBSzlFSS9CNmNxQkRFN1BEeG1EcExBPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)
  ![Darling in the frankxx](http://imglf4.nosdn0.126.net/img/SmlBNVNYWEwrN0VKeGkrbDFKb2xCREx1UnFabzMxRUZBSzlFSS9CNmNxQkRFN1BEeG1EcExBPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)
  ```

  ![](http://imglf4.nosdn0.126.net/img/SmlBNVNYWEwrN0VKeGkrbDFKb2xCREx1UnFabzMxRUZBSzlFSS9CNmNxQkRFN1BEeG1EcExBPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)
  
  ![Darling in the frankxx](http://imglf4.nosdn0.126.net/img/SmlBNVNYWEwrN0VKeGkrbDFKb2xCREx1UnFabzMxRUZBSzlFSS9CNmNxQkRFN1BEeG1EcExBPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0)

- 列表

  符号与文字之间有空格，符号为-或* 

  ```
  - 以下为无序列表
  - 列表1
  - 列表2
  	- 列表2.1
  - 列表3
  ```

  - 列表1
  - 列表2
  	- 列表2.1
  - 列表3

  - 1. 有序列表1
  - 2. 有序列表2
  - 3. 有序列表3

  ```
  - 1. 有序列表1
  - 2. 有序列表2
  - 3. 有序列表3
  ```

  

- 任务列表

  ```
    - [ ] 看番
    - [x] 写文章
    - [ ] 学习
  ```
  
    - [ ] 看番
    - [x] 写文章
    - [ ] 学习
  
- 流程图

  ```
  ​```flow
  st=>start: Start
  op=>operation: Your Operation
  cond=>condition: Yes or No?
  e=>end
  
  st->op->cond
  cond(yes)->e
  cond(no)->op
  ​```
  ```

  ```flow
  st=>start: Start
  op=>operation: Your Operation
  cond=>condition: Yes or No?
  e=>end
  
  st->op->cond
  cond(yes)->e
  cond(no)->op
  ```

- 表格

  ```
  | 项目        | 价格   |  数量  |
  | --------   | -----:  | :----:  |
  | 计算机     | \$1600 |   5     |
  | 手机        |   \$12   |   12   |
  | 管线        |    \$1    |  234  |
  ```

  | 项目   |   价格 | 数量 |
  | ------ | -----: | :--: |
  | 计算机 | \$1600 |  5   |
  | 手机   |   \$12 |  12  |
  | 管线   |    \$1 | 234  |

- 忽略Markdown语法

  ```
  Markdown是一个\*标记语言\*。
  Markdown是一个*标记语言*。
  ```

  Markdown是一个\*标记语言\*。
  Markdown是一个*标记语言*。

- 使用 emoji

  ```
  学会Markdown，真开心:grin:
  ```

  学会Markdown，真开心:grin:
  
- 脚注

  ```
  You can create footnotes like this[^footnote].
  
  [^footnote]: Here is the *text* of the **footnote**.
  ```

  You can create footnotes like this[^footnote].

  [^footnote]: Here is the **text** of the ***\*footnote\****.

## 5.Markdown编辑器

-  Windows：Typroa or vscode&插件

  PC端刚开始就用这个，边写边输出是它的特点，界面简洁功能丰富。

- Android：易写

  暂时在移动端用这个。

## 6.Markdown相关

-  [在线编写网站](<https://www.zybuluo.com/mdeditor#>)
- [Github Flavored Markdown](<https://help.github.com/en/articles/basic-writing-and-formatting-syntax#section-links>)
- [Typora support](<http://support.typora.io/>)
- [Markdown emoji](<https://blog.csdn.net/qq_41139830/article/details/85228748>)



