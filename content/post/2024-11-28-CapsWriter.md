---
title: CapsWriter-离线的大模型语音输入神器
date: 2024-11-28 00:00:00+0000
slug: CapsWriter
image: https://i.imgur.com/OXr6OPC.png
---

CapsWriter 是一个用 Python 编写的 ， 使用了大模型的 ， 本地快速语音输入工具。  
主要操作就是，按住大写锁定键，按住的时候说话，松手的时候就已经变成字了！ 

去这个项目的[github主页](https://github.com/HaujetZhao/CapsWriter-Offline)点星星、寻找更多详情和报错解答
## 下载
1. 在这个网站下载程序和模型 https://github.com/HaujetZhao/CapsWriter-Offline/releases/tag/v1.0

```
CapsWriter-Offline-Windows-64bit.zip
models.zip
```

2. 解压程序和模型，并且把模型放到程序的`models`目录下
3. 同时开启 `start client` 和`start server` exe 程序 PS: 我写了一个一键启动的 bat 脚本，可以在下面参考
4. 如果 start server 点 exe 需要你提供防火墙权限的话，请允许
5. 长按 caps lock 按钮，即可说话，松开后语音转成文字

## 设置
我建议把这个标点符号给设置成 `false` ， 因为这个标点符号它加载模型很慢

![](https://i.imgur.com/LInQWFj.png)


`config.py`
```
format_punc = False  # 输出时是否启用标点符号引擎
```

## 附件
![](https://i.imgur.com/04h9uBS.png)

保存下面的代码为`Capswriterrun.bat` 文件，可以快速启动。
```bat
@echo off
start /min "" cmd /c "start_client.exe"
start /min "" cmd /c "start_server.exe"
```

这个代码是给 win11 以及以上用的，使用到了Windows terminal，它可以让两个程序开在同一个Windows terminal中的不同tab上
```
@echo off
wt -w 0 nt -p "Command Prompt" -d . cmd /k "start_server.exe"
wt -w 0 nt -p "Command Prompt" -d . cmd /k "start_client.exe"
```

## 特性
1. 完全离线、无限时长、低延迟、高准确率、中英混输、自动阿拉伯数字、自动调整中英间隔
2. 热词功能：可以在 `hot-en.txt hot-zh.txt hot-rule.txt` 中添加三种热词，客户端动态载入
3. 日记功能：默认每次录音识别后，识别结果记录在 `年份/月份/日期.md` ，录音文件保存在 `年份/月份/assets`
4. 关键词日记：识别结果若以关键词开头，会被记录在 `年份/月份/关键词-日期.md`，关键词在 `keywords.txt` 中定义
5. 转录功能：将音视频文件拖动到客户端打开，即可转录生成 srt 字幕
6. 服务端、客户端分离，可以服务多台客户端
7. 编辑 `config.py` ，可以配置服务端地址、快捷键、录音开关……

我是不太理解他为什么要把服务端分离出来，这玩意儿是主打本地的，如果还要再弄成服务器，那不就成远程的了吗...


