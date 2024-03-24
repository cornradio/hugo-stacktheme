+++
title = "Python Win 安装"
description = ""
date = 2023-07-14T15:12:50+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "python"
]
series = []
images = []
+++

<!--more-->

当你在一台新的 windows 设备的 命令行 中输入 python / python3 时，会提示你安装 python ，并把你拐到**微软商店**下载。

但是微软商店的版本python有坑！ 

---

## 对于已经被微软商店下毒的电脑

- 关闭 **应用执行别名** 中的 python  [例图](https://i.imgur.com/4nRyMIh.png)
- 执行这些步骤[对于新电脑执行](#对于新电脑)

---

## 对于新电脑

- 正确的下载地址 [python.org](https://www.python.org/downloads/)
- 在安装时候要勾选 **Add to PATH** 选项 ![Imgur](https://i.imgur.com/Ea1cXXL.png)
- 下图可以看到他安装程序添加的系统变量
![Imgur](https://i.imgur.com/aAmq5Wx.png)

--- 

## 对于装了一堆垃圾的windows
电脑有 3-4 个python环境的，只能去卸载python，然后手动清理掉之前的环境变量，再重新安装。

## pip换源
[参考](https://cornradio.github.io/hugo/posts/pip%E9%85%8D%E7%BD%AE%E6%BA%90/)