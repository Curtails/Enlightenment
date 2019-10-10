---
layout: post
title: "BugkuCTF-MISC-WriteUp"
date: 2019-08-21 01:01:01
share: true
toc: true
tags: 
 - CTF
---

BugkuCTF-MISC-WriteUp

## 签到
- 真就白给

## 这是一张单纯的图片
一张普通图片。
- 查看属性没有信息
- WinHex查看信息末尾出有& # 数字组成的的Unicode编码 利用工具转换成ASCII即可。
- key{you are right}

## 隐写
图片隐写。
一个没有密码的rar文件，成功解压出一张图片，显示似乎是不完整的。
- 先看属性啥也没有
- 丢进winhex没有发现异常代码
- 丢进binwalk查看有无包含文件，只有zlib没有异常
- 图片显示残缺通常长宽比例被人为修改
- 回到winhex第二行000001F4 000001A4 修改后者与前者一致即可
- BUGKU{a1e5aSA}

## telnet
telnet协议为tcp/ip协议一员。
一个没有密码压缩包解压得出networking.pcap。
- Wireshark打开
- 右键追踪流-TCP即可看到flag
- flag{d316759c281bf925d600be698a4973d5}

## 眼见非实(ISCCCTF)
一个名字为zip的文件；给他加上后缀zip，解压出一个docx文件。
无法打开。
- 很有可能他不是docx文件，丢进binwalk
- 发现是一个zip文件，改后缀解压，得到许多xml文件。
- xml一个个看吧，在里面。
- flag{F1@g}

## 啊哒
一个压缩文件解压出一个图片。
- 查看属性发现照相机型号是一串hex代码，利用工具转换成text
- 得到sdnisc_2018，不是flag暂时留着
- 丢进winhex在末尾处发现flag.txt字符串，图片一个包含这个文件
- 直接丢进binwalk，验证。果然含有flag.txt并且它本质上是一个压缩文件
- ```
  binwalk -e ada.jpg
  dd if=ada.jpg of=1 skip=218773 bs=1 
  两者都可以分离出flag.txt压缩文件
  ```
- sdnisc_2018是压缩密码，解压得到真正的falg.txt
- flag{3XiF_iNf0rM@ti0n}

## 又一张图片，还单纯吗
一张普通图片。
- 查看属性，无
- 丢进winhex，没啥异常
- 丢进binwalk，有多张图片
- ```
  foremost 2.jpg
  dd if=2.jpg of=1 skip=****** bs=1
  二者皆可
  ```
- 分离出含有flag的图片
- falg{NSCTF_e6532a34928a3d1dadd0b049d5a3cc57}

## 猜
题目说图片这位美女的名字即flag
- 百度识图/谷歌识图
- 如果你认识亦非姐姐那就是姐姐白给你的。

## 宽带泄露
flag为宽带用户名；下载到conf.bin文件。
- 丢进routerpassview 
- 直接搜username得到<Username val=053700357621 />
- flag{053700357621}

## 隐写2
图像隐写。
下载到welcome.jpg 打开嘲讽了我一波。
- 看属性无内容没b数
- 丢进winhex尾部看到了flag.rar字样果然还是先丢进binwalk好了
- binwalk直接`binwalk -e Welcome_.jpg/foremost Welcome_.jpg`走一波
- 拿到提示.jpg及flag.rar
- 提示balabala一大堆告诉我压缩文件密码三位数
- ARCHPR_ha爆破走起，得出密码871
- 解压得3.jpg无属性信息
- 丢进winhex在某位发现`f1@g{eTB1IEFyZSBhIGhAY2tlciE=}`
- flag里面还有个base64，解密即可
- flag{y0u Are a h@cker!}
- bugku服务器bug？flag incorrect？

## 多种方法解决
题目提示会看到一张二维码图片。
下载得到zip文件，解压的KEY.exe
- 会看到图片，丢进winhex
- 发现代码开头有`data:image/jpg;base64`
- 代码全部为base64编码，利用工具把base编码转换成图片
- 得到二维码扫面即可
- KEY{dca57f966e4e4e31fd5b15417da63269}

## 闪的好快
一张二维码gif
- 丢进Stegsolve-打开gif-Analyse-Frame Browser
- 看到十八张二维码，挨个扫
- SYC{F1aSh_so_f4sT}

## come_game
留坑

## 白哥的鸽子
得到名为jpg的文件。
- 价格jpg后缀看到鸽子，无属性信息
- 丢进winhex，没看出异常
- 丢进binwalk正常
- 再次查看winhex，末尾处字符串规整且含有flag字符（分散开）且结尾出有@填充
- 猜测是栅栏密码字符串，用工具解码
- flag{w22_is_v3ry_cool}

## linux
题目提出linux基础问题。
解压的flag文件。
- 在kali使用`cat flag`命令
- 末尾打印出flag
- key{feb81d3834e2423c9903f4755464060b}

