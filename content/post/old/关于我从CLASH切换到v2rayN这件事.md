+++
title = "关于我从CLASH切换到v2rayN这件事"
description = ""
date = 2022-03-10T18:40:24+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "代理"
]
series = []
images = []

+++

我从clash切换到使用v2rayN了，

这件事情是因为steam，但是也因为clash是一个坏软件。

# 起因

我昨天晚上登录steam，借用朋友的账号要使用家庭共享来共享他的游戏“老头环”。

但是我登录非常有问题，总是发生登录失败或者类似的事情

在之前steam也是有问题的，有的时候他就会蹦出来“好友无法连接”之类的鬼东西。还会把我从游戏中弹出来。

归根结底，这是steam的问题。也是代理软件的问题，代理软件虽然想要“智能”但是我只能说它太他吗傻逼了，让我的网易云走国外代理，让我的steam也走代理，我无法体验到喷薄如蒸汽般的下载速度，我还要付出好多好多的流量钱！

我决定换一个软件，clash肯定是有问题！

> steam一直在用我的流量下载东西

![steam一直在使用我的代理进行网络通信](https://image.baidu.com/search/down?url=https://tvax2.sinaimg.cn/large/006rgJELly1h05265xqy9j30rw08fwkt.jpg)

# 代理的原理

![62301E4785F21D726F53429C72B1263F](https://image.baidu.com/search/down?url=https://tva4.sinaimg.cn/large/006rgJELly1h04zpqakv7j31d30l4te7.jpg)

一般情况下，翻墙就是这样，借助一个没有被强。

![3ABEDD24ECE7CD73DE4FDDFEC2E25A23](https://image.baidu.com/search/down?url=https://tvax3.sinaimg.cn/large/006rgJELly1h04zydp6srj31tm0qg10m.jpg)

实际情况更像是这样，两个庞大的网络，里面都有好多的应用，而且他们基本上“不互通”

你就是左边小小的电脑，连接到了右边蓝色的服务器上，然后可以愉快地上网！

![16E8BC6CD7F2D4E4822949B675FA6F11](https://image.baidu.com/search/down?url=https://tvax2.sinaimg.cn/large/006rgJELly1h050ak4f3ij319g0mxdnj.jpg)

但是你的代理软件也不是很智能，他手里拿着一个列表（Geoip.dat），但是他实际上也不是很清楚那些流量该怎么走，有时候就会弄错，对我来说经常有steam下载用代理、网易云听歌被代理、一些外网的名气小的网站却不被代理的情况发生。

对我来说我经常需要代理的地方有

- 谷歌搜索
- github下载
- youtube看视频
- soundcloud听音乐
- Pornhub 看视频……

但是soundcloud好像并不是很出名，在很多机场的配置文件都没有配置，结果代理软件Clash就选择直连，后果就是我听不了歌。

> clash是由节点提供商可以同时提供一份规则文件，根据规则文件对流量进行代理

# 为什么用v2rayN

其实我是一个clash老用户了，很喜欢他的外观；但是他的log和调试功能让人完全看不懂，如果是某些网站被错误代理，我也无法发现，只能感受到满速的链接和无尽的等待。

但是v2rayN可以显示log他会会在后面用**[proxy]、[direct]**来表示是否有把这个链接或者数据包通过代理发送。

配合上域名，很轻松就能看出来这个ip是不是转发的了。

![image](https://image.baidu.com/search/down?url=https://tva1.sinaimg.cn/large/006rgJELly1h050p54ylkj30o709a7bo.jpg)

对我来说，调试起来就很方便了

而且使用规则也方便多了（表示一致没弄明白过规则集要怎么用）。

## 系统代理

对于代理软件来说，默认是不会开启系统代理的。

开启系统代理之后，对于系统中产生的所有流量都要过滤一遍，也就是每个链接都要拿过去对着list算一遍在不在里面

如果开启了系统代理，我的steam就会被代理，所有很不喜欢

好处是github desktop也可以被代理了……

## 路由规则设置

这个东西我一致没有仔细研究过，说实话对我使用带来了很多不便，现在我下定决心研究一下并且把结果都写出来。

我们可以看到路由规则有三种，

| 别名     | 意义                                                       |
| -------- | ---------------------------------------------------------- |
| 全局     | 所有流量都代理                                             |
|          | 适合完全不用国内网站、服务的人                             |
| 绕过大陆 | 只有名单内的国内ip、域名直连，如果有不在list里面的就代理， |
|          | 适合上很多国外网站，但是国内只上很出名的网站的人           |
| 黑名单   | 仅代理list中的外国网站、被封的网站                         |
|          | 适合上很多国内网站，国外小网站基本不去的人                 |

![image](https://image.baidu.com/search/down?url=https://tvax4.sinaimg.cn/large/006rgJELly1h0524a18ldj30u30lm130.jpg)

没有最理想的方式，只有不断切换模式才能符合各种使用场景。

> 未完待续…… 后面还会讲 v2rayN使用技巧 、 SocksCap64的使用、NoLsp等

