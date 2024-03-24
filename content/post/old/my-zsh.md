+++

title = "安装zsh和配置主题"
date = "2021-05-29"
author = "kasusa"
cover = ""
tags = ["ubuntu", "命令行"]
keywords = ["hugo2", ""]
description = "实际上是抄袭主题"
showFullContent = false

+++

> zsh 有很多实用功能，下面安装和配置ohmyzsh的教程：
# 安装zsh
```
sudo apt install zsh
```

# 提前安装所需的字体
```
sudo apt-get install fonts-powerline
```
[powerline-GitHub](https://github.com/powerline/fonts)

# 抄国光的作业
```
sh -c "$(curl -fsSL https://github.com/Cabbagec/termux-ohmyzsh/raw/master/install.sh)"  
```

# .zshrc配置
1. 打开配置文件
```
code .zshrc
```
2. 在.zshrc中加入下面这行( 去掉每行的 username@host )
```
export DEFAULT_USER="$(whoami)"
```

# ubuntu terminal 配置

1. profiles-colors 配置主题颜色，要让主题够好看，对比色都强烈
2. profiles-command 吧zsh代替默认shell，这样每次打开terminal默认就是zsh了！

## 常用快捷键：

 按键 | 功能  | 备注
---------|----------|---------
`ctrl` + `-` | 缩小terminal | 
`ctrl`+ `shift + `+`  | 放大terminal | 