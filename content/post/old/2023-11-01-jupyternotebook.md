+++
title = "Jupyter notebook"
description = ""
date = 2023-11-01T13:40:05+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  ""
]
series = []
images = []
+++

安装 Jupyter Notebook 可以通过以下步骤完成：

1. 确保你已经安装了 Python。
2. 使用 pip 安装 Jupyter Notebook。

```
pip3 install jupyter
```

如果提示没有pip3：
- 按下 Win + Pause/Break 键打开系统属性窗口，然后选择 "高级系统设置"
- 增加一条类似 `C:\Users\kasus\AppData\Local\Programs\Python\Python310\Scripts` 的条目 这个目录里面有pip3
- 确保重启

安装完成后，可以运行以下命令来启动 Jupyter Notebook：

```
jupyter notebook
```

运行该命令后，Jupyter Notebook 服务器将在默认浏览器中打开，并显示 Jupyter Notebook 的界面。你可以在其中创建和运行 Python 代码的笔记本。

## 操作
- 运行当前单元格并将焦点移至下一个单元格：Shift + Enter 🌟
- 运行当前单元格并在下方插入新单元格：Alt + Enter 🌟
- 运行当前单元格并保持焦点在当前单元格：Ctrl + Enter 🌟
- 把单元格移动到上方/下方：  ctrl shift ⬆️ 

- 将选定的单元格标记为 "Markdown" 模式：Esc + M 🌟
- 将选定的单元格标记为 "Code" 模式：Esc + Y
- 在选定的单元格上方插入新的单元格：Esc + A
- 在选定的单元格下方插入新的单元格：Esc + B
- 删除选定的单元格：Esc + D + D (按两次 D)
- 将选定的单元格复制到上方：Esc + Shift + P
- 将选定的单元格复制到下方：Esc + Shift + N
- 合并选定的单元格：Shift + M 🌟
- 切换选定单元格的折叠状态：Shift + O (按 O)
- 将单元格切换为编辑模式：Enter
- 退出单元格的编辑模式：Esc

## 插件

也推荐使用vscode插件来使用 jupyter

https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter
