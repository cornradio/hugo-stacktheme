+++
title = "ssh to parallels （kali）"
description = ""
date = 2022-08-06T10:00:00+08:00
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "Mac","kali"
]
series = []
images = []

+++

参考：

https://wpguru.co.uk/2014/02/how-to-ssh-into-a-virtual-machine-in-parallels-desktop/

## 使用ssh链接 parallels 虚拟机的 kali linux系统

本教程基于PD17，m1 MacBook。

首先你也直接在pd虚拟机中直接下载和安装kali，而不用自己下载镜像来安装。

![安装助手](https://i.imgur.com/122vaYp.png)

## 修改sshd配置

默认情况下kali的sshd配置是无法被ssh的，我们需要首先修改sshd配置然后重新加载。

````sh
sudo vim /etc/ssh/sshd_config
# 搜索以下关键词然后取消备注/改成yes
PermitRootLogin yes
PasswordAuthentication yes
````

修改后需要重启服务，加载刚更新配置：

```bash
/etc/init.d/ssh restart 
```

增加开机自启动ssh的一个服务：
```
sudo update-rc.d ssh enable
```

## 查看虚拟机的ip

```bash
ifconfig
```

![查看虚拟机的ip](https://i.imgur.com/aHsiG9S.png)

## 使用ssh工具链接虚拟机

```bash
ssh parallels@10.221.55.4
```

- parallels 是通过pd安装虚拟机自己创建的用户名，有root权限

接下来你就可以正常远程进入虚拟机了，这样可以使用macOS的cmd+v粘贴之类的快捷键。

![ssh工具链接虚拟机](https://i.imgur.com/bT52A7j.png)
