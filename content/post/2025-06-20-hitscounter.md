---
title: hits counter 点击计数器 # 标题
slug: hitscounter # url(注释掉 和标题相同)
image: https://i.imgur.com/wIMGmVT.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2025-06-20 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fhitscounter&label=&icon=check-all&color=%23198754)


我发现 blog 中之前的 hits counter 都挂掉了，于是我找到了新的：
https://hitscounter.dev/

以及他的 github 项目地址： https://github.com/donaldzou/hits-counter

此外我发现我在 测试查看 blog 的时候，imgur 的图片也加载不出来
还在研究问题所在？
经过研究 发现问题在于 strict-origin-when-cross-origin ， 这个浏览器的政策更新了，以前可以的。

问题找到了， https://stackoverflow.com/questions/10883211/why-does-my-http-localhost-cors-origin-not-work

解决方法是测试的时候，访问本地不要用 ip，用域名即可。 比如， [http://localhost:51000/](http://localhost:51000/) 这样就可以了。