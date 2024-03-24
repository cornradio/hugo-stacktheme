+++
title = "windows酷命令"
description = ""
date = 2022-10-29T23:00:17+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "cmd"
]
series = []
images = []

+++
> 如果你更喜欢看视频：https://www.youtube.com/watch?v=Jfvg3CS1X3A&t=1s

有些命令需要使用到管理员权限。推荐直接打开一个拥有管理员权限的cmd窗口！

--网络方面的命令比较多

---

 检查一下网卡情况

```bat
ipconfig /all
```

 清除网络

```
ipconfig /release
```

 刷新获取ip

```
ipconfig /renew
```

 展示所有已知dns(并复制到剪切板)

```bat
ipconfig /displaydns | clip
```

 刷新dns（从dns服务器重新拉）

```
ipconfig /flushdns
```


 查dns字典（域名获取ip）

```
nslookup networkchuck.com
```

 你还可以指定dns服务器

```
nslookup baidu.com 8.8.8.8
```

 不知道干啥的

```
nslookup -type=ptr baidu.com
```


❤ 获取mac地址

```
getmac /v
```


 一些系统报告

```
powercfg /energy
```


```
powercfg /batteryreport
```


 检查一下文件默认启动关联

```
assoc
```


❤ 检查一下电脑的系统文件问题

```
sfc /SCANNOW
```


 查看正在运行的程序 类似ps

```
tasklist |findstr QQ
```

 kill （强制、指定pid）

```
taskkill /f /pid 40232l
```


❤ 更高级的网络报告

```
netsh wlan show wlanreport
```


 关闭、打开防火墙

```
netsh advfirewall set allprofiles state off
```


```
netsh advfirewall set allprofiles state on
```


 ping 和 不停的ping

```
ping baidu.com
```


```
ping -t baidu.com
```


 路由追踪

```
tracert -d baidu.com
```


❤ 查看当前端口开放情况

```
 netstat -af
```

135的作用就是进行远程，可以在被远程的电脑中写入恶意代码，危险极大
139、445文件和打印机共享，可以用于开启空会话
3389端口是Windows远程桌面的服务端口
1024端口一般不固定分配给某个服务，在英文中的解释是“Reserved”（保留）。之前，我们曾经提到过动态端口的范围是从1024～65535，而1024正是动态端口的开始

 展示电脑内路由表,可以修改

```
route print 
```


```
route add x.x.x.x mask 255.255.255.0 x.x.x.x
```


```
route delete x.x.x.x
```


❤ 关机(完全重启 重启到bios 强制 时间0)

```
shutdown /r /fw /f /t 0
```
