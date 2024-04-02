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
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/pausegamewhithsuspend/&count_bg=%23F26E00&title_bg=%23000000)](https://hits.seeyoufarm.com)


我开发了一个gui工具来方便的暂停游戏
来这里下载: 
- [source code](https://github.com/cornradio/pausemygame)
- [release](https://github.com/cornradio/pausemygame/releases)

![1712043101178.png](https://img2.imgtp.com/2024/04/02/g2kpaJnW.png)

---

碰到了一个好玩的工具,可以用来暂停游戏（Windows）；这个工具原本的意义是用来暂停进程的，然后分析它的内存内容。
[pstools 下载](https://learn.microsoft.com/en-us/sysinternals/downloads/pssuspend)

> (暂停后完全不占用你任何的 CPU 资源，但是会占用内存和显存)


你可以用下面这个命令来查找程序名(或者用任务管理器-右键-属性)

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
比如把【鬼泣5】暂停了，cpu占用 = 0。
![alt text](https://img2.imgtp.com/2024/03/31/6sRJZ1UY.png)


---

