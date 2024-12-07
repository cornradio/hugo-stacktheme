---
title: pip package离线安装
date: 2024-12-07 00:00:00+0000
slug: pippackage_offline_install
image: https://i.imgur.com/XxHj2zJ.png
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/pippackage_offline_install/&count_bg=%23F26E00&title_bg=%23000000)](https://hits.seeyoufarm.com)
前提背景：我需要给一个无外网环境的服务器准备如下python环境和pip包：
首先，内网和公网机器都需要安装同版本的Python 以保证下载的包适合；
## 操作内容
从 python pip 下载package ，保存到指定文件夹。
将文件夹拷贝到内网服务器中。
通过命令安装package

## 确认pip

```
# 查看位置
python3.11 -m pip --version
```

## 下载所需的package

```
mkdir flask_deps;cd flask_deps;
python3.11 -m pip download Flask Flask-CORS
```

如果下载错了，可以通过一下命令删除重装
```
python3.11 -m pip uninstall flask Flask-CORS
```

## 内网机器安装命令

无网络机器安装
```
python3.11 -m pip install --no-index --find-links=/root/flask_deps Flask Flask-CORS
```

最后效果
```
[root@xxx filebox-api]# flask --version
Python 3.11.10
Flask 3.1.0
Werkzeug 3.1.3
```
