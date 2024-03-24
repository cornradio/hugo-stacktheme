+++
title = "如何避免timemachine占用宝贵的mac磁盘空间"
description = ""
date = 2023-02-28T16:47:50+08:00
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

因为我买的MacBook只有512G的容量，所以我一直对容量使用比较在意，今天打开磁盘工具，发现我的MacBook的磁盘空间已经不足了。

![](https://i.imgur.com/vqpRmHX.png)

我一直使用 OmniDiskSweeper 来清理空间，他能直接显示你所有文件夹占用的空间，一层一层的往下看，并手动删除不需要的文件是我的清理方式 （比用清理工具比如CleanMyMac要好用多了）。

但是今天在清理之后发现，mac的磁盘空间还是不足，我感到非常奇怪。。。因为系统的磁盘管理工具和 OmniDiskSweeper 的磁盘空间使用数据对不上，差了几百G，经过一些搜索发现是因为：TimeMachine（时间机器）。

## 时间机器

时间机器除了在插上硬盘的时候备份到外置硬盘，还会平常偷偷摸摸的自动备份，在Mac内置存储空间里存放快照，并且他会在空间不足时自动删除最旧的快照。

其实合理的使用时间机器，不会占用太多的空间（因为他是增量保存，仅记录修改，不是复制整个文件），但是如果你使用了虚拟机软件，你在虚拟机里面修改了内容之后，整个虚拟机映像都会被重新备份一遍，，这是非常不合理的。

## 如何避免

把虚拟机文件之类的排除time machine 备份。至于虚拟机备份的话，PD本身就有照功能，vmware之类的也有类似的功能提供，不需要借助 timemachine。

![](https://i.imgur.com/sQHzg8x.png)

## 如何删除正在占用磁盘空间的快照
我们需要使用时间机器的命令行工具，打开终端，输入以下命令：

推荐用vscode之类的可以多光标编辑的软件，这样可以一次性写好多条命令！

```bash
tmutil listlocalsnapshots / 
```

Snapshots for disk /:
com.apple.TimeMachine.2023-02-11-102036.local
com.apple.TimeMachine.2023-02-28-092630.local
com.apple.TimeMachine.2023-02-28-102633.local
com.apple.TimeMachine.2023-02-28-143433.local

```bash
sudo tmutil deletelocalsnapshots 2023-02-11-102036
sudo tmutil deletelocalsnapshots 2023-02-28-092630
sudo tmutil deletelocalsnapshots 2023-02-28-102633
sudo tmutil deletelocalsnapshots 2023-02-28-143433
```

Deleted local snapshot '2023-02-11-102036'
Deleted local snapshot '2023-02-28-092630'
Deleted local snapshot '2023-02-28-102633'
Deleted local snapshot '2023-02-28-143433'


![删除之后](https://i.imgur.com/nfVWYE9.png)

## 参考
https://appleinsider.com/articles/21/06/26/how-to-delete-time-machine-local-snapshots-in-macos