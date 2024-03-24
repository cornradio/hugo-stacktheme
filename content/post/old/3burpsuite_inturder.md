+++
title = "burpsuite - 3 - inturder"
description = ""
date = 2022-12-21T16:00:59+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "burp"
]
series = []
images = []
+++

# inturder 
https://portswigger.net/burp/documentation/desktop/tools/intruder

burpsuite的inturder用于自动化攻击web应用，可以更换http请求中指定位置的payload，不停的发送请求。并收集返回的结果。
inturder 的天生特性可用于以下攻击范围：
- Fuzz 类型的input漏洞
- 进行暴力破解攻击
- 枚举攻击
- 快速收集有用的信息列表
> Fuzz 本意是 “羽毛、细小的毛发、使模糊、变得模糊”，在渗透测试中指的是一种基于黑盒或灰盒的测试技术，通过自动化生成并执行大量的随机测试用例来发现产品或协议的未知漏洞

# tutorial
基础教程会教会你怎么用intruder进行简单的，单个位置的payload攻击。
首先打开实验环境：
https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses
## http请求导入intruder
然后我们进入lab，点击登陆账户，模拟不知道账户和密码的情况：
![](https://i.imgur.com/7IKv51M.png)

然后我们找到刚才这条登陆的http请求，发送到intruder：
![](https://i.imgur.com/g80pcXZ.png)

来到intruder，他会自动标记几个可能是注入点的地方，我们先clear掉。
![](https://i.imgur.com/ACPEE8o.png)

然后手动选择用户名，添加一个新点位
![](https://i.imgur.com/XZf8hyA.png)

然后选择模式，我们选择sniper（狙击手）模式。其他模式啥意思我也看不太懂，我感觉就是不同种类的排列组合方法吧。
![](https://i.imgur.com/DVUAsF5.png)

## 破解用户名字段
然后我们到第二个页面，需要手动添加payload list，也就是字典，burp不提供字典。
教程可以用这个字典： https://portswigger.net/web-security/authentication/auth-lab-usernames
复制之后点击paste把我们的字典粘贴进来，然后点击右上角按钮，开始攻击
![](https://i.imgur.com/Aet6Ggx.png)

攻击过程中可以点击每一行查看发送的http请求，就是把你的标记位置*username*，变成了payload中的字符串。 通过Length排序，我们可以发现有一个返回值的长度和其他的不同，大家都是2984，他是2986。
![](https://i.imgur.com/xzRmd06.png)

点开respond发现，这里写着：“密码错误”，其他的请求都写着“用户名错误”，所以我们就找到一个可以用的用户名。用户名：alabama
![](https://i.imgur.com/UBPAiHn.png)

## 破解密码字段
我们通过上面的方法获取到了一个用户名，接下来就需要破解密码字段，首先回到intruder，修改http请求，把用户名换成刚才得到的值，然后开始破解密码位置：
![](https://i.imgur.com/vVXeyCb.png)

破解密码位置可以用这个字典，字典由burp教学网站提供： https://portswigger.net/web-security/authentication/auth-lab-passwords

破解过程很奇怪，有三种长度的返回值，2986 3073 170 ，2986和3073都是错误的，然后我就找到了密码：biteme
![](https://i.imgur.com/7rj0j1C.png)

最后就登陆成功，解决了这个lab。
![](https://i.imgur.com/bJHjLGR.png)

# 结尾
虽然破解成功了，不过很明显重要的是字典。首先用户名的字典，然后就是密码字典，我觉得现实中的网站密码绝对不会设置的这么简单。跑字典估计还没跑100个，我的ip就要被封禁了。

但是这个课程的重点是教你如何使用inturder工具，通过课程我觉得还是看的很清楚的。后续使用的话主要需要关注这几点：
- 自己搞一份好用的字典
- 后续可以研究一下不同的模式都是啥样的有什么特点，现在只用了sniper模式。