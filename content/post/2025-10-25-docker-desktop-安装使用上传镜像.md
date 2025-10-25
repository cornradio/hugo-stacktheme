---
title: docker-desktop-安装使用上传镜像 # 标题
slug: docker-desktop # url(注释掉 和标题相同)
image: https://i.imgur.com/uTdXOiW.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2025-10-25 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fdocker-desktop-安装使用上传镜像&label=&icon=check-all&color=%23198754)

> 我发现，想要在使用代理的环境下上传镜像到 Docker Hub，使用 Docker Desktop 是一个不错（唯一）的选择。

以下教程针对windows。

# docker desktop 安装使用上传镜像
1. 下载 docker desktop https://www.docker.com/ 
2. 安装完成后，先不要重启，安装wsl ： https://learn.microsoft.com/zh-cn/windows/wsl/install  命令  `wsl --install`
3. 重启电脑，并开启`·tun·`模式（clash等软件）
4. 打开 docker desktop，登录 docker hub 账号(通过web页面)
5. 打开 powershell，打包/tag/上传等操作均可正常完成

欢迎顺便看看我的项目
https://github.com/cornradio/Lan-clip