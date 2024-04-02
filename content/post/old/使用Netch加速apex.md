+++
title = "使用Netch加速apex"
description = ""
date = 2022-05-28T14:36:11+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "game","加速器","windwos","Netch"
]
series = []
images = ["https://tvax3.sinaimg.cn/large/006rgJELly1h2o5hxdsk2j305303ajrd.jpg"]

+++

> 前段时间我没有续费我的uu加速器了，因为这个老鬼东西实在是价格太贵，并且也不是多好用。

> 上次我为了和同学一些玩游戏又在网上买了个uu加速器（登录器），反正就类似卡uu加速器的bug加速游戏，但是uu很明显不想让他一直薅羊毛，所以我这边也加速不了了，找了店家，店家好像一个脑瘫问题不解决就阿巴阿巴的。

> 一直都听说能用什么软件让节点给游戏加速，我今天就仔细研究了下，hey你别说人家这个开源的Netch真的做的不错，我加速了Apex并且玩起来和用uu加速没啥区别！
>
> 垃圾uu要的太黑！黑心商人！

# 参考链接

下载Netch：[https://github.com/NetchX/Netch](https://github.com/NetchX/Netch)

[比SStap更优秀的Netch怎么用 - YouTube](https://www.youtube.com/watch?v=csUjrHjmIqA)

[Netch使用指南(190627) | 冰灵的博客 | BingLing's Blog (binglinggroup.github.io)](https://binglinggroup.github.io/archives/Netch_guide.html)

# 它与v2rayN、Clash的不同

> 我希望你可以先看一下这里，你如果了解了它的原理，后边就很明白它到底是为什么这样操作了，对于折腾来说，可以减少你浪费的时间

一般我们用v2rayN、Clash来对浏览器、系统全局进行代理，达到访问Google的目的

但是即使开了全局，他们也不能连接上 PUBG 或者 APEX 这些游戏

至于原因？

 因为他们的“全局”只是修改了windows这里的设置而已，很多游戏之类的程序并不会检查和使用系统的代理来建立网络链接。

![image](https://image.baidu.com/search/down?url=https://tva1.sinaimg.cn/large/006rgJELgy1h2o4ag3dmwj30ts0gmwgg.jpg)

那么从原理上来说的话这个Netch又有什么不同呢？

Netch是对**进程**进行代理

它是发现你的电脑开启了某个名称的进程后，就会从外部给它加上一个代理，并不需要程序本身兼容

就能达到给一些不支持代理的程序进行加速的效果。

![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/006rgJELgy1h2o4xdulj6j30cp0bo40m.jpg)

# Netch的使用

## 添加订阅

因为我一般都是使用的订阅，所以我就不讲单条节点如何导入了。

这里的界面样式非常像V2rayN，第一个按钮可以添加删除订阅（支持同时有好几个），第二个是更新订阅列表。加入成功之后你就可以在服务器下拉列表中选择自己的服务器节点了。

![image](https://image.baidu.com/search/down?url=https://tva1.sinaimg.cn/large/006rgJELly1h2o4i6fb6mj30al03sdgo.jpg)

## 主界面功能简要介绍

- 服务器

  - 选择你的节点用的，右边四个按钮分别是 编辑（查看）、删除、测速、复制（复制之后可以贴到别的软件里）

- 模式

  - 模式可以理解成，预设的加速进程列表，预设提供的还是挺多的有steam、steam游戏、git、GTAv、Unity hub等，包括了很多工作、学习软件
  - 模式是按照A-Z a-z 的顺序排序的，到时候你自己建立了模式需要起名字，然后就能在这里找到了。

- 配置名

  - 老版本没有这个，这个配置名就是给你当前选择好的服务器、模式的组合起名字，然后可以保存到下面的快速按钮里，下次开软件，点击按钮直接启动（加速）

  

![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/006rgJELly1h2o4gt3d7hj30qp08u78x.jpg)

## 新建一个APEX模式

模式可以理解成，预设的加速进程列表，进程是靠进程名称来识别的，所以即使他不知道程序本体的具体路径，只要知道名字就ok了。

1. 去`steam`里面找到游戏的目录，然后复制一下路径
2. 来到`Netch`，模式-创建进程模式，然后再打开的窗体中按“扫描“
3. 扫描会让你选择一个文件夹，我们选择游戏的整个目录，可以参考我的截图
4. 然后你会发现出现了一堆`xxx.exe`,他们就是程序再你制定好的目录下面找的程序列表，在程序启动之后，Netch可以根据这些东西找到相应的”进程“然后加速他们。
5. 起名字保存（我起名为Apex-test）
6. 保存之后，在模式的下拉框里面，你就可以找到自己新建的模式了！

![image](https://image.baidu.com/search/down?url=https://tvax2.sinaimg.cn/large/006rgJELgy1h2o4ubg52kj30dj07t41a.jpg)

![image](https://image.baidu.com/search/down?url=https://tvax4.sinaimg.cn/large/006rgJELgy1h2o4skj941j30bo042ab1.jpg)

![image](https://image.baidu.com/search/down?url=https://tva3.sinaimg.cn/large/006rgJELgy1h2o4tqih87j30cp0bogmf.jpg)

![image](https://image.baidu.com/search/down?url=https://tvax3.sinaimg.cn/large/006rgJELgy1h2o4wk8d3dj30nq0bjtdd.jpg)

![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/006rgJELgy1h2o4xdulj6j30cp0bo40m.jpg)

![image](https://image.baidu.com/search/down?url=https://tvax1.sinaimg.cn/large/006rgJELgy1h2o50cnxyrj30kc08wdjb.jpg)

## 加速、保存快速配置

这里我选择了建立了两个快速配置，你可以自己随便建立自己的快速配置（本质上就是模式和服务器的组合）

![image](https://image.baidu.com/search/down?url=https://tva4.sinaimg.cn/large/006rgJELgy1h2o51nhl4lj30kc08wq5a.jpg)

## 同时加速steam和Apex（高级）

我这边steam好友总是不好使，还有steam社区也打不开，在等待过程中看看社区好玩的图和吐槽也是乐趣呀。

那么，如何建立这种模式呢？

1. 找到它预设的steam模式，点击右边的编辑按钮，然后把他的规则都复制出来（其实就是一个大textbox，可以打字的还能选择退格之类的）
2. 打开你的模式（Apex-test），然后把steam的模式规则都贴后面
3. 保存你的修改后的模式（可以重命名再保存）

![image](https://image.baidu.com/search/down?url=https://tvax3.sinaimg.cn/large/006rgJELly1h2o57l9qyhj30cp0boac5.jpg)

![image](https://image.baidu.com/search/down?url=https://tvax1.sinaimg.cn/large/006rgJELly1h2o5a091g8j30cp0boq60.jpg)

# 结语

希望这个文章能帮到其他折腾的人，毕竟uu蛮贵的，而每个月都买的节点如果能用在游戏加速上面那当然很开心呀！谁不想省点钱呢？

不过我仍然不知道怎么让Netch给主机加速，后面用得上再想吧…

有啥问题请再评论区告诉我，错别字就算了…
