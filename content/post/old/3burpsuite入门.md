+++
title = "burpsuite（入门教学课程）"
description = ""
date = 2022-12-20T16:14:59+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "linux"
]
series = []
images = []
+++

# burpsuite（入门教学课程）
- Intercept and modify HTTP traffic with **Burp Proxy**.
- Set the target scope to focus your work on interesting content.
- Probe for vulnerabilities by reissuing requests with **Burp Repeater**.
- Run automated vulnerability scans and generate reports with **Burp Scanner**.

# intercept （拦截）流量
  https://portswigger.net/burp/documentation/desktop/getting-started/intercepting-http-traffic
  ![](https://i.imgur.com/CJyXrzi.png)
  拦截请求（intercept）之后，可以慢慢查看、修改请求，弄好了之后再点forward。
  如果你需要好多步骤之后才开始用burp，那应该先把intercept关闭，即便是这时http请求也会被记录。

# hack 例子商店

https://portswigger.net/burp/documentation/desktop/getting-started/modifying-http-requests

商店地址：`https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls`
你需要先注册一个portswigger账号，因为这个东西是人家要给你生成一个实例给你黑，所以你得注册账号让他知道你是真人......

登录用户名和密码：**Username:** `wiener` **Password:** `peter`
然后你会发现你的账号里面有100\$可以用来买东西。

开启intercept，购买一个这个1000\$ + 的jacket，然后你会收到一个POST /cart 请求。

在请求的最下面有一个`productId=1&redir=PRODUCT&quantity=1&price=133700`，最后面是以美分为单位的价格，修改这个数字，改成1，然后我们就能有极低的价格（1美分）把这个商品加入购物车。
在购物车结算（**Place order**）之后，这个lab就完成了。同时你也学会了intercept, review, manipulate HTTP traffic using Burp Proxy。真棒。

# target scope

修改目标范围，有时候网页会加载很多外链或者你不想要了解的目标，这时候需要自定义目标范围。
https://portswigger.net/burp/documentation/desktop/getting-started/setting-target-scope
打开这个实验室：
https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-error-messages

打开http请求，倒序，然后选择你想要的url，右键加入scope
![](https://i.imgur.com/SlZKo9T.png)
加入了scope的东西可以在这里修改：
![](https://i.imgur.com/ipVDjO8.png)
scope里面有东西了之后，可以在http请求里面使用filter，只查看scope内的相关url记录
![](https://i.imgur.com/DNLxl8o.png)

# Burp Repeater
首先打开上一课的假的商店，设置好scope，然后我们会看到
每次打开商品详情，会有这样的请求（Get /product?productId=xx）：
我们右键 - 发送到repeater
![](https://i.imgur.com/BeFkPse.png)

然后在repeater里面发送和查看respond，就是repeater的主要功能
![](https://i.imgur.com/21dBy9v.png)
我们修改一下productid为100试试：结果返回了notfound
然后我们发送了好几次之后，可以通过这个按钮查看历史记录。
![](https://i.imgur.com/6IAhcLJ.png)
然后我们把这个productid改成一个非数字，看看会有什么反应：
![](https://i.imgur.com/ctXIM6g.png)
结果返回了一堆错误信息，而且是没有做删减的，我们可以看出来Apache的版本号，这对于渗透来说是有意义的，尤其是这个版本的apache有漏洞可以用。
这里最后我们点击页面上的submit，把这个版本号填进去，这个lab就完成了 耶～

# burp scan

burp同样耶提供扫描的功能，他的扫描远离如下：
1. 爬网页crawl（通过模拟用户操作的方式，比如点击链接等）
2. 审计危险项audit（漏洞扫描）
注：burpscan只有专业版能用；非授权扫描别人的网站应用是违法的各位注意。
我们这里扫描他提供的例子站点：https://ginandjuice.shop/
![](https://i.imgur.com/0xuOa32.png)
scan的时候可以在target里面看看网站目录啥的
![](https://i.imgur.com/v3STT83.png)
