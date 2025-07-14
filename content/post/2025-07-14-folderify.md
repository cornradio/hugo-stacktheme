---
title: macos文件夹美化--folderify # 标题
slug: folderify # url(注释掉 和标题相同)
image: https://i.imgur.com/ydDiHFS.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2025-07-14 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Ffolderify&label=&icon=check-all&color=%23198754)

macos 的默认文件夹，比如“下载”、“桌面”等等，都是有默认的图标的。我们如何给自己的文件夹换上自己喜欢的图标呢？folderify 就是一个很好的工具。


## 1. 安装
```
brew install folderify
```

如果没有安装 Homebrew，可以先安装 Homebrew：
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
代理 brew 参考 ： https://developer.aliyun.com/mirror/homebrew/

## 2. 使用

你可以使用任何图片作为文件夹的图标，如果你没有合适的图片，可以使用下面网站获取，根据步骤来制作一个。

1. 去下载图标： https://tabler.io/icons (svg 下载到本地然后截图)
2. 可以使用 https://www.remove.bg/zh/upload 在线抠图工具，把白底截图变成透明底
3. 执行命令，替换文件夹图标，可以用 opt + cmd + c 复制目录地址（或者 opt+右键点击）
```
folderify mask.png /path/to/folder
```
4. 建议把图片都弄成正方形，可以和电脑系统的图标大小比较匹配

