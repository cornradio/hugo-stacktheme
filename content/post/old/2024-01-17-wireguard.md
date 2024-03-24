+++
title = "Wireguard-管线卫士"
description = ""
date = 2024-01-17T15:46:23+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "linux"
]
series = []
image = "wireguard.png"

+++

<!--more-->

## 简易安装：
https://github.com/xubiaolin/wireguard-onekey
使用run.sh之前可以按照需要 设置一下脚本里面的  WG_ALLOWED_IPS=10.0.8.0/24 ，改成 0.0.0.0/0 可以全流量走vpn

```
git clone https://github.com/xubiaolin/wireguard-onekey.git

bash run.sh
```

![Imgur](https://i.imgur.com/raBKUVP.png)

## wg-easy

上面的onekey脚本实际上是用了另一个项目：[wg-easy](https://github.com/wg-easy/wg-easy)

wg-easy 有一些奇怪的问题
1. 使用vps时，联入wg vpn之后就不能上网了，详见这个 [issue](https://github.com/wg-easy/wg-easy/issues/562)。 
2. 默认镜像的位置是： ghcr.io/wg-easy/wg-easy ， ghcr.io访问极慢（即使挂了代理），所以我用在线docker机器人重新拉取了一个放到了这里： togettoyou/my-wg-easy:nightly

```sh
docker run -d \
  --name=wg-easy \
  -e WG_HOST=<your-ip>  \
  -e PASSWORD=<your-password> \
  -v ~/.wg-easy:/etc/wireguard \
  -e WG_DEVICE=eth0 \
  -p <your-port>:51820/udp \
  -p <your-port>:51821/tcp \
  --cap-add=NET_ADMIN \
  --cap-add=SYS_MODULE \
  --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
  --sysctl="net.ipv4.ip_forward=1" \
  --restart unless-stopped \
  togettoyou/my-wg-easy:nightly
```
访问这个链接来使用你的vpn管理台。
```
http://<your-ip>:<your-port>
```

## 客户端下载
安装好了之后我们就要使用它，首先我们需要下载客户端，这里提供了一些下载链接：

win

https://download.wireguard.com/windows-client/ 

mac(外区商店)

https://apps.apple.com/us/app/wireguard/

linux

```shell
sudo apt install wireguard-tools
sudo apt install resolvconf

wg-quick up ./wg.conf 
```


## 配置文件
wg 的客户端配置中有一个非常方便的东西，AllowedIPs

AllowedIPs 可以用作一个路由表。可以限定访问的范围

```sh
# 全局vpn
0.0.0.0/0
# 网段 192.168.1.x 和 10.0.1.x 走vpn
192.168.1.0/24,10.0.1.0/24
```


```
[Peer]
AllowedIPs = 192.168.124.0/24
```
