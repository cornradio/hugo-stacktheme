---
title: yum离线安装软件包
date: 2024-12-07 00:00:00+0000
slug: yum_offline_install
image: https://i.imgur.com/m0nzEwx.png
---

情况背景：
你有一个 serverA 无法访问网络，需要通过离线的方式手工上传和安装 ngxin 等程序。
你有一个 serverB 可以访问网络，用来给serverA 提供安装文件。

下面的例子可以自动通过serverB从公网下载 rpm 安装包（包括依赖），下载后通过 scp 手工上传到 serverA 然后执行相关安装命令即可。
 
## 下载
```
yum_packs="pip python3.11 nginx"
sudo yum install --downloadonly --skip-broken --downloaddir=/root/myyum ${yum_packs}
## 如果要下载已经存在的包
sudo yum reinstall --downloadonly --skip-broken --downloaddir=/root/myyum ${yum_packs}
```
下载安装包（包括依赖）到`/root/myyum`文件夹
## 安装
可以使用下面两种方式进行安装
```
cd ./myyum
rpm -ivh *.rpm

# 或者yum
yum localinstall -y --disablerepo='*' /root/myyum/*.rpm

```

## ps：使用 nginx
因为这里正好离线安装了nginx ， 下面是nginx后续配置的示例

```
systemctl start nginx
```
启动nginx
```
systemctl start nginx
systemctl status nginx
```

```
netstat -tulpn | grep :80
kill -9 <占用id>
```

nginx 位置：

```
/usr/share/nginx/html
```
