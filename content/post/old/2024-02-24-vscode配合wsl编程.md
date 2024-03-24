+++
title = "vscode配合wsl编程"
description = ""
date = 2024-02-24T16:34:43+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "network security"
]
series = []
image = "vscode.jpg"

+++

使用wsl，用windows环境GUI + linux 高效地编程。
<!--more-->

https://code.visualstudio.com/docs/remote/wsl
用wsl和windows vscode 进行开发 上面是官方教程

准备：
1. 安装wsl
2. 安装vscode 插件 ： Remote Development

使用(多种方式）： 
 1. 在wsl ubuntu 中输入 `code .`
 2. 在 code中打开 `F1`  - WSL: xxx distro ... 
 3. 在windows用命令行启动code ， 附带下列参数 

```
code --remote wsl+Ubuntu /root/codes
```
