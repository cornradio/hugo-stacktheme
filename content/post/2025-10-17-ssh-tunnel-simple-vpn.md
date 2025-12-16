---
title: ssh tunnel 搭建简易 vpn # 标题
slug: ssh-tunnel-simple-vpn # url(注释掉 和标题相同)
image: https://i.imgur.com/51uKFw9.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2025-10-17 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fssh-tunnel-simple-vpn&label=&icon=check-all&color=%23198754)

因为我发现我阿里云搭建的 wireguard 总是被封，所以尝试使用 sshtunnel，简单来说就是ssh -D 命令。搭建socks通道。

然后让本地的代理工具，比如clash verge 使用这个隧道，加上tun模式开启网卡级别全局代理。这样就可以做到把本地的socks ssh tunnel 变成vpn ，路由整个电脑的流量了。

1. 开启ssh隧道，开启后保持命令行打开。
```
ssh -D 1080 root@123.123.123.123 -p 22
ssh -D开启socks代理 1080端口 用户名@远程主机ip -p ssh端口
```

2. 进行测试--可以使用 switchy omega 建立一个简单的代理服务器，填写 socks5 ， 127.0.0.1 ， 1080
   然后尝试访问一些内网站点，比如 http://192.168.31.11/ 是我在内网的服务器地址
3. 创建一个xxx.yaml 用作clash配置文件，可以参考下面的模板

``` yaml 
proxies:
  - name: "My SSH Tunnel"
    type: socks5
    server: 127.0.0.1
    port: 1080

proxy-groups:
  - name: Proxy
    type: select
    proxies:
      - My SSH Tunnel
      - DIRECT

rules:
  - MATCH,Proxy

```
4. clashverge工具 - 订阅 - 新建
	1. 类型 local （本地文件），选择你的 yaml 文件
	2. 选择你这个本地订阅 xxx.yaml
	3. 进入代理页面，选择全局，然后选择 【My SSH Tunnel】 节点
	4. 右键开启 tun 模式
5. 完成以上操作，可以百度测试一下ip看看你的公网，应该已经改变了。
6. 还可以随时取消勾选 tun 模式的开关，这可比普通vpn链接断联快速多了。

