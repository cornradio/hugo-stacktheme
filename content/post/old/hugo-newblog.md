+++

title = "hugo博客"
date = "2021-05-29"
author = "kasusa"
cover = ""
tags = ["博客", "hugo"]
keywords = ["hugo2", ""]
description = "今天我建立了我的hugo博客"
showFullContent = false

+++

![](https://tvax1.sinaimg.cn/large/0083vuQJgy1gqzlm00z45j30hs06z0sq.jpg)

### 剧情介绍

> 今天yr在我旁边弄新的hugo主题，我感觉他的新主题真的很清新，很不错，然后markdown记录之类的确实要比转化成html再放出来更加简单。不过可定制性没有那么好也是实话。
>
> 这个博客对于语法高亮支持很不错。交互和动画就只能限制于模板（这个语法蛮怪的，可能以后会研究一个自己的模板）所以暂时决定把这个弄成技术类博客。
>
> 我终于能把我的linux小知识都搬过来了！



//简单说一下hugo的安装和使用：

### pwershell安装hugo

choco install hugo 

### 创建hugo工作目录

hugo new site mysite

### 进入themes文件夹并且git pull自己用的主题

git clone https://github.com/panr/hugo-theme-terminal.git themes/terminal

- [主题市场](https://themes.gohugo.io/)
- [terminal主题(我现在用的)](https://github.com/panr/hugo-theme-terminal/)

### 配置主题

配置主题需要根据不同的主题情况,各有不同，对于我这个主题来说我要把博客官方的 `config.toml` 粘贴到hugo项目中，并且进行了一点修改。遇到了一点坑，我在后面注释，你可以看一下。

toml文件：

```toml
baseurl = "" #这个要设为空，否则生成的东西css会找不到。
languageCode = "en-us"
theme = "terminal" 
# theme 原本github上提供的版本是 "hugo-theme-terminal"，
# 但是会造成编译错误，故修改
paginate = 5

[params]
  contentTypeName = "post"
  themeColor = "red" #选择主题
  showMenuItems = 2 
  #选择显示在顶部的导航链接数目，超出的会折叠。
  #链接具体目录可以在下面修改
  fullWidthTheme = false
  centerTheme = false

[languages]
  [languages.en]
    title = "KASUSA"
    subtitle = "kasusa的技术博客"
    keywords = ""
    copyright = ""
    menuMore = "展开"
    readMore = "品读"
    readOtherPosts = "看看别的文章

    [languages.en.params.logo]
      logoText = "KASUSA"
      logoHomeLink = "/"

    [languages.en.menu] #顶部栏条目们（不知道顺序是按照什么计算的）
      [[languages.en.menu.main]] #一个顶部栏条目
        identifier = "about" #id
        name = "About_theme" #顶部条目显示为什么文字
        url = "/about" #点击后进入什么目录
      [[languages.en.menu.main]]
        identifier = "showcase"
        name = "Showcase"
        url = "/showcase"

```

### 写博客

在 content - posts 内新建md文件，系统会用mdmd文件内容生成博客。

对于md文件顶部的格式有着特殊的要求，这个也是因主体而异的，具体的话就要参考你的`theme`中`archetypes`文件夹内提供的模板了。我这个主题提供的模板如下：

```md
+++
title = "hugo博客" 
date = "2021-05-29"
author = "kasusa"
cover = "https://tvax1.sinaimg.cn/..."
tags = ["博客", "hugo"]
keywords = ["hugo2", ""]
description = "今天我建立了我的hugo博客"
showFullContent = false
+++
```

我感觉他已经很明白了，但是我遇到了一个坑就是日期，我打成了2021-5-29在预览的时候就会显示成00-01-00，要注意日期格式必须相同哦！

### 实时预览

`hugo server -t terminal -p 51000`

`-t`是自定义主题，`-p`是自定义端口，开启成功之后他会根据你后台文件的变化不停的刷新，你可以在

`localhost:51000` 实时的预览。

### 编译生成HTML

在你的项目的目录输入命令（生成到指定目录）：

`hugo -d C:\Users\kasusa\Documents\GitHub\kasusa.github.io\hugo`

默认的话文件会生成在`public`文件夹。 

然后就把public文件夹的内容上传到github即可。以后也许会考虑 [使用action自动编译](https://yantree.github.io/posts/develop/2020-06-20-action-delopy-github-page/)



