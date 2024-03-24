+++
title = "在macos上面安装burpsuite（crackverison）"
description = "111"
date = 2022-12-19T12:18:50+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "burp"
]
series = []
images = []
+++

> 下载：[java-jdk](https://www.oracle.com/java/technologies/downloads/) ｜ [破解版 burpsuite](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=burpsuite%20%E7%A0%B4%E8%A7%A3%E7%89%88%202023&oq=burpsuite%25E7%25A0%25B4%25E8%25A7%25A3%25E7%2589%2588%2520202%2526lt%253B&rsv_pq=95921bbe00081999&rsv_t=ef27GuFUOmyrbfwFDhdlPCtYjqy2aAuuaAKNGIB9hiok3BfZaI3I2lHSKPQ&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_btype=t&inputT=8287&rsv_sug3=18&rsv_sug1=16&rsv_sug7=100&rsv_sug2=0&prefixsug=burpsuite%2520%25E7%25A0%25B4%25E8%25A7%25A3%25E7%2589%2588%2520202%2526lt%253B&rsp=6&rsv_sug4=8309)

## 正常顺序
1. 打开：burploader.jar
2. 通过: burploader 打开burp pro
3. 输入 license 然后手动粘贴到 burploader，burploader 解密后给你返回一个 respond 字符串，粘贴进入，破解成功。
4. 后续每次从 loader 中打开文件即可。

## 实际情况
1. 打开：burploader.jar
2. 通过burploader 打开burp pro
3. 打开失败，报错


## 解决办法
主要原因是burp不是很兼容java 17+，所以破解的步骤就是：

1. 打开：burploader.jar
2. 通过手工输入命令，打开 burp pro，并指定 burploader 作为-noverify参数
```
java -jar --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.desktop/javax.swing=ALL-UNNAMED loader.jar
```
1. 正常流程激活(因为我激活过了不能再来一遍所以没有截图了)
2. 制作一个脚本（.bat / .sh）用于方便后面启动burp

# mac快速启动脚本
在zshrc中增加一条快速启动burp的命令/alias，（此时，你的burp应该已经完成了激活操作。
其中分为两步骤：
1. cd 到 burpsuite 目录。
2. 执行命令，用loader 挡住 agent ， 启动 burp.jar ， 加入了一些java17的 flag。
```sh
alias bp="cd /Users/kasusa/BurpSuite_pro_v2023.3&&java -noverify -javaagent:burp-loader-keygen-2_1_06.jar -jar --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.desktop/javax.swing=ALL-UNNAMED burpsuite_pro_v2023.3.jar"
```