+++
title = "nessus 无法访问的解决办法 for mac and win"
description = ""
date = 2023-06-05T13:00:07+08:00
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "nessus"
]
series = []
images = []
+++
> 本篇内容全程推荐使用chrome而不是safari，safari还是没有办法进入的。

nessus 是一款漏洞扫描软件，在我开始使用mac之后，我尝试安装并使用它，但是出现了一些问题，下面来记录下：

## 正常开启关闭的方法
在mac设置里面，最下面有一个nessus按钮，进去，解锁，然后就可以开启/停止nessus了。
nessus在不扫描的时候几乎没有负载，所以开机启动我也留着了。

开启后，nessus会在此处运行：[https://localhost:8834/##/](https://localhost:8834/##/)

![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/0083vuQJly1h3wgdnrit6j311211mtia.jpg)

![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/0083vuQJly1h3wge5qo83j310m0iajtm.jpg)

## 问题描述
安装nessus后，chrome提示如下：

![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/0083vuQJly1h3wgcgzsytj31wg192b2a.jpg)

## 解决办法

在chrome这个错误界面直接输入： `thisisunsafe` ，然后chrome就明确你知道自己在做什么，然后放行你。

![image](https://image.baidu.com/search/down?url=https://tva1.sinaimg.cn/large/0083vuQJly1h3wgiwv4y9j31tq17g4qp.jpg)

你要打开这个链接(可能需要先登陆):[https://localhost:8834/getcert](https://localhost:8834/getcert) ， 会下载一个证书文件，接下来我们要手动信任这个证书

![image](https://image.baidu.com/search/down?url=https://tvax4.sinaimg.cn/large/0083vuQJly1h3wgksfoc6j30dm050q4c.jpg)

先打开“钥匙串访问”程序，然后双击这个证书文件，证书会自动安装，但是此时是不信任的状态（有个叉叉）

![image](https://image.baidu.com/search/down?url=https://tvax3.sinaimg.cn/large/0083vuQJly1h3wgmol29dj31bk0ruzt1.jpg)

接下来我们需要双击这个证书，然后点开信任菜单栏，并且勾选始终信任，修改后系统会要求sudo权限

![image](https://image.baidu.com/search/down?url=https://tvax3.sinaimg.cn/large/0083vuQJly1h3wgoceajxj30rs0o24dk.jpg)

## 对于 windows 
windows信任证书的操作和mac有些差别：
1. 打开这个链接 :[https://localhost:8834/getcert](https://localhost:8834/getcert) 
2. 安装证书的时候，选择指定存储路径，浏览-受信任的根证书颁发机构
![Imgur](https://i.imgur.com/XTwuUTL.png)

## 结束
这样应该就能正常访问了，以后也不会有问题了。

主要学到了一招就是 `thisisunsafe`  大概能用在任何chrome信任失效界面上，可以去强制访问。

不过我还是不理解，为啥电脑要不信任localhost……

## HSTS 错误

需要解决这个保存，除了打字： `thisisunsafe` ，还可以通过chrome设置来临时放行：

首先打开chrome这个设置界面 [chrome://net-internals/##hsts](chrome://net-internals/##hsts)

滚动到最下方，输入`localhost`，点击`delete`。

![image](https://image.baidu.com/search/down?url=https://tva3.sinaimg.cn/large/0083vuQJly1h3wgy8tcjhj31su0qu11p.jpg)

就可以访问 HSTS 不允许的网站了。