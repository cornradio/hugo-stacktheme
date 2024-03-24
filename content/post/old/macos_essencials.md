+++
title = "mac essencials"
description = ""
date = 2022-07-02T20:03:07+08:00
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  ""
]
series = []
images = []
+++
# mac必装软件
- 粘贴版历史记录软件（AppleStore）

![image](https://tvax1.sinaimg.cn/large/0083vuQJly1h3su6ef38mj30kk09amyk.jpg)
- 快捷键设置软件（可以设置快捷键打开任何安装的应用）（AppleStore）

![image](https://tva2.sinaimg.cn/large/0083vuQJly1h3su7a8wj3j307u096t9c.jpg)
- 解压软件（如果碰到了rar之类的，就需要第三方软件了）（AppleStore）

![image](https://tvax3.sinaimg.cn/large/0083vuQJly1h3su954sxkj309g0aa3zm.jpg)

- 滚轮优化软件

    在macos中，你的触摸板和鼠标滚轮的方向只能是一样的，这让我非常不习惯，我比较喜欢触摸板反转，但是滚轮是正常方向。

   - [ Scroll Reverser ](https://pilotmoon.com/scrollreverser/)
   - [ Mos ](https://github.com/Caldis/Mos) ⬅️ 我更喜欢这个，还能让鼠标滚动更平滑
 
![image](https://tvax2.sinaimg.cn/large/0083vuQJly1h3suamga44j30k009m40v.jpg)

- [clashX]( https://github.com/yichengchen/clashX)

![image](https://tva3.sinaimg.cn/large/0083vuQJly1h3susw0jtfj30bo09w3zu.jpg)

- 微软远程桌面（RDP） [microsoft-remote-desktop](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) （预览版免费，还支持m1）

![image](https://tvax3.sinaimg.cn/large/0083vuQJly1h3sux0ldadj30cm09sgmr.jpg)

- [VLC](https://www.videolan.org/vlc/) mac的Quicktime支持格式不全，所以我有装这个。(视频软件我其实更想要mpv但是mpv还么有原生支持m1的版本--要自己编译啥的，坑挺多的)

![image](https://tvax3.sinaimg.cn/large/0083vuQJly1h3sv1jsbnoj30ag09k3zi.jpg)

- [Snipaste](https://www.snipaste.com/) 截图软件--平常我都用自带的，但是有的时候需要钉住图片或者需要从剪切板预览的时候他还是很好用的。

![image](https://tvax4.sinaimg.cn/large/0083vuQJly1h3sv6oesrdj30as08igm0.jpg)

# mac常备脚本

Mac 的网络硬件地址更换：
```
sudo /System/Library/PrivateFrameworks/Apple80211.framework/Resources/airport -z
sudo ifconfig en0 ether 2d:d4:e8:f8:e0:c6
```

在重启之后，mac会恢复成硬件默认值，不过我还是推荐备份一下

---

 ～/.zshrc
```conf
# path加入ptyhon pip
export PATH=~/bin:/Users/kasusa/Library/Python/3.8/bin:$PATH
# 增加ll功能
alias ll='ls -lG'
#显示有颜色的用户（不适合白色背景）
export PS1="%10F%m%f:%11F%1~%f \$ "


```

---

# 包管理器

https://brew.sh/ 这是homebrew，可以像是apt一样用，但是可能需要先给shell挂代理。

![image](https://tva4.sinaimg.cn/large/0083vuQJly1h3svdogcxyj31em0iin0u.jpg)

