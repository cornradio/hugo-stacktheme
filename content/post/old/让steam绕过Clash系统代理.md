+++
title = "steam如何绕过clash的全局代理"
description = ""
date = 2021-11-30T13:11:11+08:00
featured = false
draft = false
comment = true
toc = true
reward = true
categories = [
""
]
tags = [
  "clash","steam"
]
series = []
images = []

+++
我想要默认开启电脑的clash全局代理。但是要求steam这个东东登录和下载（尤其是游戏下载）不要走代理。下载太耗费流量了，还不能跑满网速。

下载游戏的同时我还会上网。如果特意为了steam把clash关了我就不能上外网了。

最后在github的一个issue里面看到了这个：
[0.16.2 版，Steam 商店、社区无法加载 · Issue #2035 · Fndroid/clash_for_windows_pkg (github.com)](https://github.com/Fndroid/clash_for_windows_pkg/issues/2035)

```ini
bypass:
# Steam中国大陆地区游戏下载
  - "steampipe.steamcontent.tnkjmec.com" #华为云
  - "st.dl.eccdnx.com" #白山云
  - "st.dl.bscstorage.net"
  - "st.dl.pinyuncloud.com"
  - "dl.steam.clngaa.com" #金山云
  - "cdn.mileweb.cs.steampowered.com.8686c.com" #网宿云
  - "cdn-ws.content.steamchina.com"
  - "cdn-qc.content.steamchina.com" #腾讯云
  - "cdn-ali.content.steamchina.com" #阿里云
# Steam非中国大陆地区游戏下载/社区实况直播
  - "*.steamcontent.com"
# Steam国际创意工坊下载CDN
  - "steamusercontent-a.akamaihd.net" #CDN-Akamai
# Origin游戏下载
  - "ssl-lvlt.cdn.ea.com" #CDN-Level3
  - "origin-a.akamaihd.net" #CDN-Akamai
# Battle.net战网中国大陆地区游戏下载
  - "client05.pdl.wow.battlenet.com.cn" #华为云
  - "client02.pdl.wow.battlenet.com.cn" #网宿云
# Battle.net战网非中国大陆地区游戏下载
  - "level3.blizzard.com" #CDN-Level3
  - "blzddist1-a.akamaihd.net" #CDN-Akamai
  - "blzddistkr1-a.akamaihd.net"
  - "kr.cdn.blizzard.com" #CDN-Blizzard
  - "us.cdn.blizzard.com"
  - "eu.cdn.blizzard.com"
# Epic Games中国大陆地区游戏下载
  - "epicgames-download1-1251447533.file.myqcloud.com"
# Epic Games非中国大陆地区游戏下载
  - "epicgames-download1.akamaized.net" #CDN-Akamai
  - "download.epicgames.com" #CDN-Amazon
  - "download2.epicgames.com"
  - "download3.epicgames.com"
  - "download4.epicgames.com"
# Rockstar Launcher客户端更新/游戏更新/游戏下载
  - "gamedownloads-rockstargames-com.akamaized.net"
# GOG中国大陆游戏下载/客户端更新
  - "gog.qtlglb.com"
# GOG非中国大陆游戏下载/客户端更新
  - "cdn.gog.com"
  - "galaxy-client-update.gog.com"
  - localhost
  - 127.*
  - 10.*
  - 172.16.*
  - 172.17.*
  - 172.18.*
  - 172.19.*
  - 172.20.*
  - 172.21.*
  - 172.22.*
  - 172.23.*
  - 172.24.*
  - 172.25.*
  - 172.26.*
  - 172.27.*
  - 172.28.*
  - 172.29.*
  - 172.30.*
  - 172.31.*
  - 192.168.*
  - <local>

```

# 使用方法
原理：在bypass列表中的域名、ip会直接跳过
- 域名需要用英文双引号包起来
- ip可以直接写
- 可以使用【星号】作为通配符
打开clash的设置，找到bypass，按照需要粘贴并保存：
![[Pasted image 20211130132003.png]]
![[Pasted image 20211130132122.png]]

# 我的例子
这个例子方便我后面自己取用。

```ini
bypass:
  - "*.bing.com"
  - "*.microsoft.com"
# Steam中国大陆地区游戏下载
  - "steampipe.steamcontent.tnkjmec.com" #华为云
  - "st.dl.eccdnx.com" #白山云
  - "st.dl.bscstorage.net"
  - "st.dl.pinyuncloud.com"
  - "dl.steam.clngaa.com" #金山云
  - "cdn.mileweb.cs.steampowered.com.8686c.com" #网宿云
  - "cdn-ws.content.steamchina.com"
  - "cdn-qc.content.steamchina.com" #腾讯云
  - "cdn-ali.content.steamchina.com" #阿里云
# Steam非中国大陆地区游戏下载/社区实况直播
  - "*.steamcontent.com"
# Battle.net战网中国大陆地区游戏下载
  - "client05.pdl.wow.battlenet.com.cn" #华为云
  - "client02.pdl.wow.battlenet.com.cn" #网宿云
# Epic Games中国大陆地区游戏下载
  - "epicgames-download1-1251447533.file.myqcloud.com"
# Rockstar Launcher客户端更新/游戏更新/游戏下载
  - "gamedownloads-rockstargames-com.akamaized.net"

```
