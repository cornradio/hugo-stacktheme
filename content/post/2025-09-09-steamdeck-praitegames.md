---
title: steamdeck-安装盗版游戏 # 标题
slug: steamdeck-praitegames # url(注释掉 和标题相同)
image: https://i.imgur.com/tiNW54t.jpeg # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2025-09-09 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fsteamdeck-praitegames&label=&icon=check-all&color=%23198754)

##  如何安装盗版游戏

- 在盗版[游戏网站]( https://www.gamer520.com/ )，下载游戏
- 在电脑上解压好，运行一下确保没有问题
- 通过 sftp 软件，比如 [winscp](https://winscp.net/eng/download.php) 上传到 steamdeck 上 （需要先[开启steamdeck的ssh功能](https://www.google.com/search?q=%E5%BC%80%E5%90%AFsteamdeck%E7%9A%84ssh&oq=%E5%BC%80%E5%90%AFsteamdeck%E7%9A%84ssh)）
- 在steamdeck的桌面模式下，选择对应exe文件，右键添加到steam

![picture 1](https://i.imgur.com/XALCinj.jpeg)  

- 在桌面steam库找到游戏，然后点击**设置-属性-兼容性**-勾选强制使用特定steamplay兼容工具（我一般用 Proton Experimental)

![picture 0](https://i.imgur.com/tiNW54t.jpeg)  

- 运行游戏

## 特殊情况
- 某些游戏会提示没有许可，无法运行，这时候可以用下面的方法
- 新增一个txt，把这个txt和exe放在同一个目录下
- 命名为`steam_appid.txt`
- 在txt中写入游戏的steam id，比如`205790` （Dota 2 Test 的 id）（可以在 https://steamdb.info/ 上搜索一些免费的不好玩的游戏名称，找到对应的id）

![picture 2](https://i.imgur.com/SH1jk3Z.jpeg)  
然后再次启动就可以游玩了。

## 增加游戏封面
这个比较复杂，首先需要 [decky loader](https://decky.xyz/)，然后安装[SteamGridDB](https://www.steamgriddb.com/)插件。  
这样在点击设置图标时候就能看到很多别人上传的封面了。甚至还有动图。

### 安装decky loader
https://decky.xyz/ 下载到这个文件 : decky_installer.desktop，然后双击运行就可以了。会联网下载安装，我测试国内网络也可以用。

### 安装SteamGridDB插件
- 打开decky loader，点击插件商店
- 搜索 SteamGridDB
- 点击安装
![picture 3](https://i.imgur.com/hYutur5.png)  


