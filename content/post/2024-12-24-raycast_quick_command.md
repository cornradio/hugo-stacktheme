---
title: raycast 快捷命令（macos）
date: 2024-12-24 00:00:00+0000
slug: raycast_quick_command
image: https://www.raycast.com/uploads/redesign/new-appicon.png##
---

## 创建第一个命令
1. opt+space 打开raycast
2. cmd + , 打开设置
3. 加号 - create script command
![](https://i.imgur.com/CSjnSDI.png)

4. 会创建一个 xxx.sh 到 user/document 文件夹
如 dat.sh

```
#!/bin/bash

# Required parameters:
# @raycast.schemaVersion 1
# @raycast.title dat
# @raycast.mode compact

# Optional parameters:
# @raycast.icon ⌚

date +"%Y-%m-%d %H:%M:%S %A"|pbcopy;echo time copyed
```

所以其实想要创建新的命令，可以直接复制这个文件，然后创建一个新的！修改文件名字、图标、命令内容即可。
不过鉴于不通版本的 raycast 可能采用不同的格式，我建议还是第一个模板通过 raycast 的 加号功能创建

## 执行命令

直接命令行输入即可在raycast中找到&执行
![](https://i.imgur.com/21t78GI.png)

## 修改命令
1. raycast中找到命令
2. cmd+K展开菜单
3. 选择 show in finder
在finder中打开并修改命令内容
![](https://i.imgur.com/vJ98Puj.png)
