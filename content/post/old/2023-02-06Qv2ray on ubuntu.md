+++
title = "install Qv2ray on ubuntu"
description = ""
date = 2023-02-06T14:21:50+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "ubuntu"
]
series = []
images = []
+++
## install Qv2ray
install `qv2ray` in snap store.

## get core of Qv2ray
go to this link on git hub to download  [>this link<](https://github.com/v2fly/v2ray-core/releases/tag/v4.31.0)

unzip core to whatever floder, set up the core path in `Qv2ray - Preferences - Kernel Settings` and it's all done!

>use your phone as a proxy router , speed up download process.

## settings
after you get your servers into  Qv2ray , you have to goto ubuntu settings and set up` system proxy ` to make it work 

go to `system proxy - Network Proxy` set `127.0.0.1:1089` for socks(this is default port), then it will work.

> rember some application doesn't follow this setting.