+++
title = "Permission Denied (publickey,gssapi-keyex,gssapi-with-mic) 解决办法"
description = ""
date = 2022-02-14T09:56:15+08:00
featured = false
draft = false
comment = true
toc = true
reward = true
categories = [
  
]
tags = [
  "centos","ssh"
]
series = []
images = []

+++

今天ssh登录阿里云远程的centos，出现了

```
Permission denied (publickey,gssapi-keyex,gssapi-with-mic)
```

尝试使用生成的key（pem文件）没有成功。

```
ssh -i myvmubuntu.pem root@123.56.18.36
```

提示如下错误：

```
Permission denied (publickey,gssapi-keyex,gssapi-with-mic)
```

# 解决方案

修改这文件:

```
sudo vim /etc/ssh/sshd_config
```

搜索如下两项：并把后面修改成如下所示 

```
PasswordAuthentication yes
……
ChallengeResponseAuthentication no
```

重启sshd：

```
sudo systemctl restart sshd
```

