+++
title = "Frp配置指南"
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
https://gist.github.com/cornradio/984f6c17b4f8b3ee47a732c3756dc986 


run
```
screen -S frp
./frps -c frps.toml
```

frps.toml   

```toml
bindAddr = "0.0.0.0"
bindPort = 7000

auth.method = "token"
auth.token = "******"

webServer.addr = "0.0.0.0"
webServer.port = 7500
webServer.user = "***"
webServer.password = "***"
```



## frpc 部署到家中pc等设备

run
```
./frpc -c frpc.toml
```

frpc.toml   
```toml
user = "homepc"
serverAddr  = "139.196.***.***"
serverPort  = 7000

auth.method = "token"
auth.token = "******"

[[proxies]]
name = "mrdp"
type = "tcp"
localIP  = "127.0.0.1"
localPort  = 3389
remotePort  = 33389

[[proxies]]
name = "clash"
type = "tcp"
localIP  = "127.0.0.1"
localPort  = 7890
remotePort  = 7890

[[proxies]]
name = "webalist"
type = "tcp"
localIP  = "192.168.31.11"
localPort  = 5244
remotePort  = 15244

```

## 检查
链接成功后可以在服务器上检查 http://ip:7500 查看frp面板，是否配置成功。
