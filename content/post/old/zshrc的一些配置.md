+++
title = "自定义终端标识符"
description = ""
date = 2022-09-15T23:03:01+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  "bash"
]
tags = [
  "个性化"
]
series = []
images = []

+++

# zshrc

zsh是macos目前默认的交互终端，如果要修改默认标识符有2中办法：

在～/.zshrc文件中加入行来设置：

你可以通过设置PS1这个变量，或者设置PROMPT（提示符）、RPROMPT（右侧提示符）来进行自定义。

# 可视化例子

苹果推荐：

```sh
export PS1="%10F%m%f:%11F%1~%f \$ "
```

![image](https://image.baidu.com/search/down?url=https://tva1.sinaimg.cn/large/0083vuQJgy1h67plzn0rqj30bi02saa4.jpg)

所以`%10Fxxx%f` 就是绿色的`xxx`，`%11Fxxx%f`就是黄色，其他的颜色我也没有实验所以不清楚，` \$` 就是输入$的意思（这个符号是转义符所以增加了 `\`)，`%m`代表主机名称，`%～`则是你相对于你的home的位置。

我喜欢用%B - %b、%T、%~这几个，非常干净简洁的组合。

| 转义变量 | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| %T       | 系统时间（时：分）                                           |
| %*       | 系统时间（时：分：秒）                                       |
| %D       | 系统日期（年-月-日）                                         |
| %n       | 你的用户名                                                   |
| %B - %b  | 开始到结束使用粗体打印                                       |
| %~       | 你目前的工作目录相对于～的相对路径（可能在某些zsh版本可能造成乱码） |
| %M       | 计算机的主机名                                               |

更完整详细的表格可以看这里，是zsh官方的：https://zsh.sourceforge.io/Doc/Release/Prompt-Expansion.html

简洁样式1:

```sh
export PS1="%T %B%~%b \$ "
```

![image](https://tvax3.sinaimg.cn/large/0083vuQJly1h67qc96kcoj30a403et8j.jpg)



自定义样式1:

```sh
#开启颜色
autoload -U colors && colors       
#配置提示符模式
PROMPT="%T %{$fg_bold[green]%}%1|%~ %{$reset_color%}\$ "        
#在行末显示
RPROMPT="[%{$fg[green]%}%?%{$reset_color%}]"
```

![image](https://image.baidu.com/search/down?url=https://tvax3.sinaimg.cn/large/0083vuQJly1h67qd8ra1kj30lc03mwee.jpg)

自定义样式中用到了不一样的颜色语法，更容易看懂（虽然超级乱），而且需要用到autoload，不顾你可以变得简单点，直接用上面学到的一行都配置在ps1里面。

不过总的来说效果很棒！

如果有意向高一些更自定义的可以看看这个文档，也许你会想开始用ohmyzsh，我是觉得那个有点花了…… >> [Zsh (简体中文) - ArchWiki (archlinux.org)](https://wiki.archlinux.org/title/Zsh_(简体中文)#.E5.BD.A9.E8.89.B2)
