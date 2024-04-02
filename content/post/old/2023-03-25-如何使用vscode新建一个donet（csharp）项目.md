+++
title = "如何使用vscode新建一个donet（csharp）项目"
description = ""
date = 2023-03-25T00:06:47+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "csharp","dotnet","vscode"
]
series = []
images = []
+++

通常情况下，使用 Visual Studio 来编写 csharp 代码创建项目和管理非常的简单。但是，Visual Studio 是一个非常大的 IDE（而且visual studio mac版与win版并非同根同源，mac版本比较难用），如果您只是想编写一些简单的 csharp 代码，安装一个巨大的vs是不适合的。

- visual studio 来写csharp（常规选择）
- vs code + dotnet sdk （推荐选择）
<!--more-->

主要分成下列步骤：
- 安装 .NET Core SDK
-  安装 csharp 插件
-   配置插件
-   dotnet new 新建项目
-   dotnet run   跑代码

## 安装 .NET Core SDK
首先，需要安装 .NET Core SDK。可以在官网下载安装包进行安装：https://dotnet.microsoft.com/download ，我目前使用.NET 6.0。

## 安装 csharp 插件
然后，在 Visual Studio Code 中搜索安装 csharp 插件。按下 ctrl + Shift + x 打开扩展商店，搜索 "csharp" 并点击安装。

![第一个插件](https://raw.githubusercontent.com/cornradio/imgs/main/20230325000905.png)

## 配置插件
配置插件的作用是可以使用lint功能、对你的代码中的错误进行提示、自动补全等等。

右键插件，选择 "Configure Extension Settings"，在弹出的窗口中增加搜索关键词 sdk ，修改sdk位置（是上面你刚刚装好的路径）

如果在mac下你可以这么查找到他的安装路径。
```sh
$ which dotnet
/usr/local/share/dotnet/dotnet

# 进入上面的文件夹找到sdk文件夹
/usr/local/share/dotnet/sdk/6.0.407
```
![搜索并修改设置](https://raw.githubusercontent.com/cornradio/imgs/main/20230325001140.png)

## 新建项目
在终端中输入以下命令：

```sh
dotnet new console  --name HelloWorld 
```
在当前目录下创建一个名为 "HelloWorld" 的文件夹，并创建一个新的 .NET Core 控制台应用程序,

跑代码：现在其实已经可以运行代码了，直接在终端输入
```
dotnet run
```

---

## 创建vscode配置文件 
创建vscode配置文件，这样就可以在vscode中调试运行你的代码了，比如说打断点、查看变量值等等。
以及程序运行错误的时候，会标记指定的代码行数、错误信息等等。

要调试运行他还需要一个vscode配置文件。


打开Debug侧边栏，有一个按钮：
![按钮](https://raw.githubusercontent.com/cornradio/imgs/main/20230325001854.png)

点击这个按钮造成的效果是，会在你的项目根目录下生成一个.vscode文件夹
内容如下
```
.vscode
├── launch.json
└── tasks.json
```

### 配置launch.json
这个设置你可以修改下，内置的terminal有时候 会存在没有办法输入的问题。
![](https://raw.githubusercontent.com/cornradio/imgs/main/20230325004622.png)

### vscode 调试运行代码
在Debug侧边栏，点击绿色的箭头运行按钮。
或者 F5
