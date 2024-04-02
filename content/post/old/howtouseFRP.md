+++
title = "如何使用FRP"
description = ""
date = 2022-03-12T08:56:19+08:00
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

**背景**

- 我们有一台能访问公网，但是没有公网ip（不能为外部提供服务的server）
- 我们有一台阿里云之类的**云服务器**，有公网ip

**目的**

- 让**不能为外部提供服务的server** 借用**云服务器**转发，从而为公网提供服务

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

![0F7357E41313BFC9B317E8F17213C134](https://image.baidu.com/search/down?url=https://tva3.sinaimg.cn/large/006rgJELly1h06twcbshjj31g10u2wmo.jpg)

# 配置文件怎么写

以防我写的不对，首先推荐看这里：[github官方例子](https://github.com/fatedier/frp/tree/dev/conf)

## frps.ini

```sh
[common] 
#开一个端口，用于转发信息的接收
bind_port = 7000
#开一个监控台，可以在web上面直观的看到frp运行情况
dashboard_addr = 0.0.0.0
dashboard_port = 7500
```

然后把`frps`、`frps.ini` 放到服务器上，赋予执行权限（我就无脑chomd777)

记得把云服务器的安全组策略（在云服务商的控制台界面里面）打开，然后就可以去编辑frpc了



## frpc.ini

```sh
[common]
#输入你服务器的ip、服务器的接收端口，进行frp链接
server_addr = x.x.x.x
server_port = 7000

[ssh]
#开启一些其他的转发，比如ssh，按照下面配置相当于把 127.0.0.1:22 转发到 x.x.x.x:6000
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

# tcp和udp端口转发等
[range:tcp_port]
type = tcp
local_ip = 127.0.0.1
local_port = 6010-6020,6022,6024-6028
remote_port = 6010-6020,6022,6024-6028
use_encryption = false
use_compression = false

[range:udp_port]
type = udp
local_ip = 127.0.0.1
local_port = 6010-6020
remote_port = 6010-6020
use_encryption = false
use_compression = false

```



# 服务启动

```sh
# 在云上启动服务端（接受和转发）（推荐用screen）
./frps -c ./frps.ini

# 在本地启动客户端（发送）
./frpc -c ./frpc.ini
```

本地成功的输出：

```sh
2022/03/12 08:54:09 [I] [service.go:178] [356c08cc36fd0fc1] try to reconnect to server...
2022/03/12 08:54:09 [I] [service.go:325] [356c08cc36fd0fc1] login to server success, get run id [356c08cc36fd0fc1], server udp port [0]
2022/03/12 08:54:09 [I] [proxy_manager.go:144] [356c08cc36fd0fc1] proxy added: [ssh]
2022/03/12 08:54:09 [I] [control.go:181] [356c08cc36fd0fc1] [ssh] start proxy success

```

云端成功的输出：

```sh
root@VM-12-6-ubuntu:/home/frp# sudo ./frps -c ./frps.ini
2022/03/12 08:53:51 [I] [root.go:200] frps uses config file: ./frps.ini
2022/03/12 08:53:51 [I] [service.go:193] frps tcp listen on 0.0.0.0:7000
2022/03/12 08:53:51 [I] [service.go:292] Dashboard listen on 0.0.0.0:7500
2022/03/12 08:53:51 [I] [root.go:209] frps started successfully
2022/03/12 08:54:06 [I] [dashboard_api.go:70] Http request: [/api/serverinfo]
2022/03/12 08:54:06 [I] [dashboard_api.go:63] Http response [/api/serverinfo]: code [200]
2022/03/12 08:54:09 [I] [service.go:449] [356c08cc36fd0fc1] client login info: ip [211.161.248.81:2910] version [0.40.0] hostname [] os [linux] arch [amd64]
2022/03/12 08:54:09 [I] [tcp.go:64] [356c08cc36fd0fc1] [ssh] tcp proxy listen port [6000]
2022/03/12 08:54:09 [I] [control.go:465] [356c08cc36fd0fc1] new proxy [ssh] success
```

# 检查frp控制台

![image](https://image.baidu.com/search/down?url=https://tvax1.sinaimg.cn/large/006rgJELly1h06ueiqri1j310k0izwis.jpg)

