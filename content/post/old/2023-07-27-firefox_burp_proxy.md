+++
title = "Firefox 配置 burp_proxy 和 证书"
description = ""
date = 2023-07-27T12:39:49+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  ""
]
series = []
images = []
+++

## 安装代理拓展
安装拓展：

chrome ： [switchomega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif?hl=zh-CN)

firefox ： [foxyproxy](https://addons.mozilla.org/zh-CN/firefox/addon/foxyproxy-standard/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)

创建代理 ： `127.0.0.1:8080`

## 安装burp证书
1. 先开启burp，然后切换到 burp 的代理
2. 访问 https://burp/ 下载证书
3. 打开firefox设置 - 搜索”证书“ - 查看证书 - 导入 - 选择刚刚下载的证书


