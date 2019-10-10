---
layout: post
title: "BugKuCTF-论剑场-MISC-WriteUp"
date: 2019-08-31 01:01:01
share: true
toc: true
tags: 
 - CTF
---

BugKuCTF-论剑场-MISC-WriteUp

## 头像
得一张可爱妹子照片
hint：flag为flag{flag的md5 32位加密值}
- 丢进winhex 搜索flag得 `flag{bGxvdmV0aGVnaXJs}`
- 将{}内容base64解码 在MD5加密
- 补全flag格式

## 签到
白给

## 0和1的故事
hint；听说空格和零很配
此题想法有些牵强
- 下载得压缩包不断解压得txt 内容显示`Flag_is_not_here`加一堆空格
- 丢进winhex发现有规律hex
  ```
  0920200920092009092009200920090920200920200909092020200909092009200920090909092020202009090920090909090909202020202020
  ```
  对照右侧ascii判断20是对应空格的 听说空格和0很配所以把20当作0 09当作1
- 转换得`10010101101010110010011100011101010111100001110111111000000`
- 转换hex`4ad5938eaf0efc0`
- flag{4ad5938eaf0efc0}

## 这个人真的很高
下载得一图片
- 丢进winhex 末尾发现`aabI11us11ts1yy0}`
- 很高 那就改高加长一点改个800 打开图片得`ffoEliuaanrsgDey{`
- 拼起来`ffoEliuaanrsgDey{aabI11us11ts1yy0}`栅栏密码
- 傻了 解不出来 查了其他人writeup最后靠猜？`flag{Iss0@finDa111}@ourea11y@@Easybuty@@` to `flag{Iss0Easybutyourea11yfinDa111}`

## snake
hint：攒够500分就给flag哦
竟然要500 王校长能吃那么多的面包吗
- jd gui反编译出java代码 搜索flag 得到相关函数
```java
    if (this.score >= 500 && 
      this.isshow) {
      String flag = "eobdxpmbhf\\jpgYaiibYagkc{";
      int key = this.snake.len - this.score;
      String xx = "";
      for (int i = 0; i < flag.length() / 2; i++) {
        
        int c = flag.charAt(i);
        char c1 = (char)(c ^ key);
        xx = String.valueOf(xx) + c1;
      } 
      for (int i = flag.length() / 2 + 1; i < flag.length(); i++) {
        
        int c = flag.charAt(i);
        char c1 = (char)(c ^ key * 2);
        xx = String.valueOf(xx) + c1;
      } 
      
      JOptionPane.showInputDialog(null, "This is your flag CALCULATE BY YOUR SCORE:\n", "Congratulations", -1, null, null, 
          xx);
      
      this.isshow = false;
    } 
```
- 可以看出这是一个求flag算法 没有直接给出flag
- 构造程序payload.java
```java
public class payload {

    public static void main(String[] args) {
      String flag = "eobdxpmbhf\\jpgYaiibYagkc{";
      int key = 3;
      String xx = "";
      for (int i = 0; i < flag.length() / 2; i++) {
        int c = flag.charAt(i);
        char c1 = (char)(c ^ key);
        xx = String.valueOf(xx) + c1;
      } 
      for (int i = flag.length() / 2 + 1; i < flag.length(); i++) {
        int c = flag.charAt(i);
        char c1 = (char)(c ^ key * 2);
        xx = String.valueOf(xx) + c1;
      } 
      System.out.println(xx);
    }
}
```
- 运行得flag
- 或者直接上修改器 修改 长度 分数 
- flag{snake_ia_good_game}

## easypdf
下载解压得easy.pdf打显示好像不完整的图片
- 丢进Adobe Acrobat DC 把图片挪一下 能看到背后的flag


## 损坏的图片
下载得无法打开的图片
- 丢进winhex观察结尾`47 4E 50 89`很明显是png`89 50 4E 47`倒序
- 我们把整个文件hex倒序过来
```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int main()
{ 
    char a[15000]="hex";//hex太长
    char b[15000];
    for(int i =0;i<strlen(a);i=i+2){

        b[i]=a[strlen(a)-2-i];
        b[i+1]=a[strlen(a)-1-i];
    }
    for(int i =0;i<strlen(a);i++){

        cout<<b[i];
    }
    return 0;
}
```
- 得到反转之后的hex在winhex新建粘贴保存位1.png
- 打开图片为二维码 扫描即可
- flag{f3f4a1a0d4e8e8e1f4a0f}

## 怀疑人生
下载解压得ctf1.zip ctf2.jpg ctf3.jpg
- ctf1.zip有密码丢进winhex查看真加密 尝试暴力无果 尝试字典得密码`password`
  - 解压打开txt得字符串base64-去掉\u hex解码 得`flag{hacker` 
- ctf2.jpg丢进binwalk分离zip解压打开txt Ook!解码得`3oD54e`
  - 在进行base58解码字符串？？？`misc`
- ctf3.jpg扫描即可`12580}`
- 拼起来flag{hackermisc12580}

## 向日葵
解压得一张图片
- 丢进binwalk分离rar解压得txt打开
```
在一个a[5][5]的二维数组中有下列几个元素
（2,5）
（5,1）
（2,4）
（2,5）
（3,5）
（3,2）
（1,4）
（5,1）
（2,2）
（2,5）
（4,5）
（2,1）
（1,2）
（4,5）
（5,5）
那么flag是什么呢？
```
- 类似于棋盘密码
```
  1 2 3 4 5
l a b c d e
2 f g h i j
3 k 1 m m o
4 p q r s t
5 u v w x y
```
- 根据坐标得`juijoldugjtfbty`
- 凯撒密码遍历得`ithinkctfiseasy` 题目牵强
- flag{ithinkctfiseasy}

