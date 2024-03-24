+++
title = "clash 中的 minxin 使用教程"
description = "简单说，mixin是一种混合配置的方式，你可以把自己的配置注入到“配置文件”中 "
date = 2022-12-26T22:57:21+08:00
featured = false
comment = true
toc = true
categories = [
  ""
]
tags = [
  "clash"
]
series = []
images = []
+++

# 什么是mixin
mixin就是这个按钮，简单说，mixin是一种混合配置的方式，你可以把自己的配置注入到“配置文件”中，这样就可以在一定程度上的自定义配置了，比如加入一些你自己的规则之类的。
![](https://raw.githubusercontent.com/cornradio/imgs/main/20221226230540.png)
为了理解mixin，我们需要先了解什么是“配置文件”，clash的配置文件一般可以通过下面的方法查看
一般来说，从机场下载过来的配置中包含了规则相关内容，你可以通过下面的方式检视机场提供给你的配置。
![](https://raw.githubusercontent.com/cornradio/imgs/main/20221226230817.png)
除了检查配置之外，你还可以做出修改，diff功能：比如原来“漏网之鱼”都是走proxy的，我把这条标记为删除之后，clash在每次下载这个配置之后，都会删除这条。这样我所有的“漏网之鱼”都会走direct了。
![](https://raw.githubusercontent.com/cornradio/imgs/main/20221226230927.png)

# 使用mixin
我这里举例我自己的使用办法,我比较喜欢让网络默认走直连,如果直连不上的网站再走代理。所以，我在上面的步骤中先删除了“漏网之鱼”全部走proxy的配置。

这个取决于个人习惯，如果你日常上的网站都是没有办法直连的那么我推荐你直接默认代理，然后加一些直连规则

mixin的设置位置在这里。
![](https://raw.githubusercontent.com/cornradio/imgs/main/20221226231515.png)
他会默认使用自带的编辑器打开，我不喜欢，可以用外置vscode打开，使用外置编辑器的功能在这里开启：
![](https://raw.githubusercontent.com/cornradio/imgs/main/20221226231635.png)

配置文件的默认格式我建议直接删除，因为我到现在也看不出来它到底是做什么的…… 你可以参考我现在的配置来建立自己的mixin配置。mixin是有JavaScript和yaml两种版本的，我使用的是yaml，yaml要注意缩进，我是用它是因为比js要简单一点，尤其是你有vscode的时候对齐很简单。

简单解释两条：

```yaml
- 'DOMAIN-SUFFIX,redditstatic.com,PROXY'
  全域名匹配模式，域名，走proxy    
- 'DOMAIN-SUFFIX,edu.tw,DIRECT'
  域名后缀匹配模式，域名，走direct
```

# 关于国内是否能够访问
我这里推荐使用站长工具：多地ping，可以看到国内的ping值，如果ping值很高，那么就说明国内访问不了，就得加进代理。
https://ping.chinaz.com/baidu.com

# 通过chrome网络工具查看需要添加规则的域名
一般来说，很大型的网站往往都有好多不一样的子域名，有的是站点内容，有的是图片存储。对于这种我们需要把所有的子域名都加进去，这个时候就需要用到chrome的网络工具了。

如果你想要添加一个网站的规则，可以通过chrome的网络工具来查看这个网站的所有建立的连接，有连接不上的域名加入mixin配置中即可。


# 我的例子
```yaml
rules:
    # direct:
    - 'DOMAIN,sub.godetia.xyz,DIRECT'
    - 'DOMAIN,vpsgongyi.com,DIRECT'
    - 'DOMAIN-SUFFIX,edu.tw,DIRECT'
    #steam direct
    - 'DOMAIN,steampowered.com,DIRECT'
    - 'DOMAIN,steamcommunity.com,DIRECT'
    #derpi
    - 'DOMAIN,derpibooru.org,PROXY'
    - 'DOMAIN,derpicdn.net,DIRECT'
    # proxy:
    - 'DOMAIN,docs.cfw.lbyczf.com,PROXY'
    - 'DOMAIN,patreon.com,PROXY'
    - 'DOMAIN,outlook.live.com,PROXY'
    - 'DOMAIN,pony.town,PROXY'
    - 'DOMAIN,gamepad-tester.com,PROXY'
    - 'DOMAIN,stackoverflow.com,PROXY'
    - 'DOMAIN,services.gradle.org,PROXY'
    - 'DOMAIN,openuserjs.org,PROXY'
    - 'DOMAIN,stackoverflow.com,PROXY'
    - 'DOMAIN,gamepadviewer.com,PROXY'
    - 'DOMAIN,go.microsoft.com,PROXY'
    - 'DOMAIN,nginx.org,PROXY'
    - 'DOMAIN,marketplace.visualstudio.com,PROXY'
    - 'DOMAIN,musicnotes.com,PROXY'
    - 'DOMAIN,fimfiction.net,PROXY'
    - 'DOMAIN,softonic.com,PROXY'
    - 'DOMAIN,zh.wikipedia.org,PROXY'
    - 'DOMAIN,nordvpn.com,PROXY'
    - 'DOMAIN,w3schools.com,PROXY'
    - 'DOMAIN,cdn.jsdelivr.net,PROXY'
    - 'DOMAIN,www.patreon.com,PROXY'
    - 'DOMAIN,getrolan.com,PROXY'
    - 'DOMAIN,cdnjs.cloudflare.com,PROXY'
    - 'DOMAIN,cdn.jsdelivr.net,PROXY'
    - 'DOMAIN,fonts.googleapis.com,PROXY'
    - 'DOMAIN,hugothemesfree.com,PROXY'
    - 'DOMAIN,ssltd.xyz,PROXY'
    - 'DOMAIN,forums.terraria.org,PROXY'
    - 'DOMAIN,c.biancheng.net,PROXY'
    - 'DOMAIN,alcorart.com,PROXY'
    - 'DOMAIN,uso.kkx.one,PROXY'
    - 'DOMAIN,grabient.com,PROXY'
    - 'DOMAIN,dollarexcel.com,PROXY'
    - 'DOMAIN,vscode.dev,PROXY'
    - 'DOMAIN,userstyles.world,PROXY'
    - 'DOMAIN,npmjs.com,PROXY'
    - 'DOMAIN,hath.network,PROXY'
    - 'DOMAIN,www.emojiall.com,PROXY'
    - 'DOMAIN,go.ezodn.com,PROXY'
    - 'DOMAIN,cd.connatix.com,PROXY'
    - 'DOMAIN,itch.io,PROXY'
    - 'DOMAIN,coub.com,PROXY'
    - 'DOMAIN,chaturbate.com,PROXY'
    - 'DOMAIN,highwebmedia.com,PROXY'
    - 'DOMAIN,diygod.me,PROXY'
    - 'DOMAIN,*.fandom.com,PROXY'
    - 'DOMAIN,www.dogfight360.com,PROXY'
    - 'DOMAIN,www.screentogif.com,PROXY'
    - 'DOMAIN,www.techworld-with-nana.com,PROXY'
    # 开卡车游戏\openai
    - 'DOMAIN,slowroads.io,PROXY'
    - 'DOMAIN-SUFFIX,openai.com,PROXY'
    - 'DOMAIN-SUFFIX,sentry.io,PROXY'
    # reddit
    - 'DOMAIN-SUFFIX,redditstatic.com,PROXY'
    - 'DOMAIN-SUFFIX,redd.it,PROXY'
    # from rocket
    - 'DOMAIN-SUFFIX,nhentai.to,PROXY'
    - 'DOMAIN-SUFFIX,chaturbate.com,PROXY'
    - 'DOMAIN-SUFFIX,xvideos.com,PROXY'
    - 'DOMAIN-SUFFIX,derpibooru.org,PROXY'
    - 'DOMAIN-SUFFIX,pornhub.com,PROXY'
    - 'DOMAIN-SUFFIX,sex.com,PROXY'
    - 'DOMAIN-SUFFIX,www.sex.com,PROXY'
    - 'DOMAIN-SUFFIX,equestria.social,PROXY'
    - 'DOMAIN-SUFFIX,openai.com,PROXY'
    - 'DOMAIN-SUFFIX,redditmedia.com,PROXY'
    - 'DOMAIN-SUFFIX,chat.openai.com,PROXY'
    - 'DOMAIN-SUFFIX,redd.it,PROXY'
    - 'DOMAIN-SUFFIX,reddit.com,PROXY'
    - 'DOMAIN-SUFFIX,netlify.app,PROXY'
    - 'DOMAIN-SUFFIX,patreon.com,PROXY'
    - 'DOMAIN-SUFFIX,sickipedia.net,PROXY'
    - 'DOMAIN-SUFFIX,naver.com,PROXY'
    - 'DOMAIN-SUFFIX,pstatic.net,PROXY'
    - 'DOMAIN-SUFFIX,tenable.com,PROXY'
    - 'DOMAIN-SUFFIX,e-hentai.org,PROXY'
    - 'DOMAIN-SUFFIX,v2ex.com,PROXY'
    - 'DOMAIN,www.ihezu.cn,PROXY'
    - 'DOMAIN-SUFFIX,www.ihezu.cn,PROXY'
    - 'DOMAIN-SUFFIX,mixkit.co,PROXY'
    - 'DOMAIN-SUFFIX,tunemymusic.com,PROXY'
    - 'DOMAIN-SUFFIX,soundcloud.com,PROXY'
    - 'DOMAIN-SUFFIX,*.github.io,PROXY'
    - 'DOMAIN-SUFFIX,*.github.com,PROXY'
    - 'DOMAIN-SUFFIX,netflix.com,PROXY'
    - 'DOMAIN-SUFFIX,nflximg.net,PROXY'

```