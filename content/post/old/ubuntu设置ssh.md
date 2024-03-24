+++
title = "ubuntu设置ssh、修改mac地址(home pc)"
description = ""
date = 2022-11-22T22:03:01+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
]
tags = [
"ubuntu","ssh","macaddress"
]
series = []
images = []

+++
> 本教程包含：开启ubuntu ssh server 功能（可以被远程）\修改ubuntu 的 网卡mac地址

1. 安装ssh服务器
```
sudo apt update
sudo apt install openssh-server
```
2. 查看ssh服务器启动状态
```
sudo systemctl status ssh
```
3. 使用内置的防火墙软件允许ssh通过
```
sudo ufw allow ssh
```
4. 查看你的ubuntu ip地址（这条命令会显示所有网卡的ip，选择你觉得最像的那个）
```
ip -f inet address
```

## 笔记本关闭盒盖休眠功能
> ubuntu2204默认开启了笔记本盒盖，系统自动休眠功能，这显然不是我们想要的，因为需要让他在盒盖状态下当一个家庭服务器，所以需要关闭他的[盒盖休眠]功能
> 下面是关闭[盒盖休眠]功能的指南,可以使用`/关键词` 在vi中搜索
```
sudo vi /etc/systemd/logind.conf
```
将其中的
```#HandleLidSwitch=suspend```
改成
```HandleLidSwitch=ignore```


## 修改ubuntu MAC地址
> 单位的内网wifi开启了MAC地址认证功能，只有在清单中的MAC地址可以连接到内网WiFi，我有一个可用的内网mac地址，正好给他上上，然后自己搭建一个私人vpn
1. 安装macchanger
```
apt install macchanger -y
```
2. 查看需要更改的王开名称
```
ip addr sh
```
3. 设定网卡指定ip地址
```
sudo macchanger -m e0:d4:e8:f8:e0:c6 wlp0s20f3
```
4. 查看网卡地址(是否修改成功)
```
macchanger --show wlp0s20f3
```
5. optional：恢复网卡mac地址（恢复成固件地址）
```
macchanger -p wlp0s20f3
```