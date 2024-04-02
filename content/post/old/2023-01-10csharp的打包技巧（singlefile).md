+++
title = "csharp的打包技巧（打包成singlefile)"
description = ""
date = 2023-01-10T16:10:14+08:00
featured = false
draft = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "csharp"
]
series = []
images = []
+++

> 我已经想要把我的小工具打包成单个程序很久了。但是一直不知道怎么操作
> 
> 今天看到reddit里面给我推送：[how_to_build_my_console_app_as_single_exe_file](https://www.reddit.com/r/csharp/comments/107juxi/how_to_build_my_console_app_as_single_exe_file/)
> 
> 但是进去看了一圈都是垃圾回答，所以我自己研究了一下（因为也确实需要）
> 
> 最后在youtube视频评论里找到了答案。
>
> 使用了 dotnet 命令行，官方文档在这里：
> https://learn.microsoft.com/zh-cn/dotnet/core/tools/dotnet-publish

# 打包方法

1. 用vs2019 + 打开你的项目
2. 打开视图 - 终端
3. 输入需要的命令，有两种

打包成单个文件的命令：

```
dotnet publish -r win-x64 -p:PublishSingleFile=True --self-contained false --output "C:\abc"
```

打包成单个文件（带.net core环境）的命令：
> 包比较大，但是兼容性会好，因为不需要客户端安装环境
> 我没有测试过.net frame work的打包功能，据说那个不能连同环境一起打包

```
dotnet publish -r win-x64 /p:PublishSingleFile=true /p:IncludeNativeLibrariesForSelfExtract=true /p:PublishTrimmed=true --output "C:\abc"
```

---

打包这里面的 pdb 文件可以删除，他是用来调试的

可以看出来那个带了环境的的打包文件就大很多。

我用 windows sandbox 测试了，真的有用，sandbox 里面没有安装过.net环境也可以运行那个带环境的打包版本。

![示例图](https://raw.githubusercontent.com/cornradio/imgs/main/20230110174158.png)