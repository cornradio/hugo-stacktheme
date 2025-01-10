+++
title = "如何使用FRP 2.0"
description = ""
date = 2025-01-10T08:56:19+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "frp"
]
series = []
images = []

+++

FRP是一个开源的内网穿透软件，本文将会介绍如何使用frp。

[frp - github](https://github.com/fatedier/frp)

# 原理解释


## 下载和安装

从github下载之后我们会得到这些文件：

```sh
frpc		放在本地server上
frpc.ini	frpc的配置文件
frpc_full.ini	frpc的配置文件（有完整的注释和例子）
```

```sh
frps		放在云服务器上
frps.ini	frps的配置文件
frps_full.ini	frps的配置文件（有完整的注释和例子）
```

<img width="542" alt="image" src="https://github.com/user-attachments/assets/b3448c76-054b-4b8e-ad84-6575071989fa" />

## frps 部署到服务器
参考使用这个脚本：
<script src="https://gist.github.com/cornradio/984f6c17b4f8b3ee47a732c3756dc986.js"></script>

## frpc 部署到家中pc等设备
frpc.toml
```toml
[common]
server_addr = "<your_server_ip>"
server_port = 7000
token = "your_token" # 可选，如果用了密码则需要

# TCP 端口转发示例
[tcp_8080_to6000]
type = "tcp"
local_ip = "127.0.0.1"
local_port = 8080
remote_port = 6000

# 转发内网其他设备
[localserver80to80]
type = "tcp"
local_ip = "192.168.1.4"
local_port = 80
remote_port = 80
```

```
./frpc -c frpc.toml
```

## 检查
链接成功后可以在服务器上检查 http://ip:7500 查看frp面板，是否配置成功。
