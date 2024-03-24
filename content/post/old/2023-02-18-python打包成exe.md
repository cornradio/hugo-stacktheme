+++
title = "如何把 Python 程序打包成 exe"
description = ""
date = 2023-02-18T22:27:09+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "python"
]
series = []
images = []
+++

我需要把我写的程序分给很多没有装 `python` 环境的人用（即使撞上了 `python` 环境，也会因为网络原因无法 `pip` 下载依赖），所以我需要把它打包成 `exe` ，这样使用门槛就可以很低了。

我主要参考了[这篇文章](https://blog.csdn.net/chichu261/article/details/106392385)。


## 我的场景
我的程序比较复杂，虽然是命令行程序，但是有很多依赖，并且程序文件分散在几个文件夹里。

## 如何打包
### 1. 安装 `pyinstaller`
```bash
pip install pyinstaller
```
### 2. 在命令行打包

我的主程序从main2.py开始，并且使用了三个库，采用自动覆盖不提示模式打包，命令如下：

我没有采用打包成单个exe的方式，听说打包成 **单个exe** 影响性能，本来程序性能就不太好……

```
pyinstaller -c main2.py --noconfirm --hidden-import pandas，bs4，json5 

```

pyinstaller:
* -c 命令行模式
* --noconfirm 不需要确认，直接覆盖文件
* --hidden-import 导入库

### 3. 复制配置文件

workdir下有一个config文件夹，里面有一些配置文件会在程序运行时动态加载，需要复制到打包后的文件夹里，这里我用了 `xcopy` 命令，如果你用的是 `linux` ，可以用 `cp` 命令。

这里其实完全可以手动复制，但是如果从 Devops 的角度来看，这个过程应该是自动化的。

```bat
xcopy config dist\main2\config\ /S /c /y
xcopy config\xml转换工具.bat dist\ /S /c /y
```

### 4. 检查打包结果

默认打包后的位置是 `dist\main2\main2.exe` 

推荐使用[windows沙盒](https://learn.microsoft.com/zh-cn/windows/security/threat-protection/windows-sandbox/windows-sandbox-overview)测试，如果测试使用没有问题，就可以把整个目录打包给别人用了。
