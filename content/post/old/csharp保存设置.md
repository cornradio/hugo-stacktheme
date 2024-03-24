+++
title = "C# 保存程序设置"
description = ""
date = 2021-11-30T22:42:30+08:00
featured = false
draft = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "c#"
]
series = []
images = []

+++

一个可视化应用程序难免要保存一些数据，保存数据如果要自己手动操作文件的话就感觉很麻烦，好在微软提供一个很好用的保存功能，这就让我给你讲一下：

这里是我写的一个小c#程序，需要保存的内容就是这上面4个textbox的东东。
# 操作
1. 右键项目属性，选择左侧的设置
2. ![Snipaste_2021-11-30_22-39-43](https://tvax4.sinaimg.cn/large/006rgJELly1gx29nlfid0j31100mznbw.jpg)
3. 增加一些变量名称，这里还能手动选择变量类型、默认值（范围选择用户即可，然后应该会保存到一个用户文件夹下面的一个不知道什么鬼地方） 
4. 访问：
```csharp
using hugoAuto1.Properties;

textBox1.Text = Settings.Default.source;
```
4. 保存：
```csharp
using hugoAuto1.Properties;

Settings.Default.source = textBox1.Text;
Settings.Default.Save();
```

原理和操作就是这么简单，用起来也很方便！
