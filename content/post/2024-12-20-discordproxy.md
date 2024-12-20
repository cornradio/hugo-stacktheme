---
title: Discord proxy-给discord上代理
date: 2024-12-20 00:00:00+0000
slug: discordproxy
image: https://i.imgur.com/2jYJ6lu.png
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/discordproxy/&count_bg=%23F26E00&title_bg=%23000000)](https://hits.seeyoufarm.com)

# 如何使用 DiscordProxyStart.exe

DiscordProxyStart.exe 是一款实用工具，专为需要通过代理访问 Discord 的用户设计。  
以下是如何使用这款软件的简单指南。  
官方不支持任何形式的代理真的是太烦了,一定要开全局的话使用起来是很麻烦的。

## 第一步：下载与安装

1. 从 [GitHub 仓库](https://github.com/aiqinxuancai/DiscordProxyStart) 下载 DiscordProxyStart.exe。
2. 将文件解压到一个安全的文件夹中。
![](https://i.imgur.com/VKaCFSt.png)


## 第二步：准备代理服务器

1. 确保你已在本地运行 Clash。
    - Clash 默认会在本地的 `7890` 端口开放 HTTP 代理。

## 第三步：运行软件

编辑配置文件  Config.ini
```
[Config]
Proxy=http://127.0.0.1:7890
```

- 可以参考这个官方的 [config 配置写法](https://github.com/aiqinxuancai/DiscordProxyStart?tab=readme-ov-file#configini%E9%85%8D%E7%BD%AE%E4%BE%8B%E5%AD%90)

## 第四步：启动 Discord

1. 直接启动 DiscordProxyStart.exe 
2. 软件会自动通过代理启动 Discord 客户端


## 常见问题解答

### 1. 为什么无法连接？

- 检查 Clash 是否正常运行。
- 确认 Clash 配置文件中的规则是否正确。
- 检查防火墙或杀毒软件是否阻止了程序运行。


