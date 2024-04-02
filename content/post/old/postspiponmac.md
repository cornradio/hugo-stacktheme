+++
title = "pip on mac"
description = ""
date = 2022-06-25T22:03:07+08:00
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

mac自带了python，但是竟然不带pip，这篇文章将会教你如何在mac上面安装pip包管理器。

> 这个文章是在mac上面写的哦，因为环境很难搞所以也蛮折腾的，不过这也是乐趣～
> 本文章用mac（m1）编写，环境可能与intel版mac不同，请提前注意这一点。


# pip安装脚本获取

https://bootstrap.pypa.io/pip
使用浏览器访问这个地址，应该有一个 get-pip.py 脚本，由于我不熟悉crul之类的工具，我选择手动复制下来。

cmd + A ， cmd + C ， 复制全文，存到一边一会儿要用。
![image](https://image.baidu.com/search/down?url=https://tvax4.sinaimg.cn/large/0083vuQJly1h3kunji5jej313w0t8e0o.jpg)

<!-- 然后来到terminal中，首先输入`python3`，开启python交互式界面，通过下列命令查询到python的安装位置。

```py
>>> import os
>>> os.path
```

![image](https://image.baidu.com/search/down?url=https://tva3.sinaimg.cn/large/0083vuQJly1h3kurdqpqxj31ki14akjl.jpg)

然后进入安装python的目录（`/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8`） -->

# pip脚本的安装

使用vim新建一个pip.py脚本文件，内容就是上面网页中的内容，你可以选择任何位置，不知道的话就放到家目录吧（因为很好找）,然后，使用python3运行这个脚本文件

> 图片右上角是我新创建的文件 pip.py，他的内容是从网页复制的


![image](https://image.baidu.com/search/down?url=https://tva3.sinaimg.cn/large/0083vuQJly1h3kuzs0ljoj312i0gfwzi.jpg)

# 配置环境变量
脚本用黄色高量字体提醒了我们：
 > WARNING: The scripts pip, pip3, pip3.10 and pip3.8 are installed in '/Users/kasusa/Library/Python/3.8/bin' which is not on PATH.

pip安装的位置不在path中，所以我们要手动的加个环境变量。

首先打开用户根目录，然后新建个`.zshrc`文件，zsh是mac的terminal的默认shell，`.zshrc`是zsh的配置文件，但是默认情况并不存在！

新建之后在添加这一行即可:

```
export PATH=~/bin:/Users/kasusa/Library/Python/3.8/bin:$PATH
```

![image](https://image.baidu.com/search/down?url=https://tva1.sinaimg.cn/large/0083vuQJly1h3kv8fwyn9j31yw0luwkz.jpg)

这个例子中包含了三个path(使用冒号分割）：
- ~/bin
- ~/Library/Python/3.8/bin
- $PATH

他们分别是：
- 我的自设path目录
- python pip目录
- 从系统继承的path

> 注：`~`是`/Users/kasusa`的缩写

# 使配置生效
有两种方式使配置生效：
1. 重新开启一个terminal
2. 执行命令

```
source ~/.zshrc
```

# 成功结果展示
![image](https://image.baidu.com/search/down?url=https://tva4.sinaimg.cn/large/0083vuQJly1h3kvhhp942j30zl0sg1kx.jpg)