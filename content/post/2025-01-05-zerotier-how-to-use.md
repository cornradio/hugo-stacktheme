---
title: zerotier 入门指南
date: 2025-01-05 00:00:00+0000
slug: zerotier-how-to-use
image: https://i.imgur.com/cZ876U1.png
---


## 提前准备下载客户端:
https://www.zerotier.com/download/
文档
https://docs.zerotier.com/start

## 第一次使用的教程:
1. 电脑安装客户端
2. 先往这个地址 https://my.zerotier.com/ ，注册并创建一个你的私有网络,获取网络的 id 
3. 比如我这个这个网络的 id 是:`<已屏蔽>`
4. 用客户端设备加入这个网络 `右键-Join new network`
5. 进入管理网站 https://my.zerotier.com/network ，授权你的新设备
![image](https://hackmd.io/_uploads/Bk5BW9v8Jg.png)
6. 接下来 你的设备就可以用右边的 Managed IP来直接访问了。


## 提示
如果你加入的设备都是windows，是默认无法ping通的，具体可参考文档 https://docs.zerotier.com/start/#test-connectivity

如果你想要开一个内网服务器，其他设备默认是无法访问的，需要windows防火墙中开启端口，下面示例开启 5678 端口
1. ![image](https://hackmd.io/_uploads/SyOIMqv8ye.png)
2. ![image](https://hackmd.io/_uploads/BJVdMcDUke.png)
3. ![image](https://hackmd.io/_uploads/BJXKM5DUJx.png)
4. 剩下的全都默认即可。


