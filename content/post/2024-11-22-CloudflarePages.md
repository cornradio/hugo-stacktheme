---
title: Cloudflare Pages 免费部署静态博客
date: 2024-11-22 00:00:00+0000
slug: CloudflarePages
image: https://i.imgur.com/ODmqjpJ.png
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/CloudflarePages/&count_bg=%23F26E00&title_bg=%23000000)](https://hits.seeyoufarm.com)

## 为什么要换
因为一些费用的原因，我打算把我的服务器从vultr 上面给取下来，这样我就可以每个月省下来五刀左右的费用，相当于35块钱
但是同时我又不想放弃我这个博客,于是目前的做法是使用免费的 
[cloudflare pages](https://pages.cloudflare.com/)    
![](https://i.imgur.com/ODmqjpJ.png)
## 使用 cf pages
进入 [cloudflare ](https://dash.cloudflare.com/)， 左侧往下滑，找到 workers-and-pages ，选择 page。
page 可以通过从 github 同步 repo ， 或者直接上传静态 html 文件。

![](https://i.imgur.com/LZHREXt.png)

我选择同步 github repo ， 需要进行授权操作。
![](https://i.imgur.com/PzoXBsj.png)

## 配置域名
如果你想要用自己的域名的话,你不能直接去 dns 那边配,可能会导致打不开。   
需要直接在 pages 这里配置：
![](https://i.imgur.com/qXFIS2A.png)

## 后续使用
在这之后，每次写新blog直接通过github在线编写，这样就像是那些在线博客一样～ 
不通之处是过你拥有全部的博客源文件，并且博客的定制性更高

