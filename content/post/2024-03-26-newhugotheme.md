---
title: 新的HUGO主题 # 标题
date: 2024-03-26 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
slug: newhugotheme # url(注释掉 和标题相同)
# description: xxxx # 描述小字(注释掉 不显示描述)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)
image: SLACK.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---


我换了一个新的HUGO主题, 你们觉得怎么样?

总结了一下这个新主题的几个优点：
- 默认样式好看
- 侧边导航好用
- 头图好看

但是他也有一些缺点：
- 配色冷淡
- 图片放置麻烦
- 预览需要环境较多

我之前的主题也还能用, 但是新版的hugo不支持我那个旧主题了,在编译的时候会报错。于是我想不如趁此机会直接换个新的主题吧。

## 官方网站(教程)
https://github.com/CaiJimmy/hugo-theme-stack-starter

## 前置操作
需要安装  git 和 [Go](https://go.dev/dl/) 以及 [hugo-extended](https://github.com/gohugoio/hugo/releases/download/v0.124.0)


## 修改配置文件

`config/_default/config.toml`

```
baseurl = "https://cornradio.github.io/hugo"
title = "CornRadio Blog"
```

修改头像 ：`assets\img\avatar.png`

修改头像角标、个性签名、不显示头像：`config\_default\params.toml`
以及修改footer时间和文字
```
[sidebar.avatar]
enabled = true

[sidebar]
emoji = ""
subtitle = "The more you know, the more you realize you don't know. - Aristotle"

[footer]
since = 1998
customText = "吸引力法则，大圣灵、外星人和心灵能量"
```


修改评论区： `config\_default\config.toml`

评论区使用的是这个系统： [disqus](https://disqus.com/admin/create/)


修改icon `static\favicon.png`

增加友链接、外链导航  `content\page\links\index.md`

## 增加文章
他这里的 blog 放在 `content/post` , 文件头部定语如下：

```js
title: abctest # 标题
date: 2024-02-26 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# slug: abc # url(注释掉 和标题相同)
# description: xxxx # 描述小字(注释掉 不显示描述)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)
# image: 2.jpg # 头图，注释掉，否则会有一个难看的呃加载不出来的图片

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
```

## 头图

头图有两种放置方式：
**第一种** 需要新建文件夹，每个文章放在文件夹里面。
```
post
└── xxx (文章的名称)
    ├── cover.png
    └── index.md
```

**第二种** 你需要，把`头图`都放到 `static` 文件夹中，并且做好独立名称（比如用post的文件名）。

