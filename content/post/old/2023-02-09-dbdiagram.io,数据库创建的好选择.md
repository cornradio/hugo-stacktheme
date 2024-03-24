+++
title = "Dbdiagram.io,数据库设计的好选择"
description = ""
date = 2023-02-09T16:01:23+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "database","free"
]
series = []
images = []
+++

说到数据库设计软件，之前上学的时候用过 powerdesigener 、 navicat设计数据库。

但是都是付费软件，今天找到了一个免费的数据库设计工具 [dbdiagram.io](https://dbdiagram.io)。
<!--more-->

首先，以防你看完了文章才发现自己不喜欢这个，先来看一下截图：

![](https://raw.githubusercontent.com/cornradio/imgs/main/20230209160353.png)

一般操作就是左边写语句，右边可以拖拽生成外键，设计好了之后可以生成各种数据库的 sql 语句，也可以PDF导出。


这里使用的语句叫做 `dbml` 语句,语法类似sql建表语句，具体语法参考[这个链接](https://www.dbml.org/home/?utm_source=dbdiagram)，这个语言是 `dbdiagram.io` 自己的，可能需要小小的学习一下。

> 我这里在 `vscode` 中安装了一个 `dbml` 插件，可以在 vscode 中写设计语句，通过 `copilot` （AI插件），我只要写好备注，就可以自动生成大段的语句。

关于外键的用法其实也非常的符合直觉：你只需要使用 `-` `>` 之类的富豪榜，就能轻松的表示一对一、一对多的关系。 

最后用 datagrip 导入生成的 sql 语句到 mysql，简直不要太爽！导出操作比我之前用过的那些软件方便得多！

![](https://raw.githubusercontent.com/cornradio/imgs/main/20230209161253.png)