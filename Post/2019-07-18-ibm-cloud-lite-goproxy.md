---
layout: post
title: "Install Goproxy with IBM Cloud Lite"
date: 2019-07-18 01:01:01
share: true
toc: true
tags: 
 - Goproxy
---

Goproxy is a powerful proxy.

## IBM Cloud Lite 特点

- 免费使用
- 无需信用卡
- 账户永不过期

## IBM Cloud Lite 创建

### 注册IBM账户（略）

[IBM Cloud官网](https://cloud.ibm.com/)

- 注册有谷歌验证需要梯子

### 创建资源

- 创建轻量PHP应用

![](https://i.loli.net/2019/07/18/5d304c07597c026701.png)



- 填写应用程序名称
- 选择域（推荐cf.appdomain.cloud）
- 选择位置（推荐达拉斯）
- 选择价格套餐（免费最多可选256M）

![](https://i.loli.net/2019/07/18/5d304cd9efc4b73464.png)

- 创建之后启动该应用

![](https://i.loli.net/2019/07/18/5d304e0adf4c124800.png)

## 安装 Goproxy

### 使用在线SSH连接应用

- 打开应用查看概述

![](https://i.loli.net/2019/07/18/5d304f6c869e518546.png)

- 点击运行时-SSH

![](https://i.loli.net/2019/07/18/5d304fce9e92d85479.png)

### 部署Goproxy服务端

- 在SSH执行以下命令即可

```
cd /home/vcap/app/htdocs
rm -rf *
git clone https://github.com/malaohu/goproxy-php.git && mv goproxy-php/* ./
```

### 部署Goproxy本地端

- 下载本地端

  [下载地址](https://pan.black1ce.com/GAE%E7%B1%BB%E4%BB%A3%E7%90%86/Goproxy%2064%E4%BD%8D.7z)

- 解压后打开php.json

  ![](https://i.loli.net/2019/07/18/5d30540907ea457856.png)

- 需要修改三个位置URL、Password 以及SSLVerify

  "URL":"访问应用程序URL//index.php"

  本地端Password与服务端goproxy.php中Password保持一致 本例中"Password":"123456"

  SSLVerify ：URL为https则为true；http则为flase

- 修改浏览器端口为8080并运行goproxy-gui.exe即可使用



## 提升使用体验

### 使用SwitchyOmega管理代理

- 安装chrome插件SwitchyOmega

- 创建一个新的情景模式

  ![](https://i.loli.net/2019/07/18/5d3056f77e8f587733.png)

- 使用Goproxy时切换代理；不使用时还原代理

  ![](https://i.loli.net/2019/07/18/5d30573c88d8e93437.png)

- 此扩展方便切换代理



### 防止PHP应用程序休眠

根据IBM Cloud规则，10天应用程序不活跃就要休眠。

我们可以使用云监控避免不活跃导致休眠。

国内的免费云监控很多，例如[阿里云云监控](https://www.aliyun.com/product/jiankong/)。

![](https://i.loli.net/2019/07/18/5d305917a661467035.png)

- 点击站点监控-站点管理-新建监控任务

![](https://i.loli.net/2019/07/18/5d30598c98e2f46155.png)

- 按照说明设置即可