## 隐写3
得到压缩文件，解压出一张图片，打开可显示但不完整
- 无属性信息
- 丢进winhex 有了前面经验直接看第二行修改比例
- 修改成`000002A7 000002A7`
- 图片显示完整看到flag
- flag{He1l0_d4_ba1}

## 做个游戏
题目让我坚持60秒，下载得到jar文件；打开嘲讽我只能坚持6秒。
- jar可改后缀为zip解压能看到源文件
- 丢进jd-gui可查看源代码
- cn.bjsxt.plane.PlaneGameFrame中找到flag
- 拿到flag{RGFqaURhbGlfSmlud2FuQ2hpamk=}把里面base64解码一下
- flag{DajiDali_JinwanChiji}

## 想蹭网先解开密码
留坑

## linux2
题目高速key的格式是KEY{}
拿到压缩包解压得到名为brave文件
- 没头绪丢进binwalk发现含有jpg
- 分离得出jpg，图片显示的是flag不是key
- 直接用notepad++打开brave搜索key能找出key{}
- 正确做法是在应该在linux中
  ```
  → ∮ ← :~/桌面# grep "KEY" -an brave 
  PS：a代表二进制问价、n代表字符串出现的位置
  ```
- KEY{24f3627a86fc740a7f36ee2c7a1c124a}

## 账号被盗了
打开题目所给网址-点击getflag-显示not admin
- 久违的burpsuite_pro抓包
  - 监听在Raw中发现`Cookie: isadmin=flase`
  - send to reptater 把值改成true；go
  - 得到 http://120.24.86.145:9001/123.exe
- 或者在firefox中打开控制台
  - 找到存储-cookie-把两个flase值改成true
- 这个网址打不开看来其他的writeup http://123.206.87.240:9001/123.exe
- 下载打开是一个cf刷枪软件
- 打开Wireshark选择环境，开始捕获
- 刷枪，停止捕获，分析
- 发现含有smtp邮箱连接，显然有问题，选中右键追踪流分析
- 看到两条base64字符串
  ```
  YmtjdGZ0ZXN0QDE2My5jb20=
  YTEyMzQ1Ng==
  ```
- 解码的邮箱的账号和密码，登入
- 找到草稿箱中一封邮件告诉我们`KEY{sg1H78Si9C0s99Q}`
- 然而真的flag是`flag{182100518+725593795416}`，上面是假的

## 细心的大象
下载得到zip，解压的jpg
- 看属性得到`TVNEUzQ1NkFTRDEyM3p6`,base64解码得`MSDS456ASD123zz`
- 丢进winhex无异常
- 丢进binwalk `foremost 1.jpg `,得到压缩文件，输入MSDS456ASD123zz解压
- 查看2.png属性无信息，打开显示残缺
- 丢进winhex修改长宽比例为`000001F4 000001F4`
- 打开图片得flag
- BUGKU{a1e5aSA}

## 爆照(08067CTF)
下载得一张图片，穹妹？
题目提示flag由xxx_xxx_xxx，猜测三个字段组成
- 查看属性无信息
- 丢进binwalk，发现含有zip`foremost 8.jpg`分离
- 得到压缩包解压得8个文件和一张gif
- 8个文件没头绪丢进kali里竟然都能识别出图片
- 8文件丢进winhex 末尾处有字符串`flag`
- 88文件有二维码扫描得出`bilibili`
- 888看属性有`c2lsaXNpbGk=` 解码`silisili`
- 8888丢进binwalk含有压缩文件解压得二维码扫描得出`panama`
- 剩下文件没啥
- 得出flag，这题绕
- flag{bilibili_silisili_panama}

## 猫片(安恒)
提示：LSB BGR NTFS
图片隐写
下载得到名为png图片，改后缀看看图片吸一吸
- 看属性啥也没有
- 丢进winhex没看出来
- 丢进binwalk无异常
- 想起提示丢进Stegsolve-Analyse-Data Extract
- RGB勾选000-LSBfirst-BGR preview一下发现
  `
  fffe 89504e470d0a
  `
  明显png但是是以fffe开头 保存丢进winhex
- 移除fffe保存能打开图片是一张而二维码，残缺
- 残缺了就改长宽`00000118 0000008C`前后一致即可
- 扫描二维码得出网盘地址`https://pan.baidu.com/s/1pLT2J4f`
- 下载的flag.rar解压的txt内容没有flag顺便嘲讽一波
- 看一下Hint ntfs没用到 本题存在ntfs数据流
- 使用ntfstreamseditor工具可搜索解压导出的文件夹，可得到数据流flag.pyc导出
- 注意解压要用winrar这款软件！？！？？？？
- 使用在线工具反编译得出代码
- 编写解密代码 找来前辈的
  ```python
  def decode():
    ciphertext = [
        '96', '65', '93', '123', '91', '97', '22', '93', '70', '102', '94',
        '132', '46', '112', '64', '97', '88', '80', '82', '137', '90', '109',
        '99', '112'
    ]
    ciphertext.reverse()
    flag = ''
  for i in range(len(ciphertext)):
        if i % 2 == 0:
            s = int(ciphertext[i]) - 10
        else:
            s = int(ciphertext[i]) + 10
        s = chr(i ^ s)
        flag += s
    return flag


  def main():
    flag = decode()
    print(flag)


  if __name__ == '__main__':
        main()
  ```
