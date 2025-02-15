---
title: 本地部署 deepseek R1 大模型 # 标题
date: 2025-02-15 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
slug: deepseed-local-deploy # url(注释掉 和标题相同)
# description: xxxx # 描述小字(注释掉 不显示描述)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)
image: https://i.imgur.com/7JcYMcq.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/deepseed-local-deploy/&count_bg=%23F26E00&title_bg=%23000000)](https://hits.seeyoufarm.com)

## 检查配置 
这网站很强的，好多命令都能在里面直接找，不需要看别的东西
https://tools.thinkinai.xyz/
![](https://i.imgur.com/3tSDNeX.png)

## 下载ollama
https://ollama.com/

![](https://i.imgur.com/qT49ccK.png)


## 运行命令安装模型

包括下载镜像速度还挺快的不用翻墙  
这个模型还是挺大的10个 g   
也不知道他下哪儿去了反正我电脑空间多
```
ollama run deepseek-r1:14b
```

 Windows 电脑还要安装这个cuda （这是网站教程上说的但是我实测好像并不需要）
![](https://i.imgur.com/1V7aOWy.png)


## 安装 webui
毕竟用这个网页端还是比较方便 命令行也太麻烦了
![](https://i.imgur.com/SF2Ex2n.png)

```
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```
预想好之后会开启在这个网站：
你就可以体验到你自己本地在跑的模型了。

http://127.0.0.1:3000/
![](https://i.imgur.com/6tFlB1X.png)

据说这里能有无审查版的模型下载 https://huggingface.co/huihui-ai/DeepSeek-R1-Distill-Qwen-14B-abliterated-v2
