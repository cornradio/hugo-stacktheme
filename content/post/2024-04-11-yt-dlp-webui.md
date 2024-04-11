---
title: yt-dlp-webui 视频下载器（docker部署版） # 标题
slug: yt-dlp-webui # url(注释掉 和标题相同)
image: ytdlpweb.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2024-04-11 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/yt-dlp-webui/&count_bg=%230C0E0A&title_bg=%23000000)](https://hits.seeyoufarm.com)

[yt-dlp-webui](https://hub.docker.com/r/marcobaobao/yt-dlp-webui) 是 [yt-dlp](https://github.com/yt-dlp/yt-dlp/releases)（命令行工具）的一款网页UI，
使用起来门槛比较低（但是安装门槛挺高的），还蛮好看的!

关于yt-dlp的使用可以看这个[文章](https://www.appinn.com/yt-dlp-cookies-from-browser/)

## 下载安装

```
docker run -p 7892:3033 marcobaobao/yt-dlp-webui:latest
```

浏览器访问： http://127.0.0.1:7892
此时已经可以随意下载 bilibili 等网站的视频了。
## 代理

为了能够下载youtube视频，需要挂代理 ， 需要开启参数功能（设置-Enable custom yt-dlp args 开启）

实现挂代理下载，还需要一个**代理服务器**，这里就使用本机电脑，因为这样最方便；

比如我在电脑上开启了clash，只需要开启【允许局域网链接】功能。 并查询到电脑内网ip地址，我就获得了代理地址：http://192.168.50.32:7890

### 参数如下

```
--proxy http://192.168.50.32:7890
```


## 指定参数下载

新建一个下载：输入网址和启动参数
![1712804451781.png](https://img2.imgtp.com/2024/04/11/9HkHB4vl.png)

## 参数模板

用参数模板可以保存制定参数，不用每次手打。

设置参数：加号 - 设置图标（tamplet editor）可以增加常用的参数，比如把上面这条proxy增加保存成一个常用模板：

```
# template name
proxy
# template content
--proxy http://192.168.50.32:7890
```

## 视频下载

视频默认下载到docker容器里面，需要把它下载到本机步骤：
- 左边archive菜单
- 右键指定视频- download