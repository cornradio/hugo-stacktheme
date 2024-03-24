+++
title = "Csahrp Arg Test"
description = "让 csharp 接受命令行参数的测试"
date = 2023-06-28T12:00:40+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "csharp","命令行参数"
]
series = []
images = []
+++

## 前言
命令行参数在csharp中有专门的类库，<https://github.com/commandlineparser/commandline> \

不过这个文章从底部的原理开始，不使用这么多功能的类库，并实现简单的参数处理功能。

## csharp 接受命令行参数（简单例子）
csharp 接受的命令行参数其实就是一个 string 数组：

这是一个简单接受参数输入的程序

```cs
static void Main(string[] args)
{
    // 判断是否有传入参数
    if (args.Length > 0)
    {
        // 使用参数 args[0]
        for (int i = 0; i < args.Length; i++)
        {
            Console.WriteLine($"传入的参数 {i} 是: " + args[i]);
        }
    }
    else
    {
        Console.WriteLine("没有传入参数。");
    }
    Console.ReadLine();
}
```
你可以如下方式使用它

```bat
.\CsahrpArgTest.exe -PentestReport "c:/a.docx"
```

输出结果如下

    传入的参数 0 是: -PentestReport
    传入的参数 1 是: c:/a.docx

## 传参测试脚本

为了方便测试，我编写了一个小脚本（powershell格式）：

他的功能是 build 项目，然后运行程序，传入参数
  
```ps1
$originalPath = Get-Location
Set-Location CsahrpArgTest/
dotnet build
echo --runcode:--------------------------------
Set-Location bin/Debug/net7.0
.\CsahrpArgTest.exe -PentestReport "c:/a.docx"

# 恢复原始工作目录
Set-Location $originalPath
```

## 传参-更实际的的例子

我们实际使用的程序中，更常见的是这样的参数传递方式：

```
.\CsahrpArgTest.exe --pentestreport "c:/a.docx"
```

我们使用 switch 语句来处理参数 arg0

下面的例子函数中中包含：
- -h 的处理
- -p 的处理
- 未知参数的处理

```cs
public static bool processArgs(string[] args)
{
    // 判断是否有传入参数
    if (args.Length > 0)
    {
        string arg0 = args[0];
        switch (arg0)
        {
            case "--help":
            case "-h":
                Console.WriteLine(@"帮助信息：
  本软件可以使用参数如下：
  --help, -h: 打印帮助信息
  --pentestreport <path> ,-p <path>: 指定渗透测试报告路径并转换");
                return true;
                break;

            case "--pentestreport":
            case "-p":
                if (args.Length > 1)
                {
                    string reportPath = args[1];
                    Console.WriteLine("渗透测试报告路径：" + reportPath);
                    return true;
                }
                else
                {
                    Console.WriteLine("未指定渗透测试报告路径");
                    return false;
                }
                break;

            default:
                Console.WriteLine("未知参数：" + arg0);
                return false;
                break;
        }
    }
    else
    {
        Console.WriteLine("没有传入参数");
        return false;
    }
}
```