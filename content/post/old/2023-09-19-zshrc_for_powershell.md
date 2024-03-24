+++
title = "powershell 设置别名 alias"
description = ""
date = 2023-09-19T09:32:55+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "pwsh"
]
series = []
images = []
+++

使用 zsh 之后，回到windows，我很怀念alias功能。 以及 zshrc 配置文件。

但是 powershell 可以实现类似的功能：[参考](https://blog.csdn.net/lei_qi/article/details/106592404)

---

1. 打开管理员 powershell  ， 执行允许ps1脚本的命令：

```
Set-ExecutionPolicy RemoteSigned
```

2.  编辑配置文件（可以用任何自己喜欢的编辑器）

```pwsh
code $PROFILE
```

```powershell
# 例如：
# 快速移动到 hugo 工作目录：

function hg { Set-Location -Path 'C:\Users\kasus\hugo-win' }

# 执行多行命令

function xxx { Set-Location -Path 'C:\github\xxx' ; git pull }
```