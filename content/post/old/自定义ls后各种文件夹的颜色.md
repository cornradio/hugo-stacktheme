+++
title = "自定义ls后各种文件夹的颜色"
description = ""
date = 2022-05-22T16:14:26+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "linux"
]
series = []
images = ["https://tva2.sinaimg.cn/large/006rgJELgy1h2h9h5nahuj30qt0ewgwe.jpg"]

+++

今天用WLS打开windows目录，一片亮瞎眼的绿色，再加上这个复古特效，真的字都看不清了：

![image](https://image.baidu.com/search/down?url=https://tva3.sinaimg.cn/large/006rgJELgy1h2h94lpkckj30it047q5g.jpg)

在网上搜了一圈修改办法，终于找到一个有用的文章：[在WSL环境下修改文件夹的颜色](https://sspai.com/post/39499)

# 操作步骤

回到主目录然后导出（新建）一个.dircolors文件

```
cd ~/
dircolors -p > .dircolors
```

使用vim打开这个新文件（vim可以看见设置的颜色效果，搜索`OTHER_WRITABLE`

```
vim ~/.dircolors
```

把颜色修改成你想要的，有前景色、背景色、字体三种东西可以修改，具体的样式数字
修改好了之后 :wq 保存退出

最后用 `source ~/.bashrc` 重加载一下bash配置文件即可完成修改了

![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/006rgJELgy1h2h9h5nahuj30qt0ewgwe.jpg)



# 颜色列表

> 这个颜色列表应该在很多程序中都用得到，比如各种输出，他们的颜色应该都是用的同一种映射

你可以修改成任何你要字体、前景色、背景色搭配，用`;`分开即可

例如 **加粗 黑色字 Cyan背景** = `01;30;46`

```bash
# 字体
00 　　　 //默认
01 　　 　//加粗
04 　 　　//下划线
05 　 　　//闪烁
07 　 　　//反显
08 　 　　//隐藏
# 文字颜色 
30 — Black   //黑色
31 — Red     //红色
32 — Green   //绿色
33 — Yellow  //黄色
34 — Blue    //蓝色
35 — Magenta //洋红色
36 — Cyan    //蓝绿色
37 — White   //白色
# 背景颜色 
40 — Black 
41 — Red 
42 — Green 
43 — Yellow 
44 — Blue 
45 — Magenta 
46 — Cyan 
47 – White
```

