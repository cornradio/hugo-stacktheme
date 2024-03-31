---
title: 用 suspend 工具暂停游戏（Windows） # 标题
slug: pausegamewhithsuspend # url(注释掉 和标题相同)
image: pausegame.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2024-03-31 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

tags: # 只能在侧面看到的标签,会显示在文章的底部
    - gaming
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

碰到了一个好玩的工具,可以用来暂停游戏（Windows）；这个工具原本的意义是用来暂停进程的，然后分析它的内存内容。
[pstools 下载](https://learn.microsoft.com/en-us/sysinternals/downloads/pssuspend)
> (真正的暂停--完全不占用你任何的 CPU 和 GPU 的资源)


你可以用下面这个命令来查找程序名(或者用任务管理器)

```
tasklist | findstr Devil
```

suspend 会把程序放到内存里。需要准确的程序名。（或者pid）
这里用  [quicker](https://getquicker.net/Download)的“运行选中文字”功能非常合适。

```
# 暂停程序DMC5
PsSuspend DevilMayCry5.exe
# 恢复程序DMC5
PsSuspend -r DevilMayCry5.exe 
```


---
比如下面的例子把【鬼泣5】暂停了，可以看到它除了占用了内存，其他的都是0。
![alt text](https://img2.imgtp.com/2024/03/31/6sRJZ1UY.png)

这里需要注意不要暂停一些重要的进程，比如 explorer.exe，否则你的桌面就会卡住鼠标也卡住了。

也不要对线上在线多人游戏进行这种操作，因为这样会导致你被踢出游戏，甚至有封号的风险。
