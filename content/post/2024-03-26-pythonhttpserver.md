---
title: Python HTTP server # 标题
date: 2024-03-26 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
slug: pythonhttpserver # url(注释掉 和标题相同)
# description: xxxx # 描述小字(注释掉 不显示描述)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)
image: python http server.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片

tags: # 只能在侧面看到的标签,会显示在文章的底部
    - python
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---


```sh
python3 -m http.server
# 自定义端口
python3 -m http.server 80
```

注意这个会把你的所在文件夹直接全部暴露出来，默认使用 8000 端口 

---
我这里是开启 httpserver 作为临时服务器 让别人可以访问我的文件
为了让他们能访问，还需要看一下我的内网ip

```py
# mac
ip | grep inet 
# win
ipconfig | findstr IPv4
# linux
ip addr  | grep inet 
```

如果还是访问不了注意查看防火墙,关闭防火墙；
windows 防火墙需要增加入规则才可以被访问
```sh
# 运行 win + R
wf.msc
```