- 运行得出flag
- flag{Y@e_Cl3veR_C1Ever!}

## 多彩
下载得到一张名为lipstick.png普通图片
- 看属性无信息
- 这题涉及口红色号、白学家？！ 太难留坑不做了


## 旋转跳跃
题目：熟悉的声音中貌似又隐藏着啥，key：syclovergeek
下载得到压缩文件解压得sycgeek-mp3.mp3
- 用MP3Steno结合key解码
  `Decode.exe -X -P syclovergeek sycgeek-mp3.mp3`
- 得到 sycgeek-mp3.mp3.txt打开即密码
- SYC{Mp3_B15b1uBiu_W0W}

## 普通的二维码
下载得misc80.zip，解压得misc100.bmp 是一张二维码
- 扫描的文本`哈哈!就不告诉你flag就在这里!`
- 看一眼属性无信息
- 丢进binwalk无异常
- 丢进winhex末尾处有字符串
  ```
  146154141147173110141166145137171060125137120171137163143162151160164137117164143137124157137124145156137101163143151151041175
  ```
- 分析一波数字最带为7 感觉八进制，转ASCII试试（三个数字为一组）
- flag{Have_y0U_Py_script_Otc_To_Ten_Ascii!}

## 乌云邀请码
下载解压得misc50.png 图片内容是一份来自乌云得邮件信息（哀悼乌云）
- 无属性信息
- 丢进binwalk无异常
- 丢进winhex无异常
- 考虑隐写丢进Stegsolve lbsfirst及BGR
- 看到flag 多余空格删掉
- flag{Png_Lsb_Y0u_K0nw!}

## 神秘的文件
下载解压包解压得logo.png和flag.zip flag.zip有密码
- flag.zip丢进winhex查看是否伪加密
- 全局加密和全局方式标记皆为`0900`，真加密
- 丢进ARCHPR_ha 我们选择明文攻击因为zip文件中含有logo.png 我们有此png 压缩png得logo.zip
- ！！要用winrar这个软件压缩:) 成功得密码`q1w2e3r4  `
- 解压得docx打不开 丢进binwalk分离
- 得flag.txt
- flag{d0cX_1s_ziP_file}

## 论剑
题目赋诗一首：
剑客
十年磨一剑，霜刃未曾试。
今日把示君，谁有不平事。
下载得lunjian.jpg 正常打开显示ctf论剑场
- 查看属性无信息
- 丢进binwalk分理出一样的图片未果
- 丢进Stegsolve未果
- 丢进winhex发现
  ```
  1101101 01111001 01101110 01100001 01101101 01100101 01101001 01110011 01101011 01100101 01111001 00100001 00100001 00100001 01101000 01101000 01101000
  ```
  猜测二进制转换成ASCII
- 得出`mynameiskey!!!hhh`
- 修改图片长宽比由于是jpg FFC2 后3个字节的4个字节是高宽
- 能显示有残缺的字符串图片
- 继续分析jpg 01101000紧跟着7z标识 修复标识为`27 7A BC AF 27 1C`
- 丢进binwalk分理处7z输入`mynameiskey!!!hhh`解压得图片继续修改高宽
- 显示残缺字符串图片与上一张互补
- 得到字符串 base16解码
- flag{my_name_H!!H}

## 图穷匕见
下载得正常图片paintpaintpaint.jpg
- 看属性有信息“会画图吗？”
- 丢进winhex发现hex代码 解码得出一堆坐标 去掉()和逗号换为空格保存为txt
- 利用gnuplot根据坐标画图得出二维码
  ```
  gnuplot
  plot "1.txt"
  ```
- 扫码得出flag
- flag{40fc0a979f759c8892f4dc045e28b820}

## convert
convert意思为转换 下载得到内容很长的txt 由二进制组成
- 转换成hex 发现
  ```
  52617221 ......
  ```
- 发现是以`5261 7221`开头是rar标识 打开winhex写入hex保存为rar
- 解压得图像 看属性得base64 解码
- flag{01a25ea3fd6349c6e635a1d0196e75fb}

## 听首音乐
题目：听首音乐放松放松吧~
我：好的我不做了你能给我flag吗？
获得stego100.wav 带上耳机听听
喵喵喵？只有右声道？左声道好像听见了电报声？！
- 丢进Audacity拉长轨道能看见莫斯电码
  ```
  ..... -... -.-. ----. ..--- ..... -.... ....- ----. -.-. -... ----- .---- ---.. ---.. ..-. ..... ..--- . -.... .---- --... -.. --... ----- ----. ..--- ----. .---- ----. .---- -.-. 
  ```
- 解码即可
- flag为5BC925649CB0188F52E617D70929191C

