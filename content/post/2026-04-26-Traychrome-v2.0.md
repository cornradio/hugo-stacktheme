---
title: 托盘浏览器 Traychrome-v3.0  # 标题
slug: Traychrome-v2.0 # url(注释掉 和标题相同)
image: https://wcp.cornradio.org/images/traychrome/image-6.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2026-11-06 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2FTraychrome-v2.0&label=&icon=check-all&color=%23198754)


<https://github.com/cornradio/tray-chrome>


Traychrome-v3.0 带来了许多令人兴奋的新功能和改进：


- 标签页模式
- 本地主页
- 页面搜索功能
- 深色模式设置和设置快捷键。
- 历史记录
- 支持大量书签的书签管理
- App组管理 功能（支持设置定义好的一组托盘菜单以及自定义icon，并且一键打开所有的托盘软件）
- 极简模式下的 alt 拖拽和窗口大小调整
- 可编辑底部栏
- 内置脚本支持（油猴脚本）


本质上，TrayChrome可以把任何的网页变成一个小软件，例如我自己开发的rbtodo、rbwiki、tricksvideos等。
另外比如，像一些网页软件，例如：ChatGPT、Notion、icloud、appleMusic.

上面这些我自己开发的网页软件，我并没有过多的在博客介绍。
但是你可以直接在我的GitHub上搜索到，你可以自行部署并尝试，它们是非常实用的软件。

Traychrome 这个软件修改有一个非常大的难点，就是我需要在增加这些功能的同时，保证它主界面的简洁，这很难。


标签页模式
![alt text](https://wcp.cornradio.org/images/traychrome/image-9.png)

本地主页
![alt text](https://wcp.cornradio.org/images/traychrome/image-8.png)

极简模式
![alt text](https://wcp.cornradio.org/images/traychrome/image-10.png)

App组管理
![alt text](https://wcp.cornradio.org/images/traychrome/image-7.png)




---

这个版本的托盘浏览器 Traychrome-v2.0 带来了许多令人兴奋的新功能和改进：

- 增加了代理支持 ！！！
- 优化了书签编辑功能

** 代理支持**

下图中展示了代理设置的功能界面：
开启代理后需要重启一下程序实例才可以使代理生效。

![alt text](https://wcp.cornradio.org/images/traychrome/image-1.png)

这是代理开启前及开启后的图片对比：

![alt text](https://wcp.cornradio.org/images/traychrome/image-4.png)

目前存在一个已知问题就是如果开了代理之后你再把代理关掉再创建一个新的实例它就会不停的报错：   
WebView2初始化失败: 组或资源的状态不是执行请求操作的正确状态。(0x8007139F)

 优化书签编辑功能
1. 现在书签编辑界面更加简洁，显示更加compact
2. 星星按钮增加了快捷进入书签管理器的菜单

![alt text](https://wcp.cornradio.org/images/traychrome/image-5.png)


