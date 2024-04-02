+++
title = "csharp执行命令"
description = "使用csharp执行任何命令（模拟cmd的输入）"
date = "2021-11-14"
featured = false
comment = true
toc = true
reward = true

tags = [
  "csharp","编程"
]

+++



```csharp
using System.Diagnostics;

private void runincmd(string yourcommand)
{
string strCmdText;
strCmdText = $"/C {yourcommand}";
Process.Start("CMD.exe", strCmdText);
}
```

Process.Start(string 程序, string 参数);

程序最好是有完整的地址，如果不需要传入参数的话可以只传入一个参数。

上面这个语句启动一个程序并且可以附带一些参数，本质上是把要执行的命令作为windows cmd 的参数传入了，所以只能传入一行，多行可能还需要写个bat脚本。

如果需要“**静音启动**”的话写起来比较麻烦，可以这么做到：

```csharp
ProcessStartInfo processStartInfo =
	new ProcessStartInfo(txtExecutable.Text.Trim(), txtParameter.Text.Trim());
//保持静音
processStartInfo.ErrorDialog = false;
processStartInfo.UseShellExecute = false;
//用于重定向输出
processStartInfo.RedirectStandardError = true;
processStartInfo.RedirectStandardInput = true;
processStartInfo.RedirectStandardOutput = true;
//用上面的设定新建一个进程
Process process = new Process();
process.StartInfo = processStartInfo;
//以下是输出 output 或者 error msg
if (processStarted)
{
    //Get the output stream
    outputReader = process.StandardOutput;
    errorReader = process.StandardError;
    process.WaitForExit();//这局可能把人卡住

    //展示
    string displayText = "Output:" + Environment.NewLine;
    displayText += outputReader.ReadToEnd();
    displayText +="Error:" +  Environment.NewLine ;
    displayText += errorReader.ReadToEnd();
    txtResult.Text = displayText;
    
    //关闭stream
    if(outputReader != null)  outputReader.Close();
    if(errorReader != null)  errorReader.Close();
}
```



> 我一开始打算把cmd搬到我的winform里面（可以实时更新输出的那种），但是我搜了好久也没有可以拷贝的代码，而且获取输出并且贴到textbox中会有时产生莫名其妙的死循环，于是我便放弃了于是就选择了功能相同但是弹出窗口的了。



这个函数除了这些功能还可以做打开浏览器指定网页、打开文件夹等，是一个windows环境很常用的csharp函数了

```
//打开浏览器指定网页
private void openinbrowser(string link)
{
    string strCmdText;
    strCmdText = $"{link}";
    Process process = Process.Start(@"C:\Users\kasusa\AppData\Local\Google\Chrome\Application\Chrome.exe", strCmdText);
}

```

```
//打开文件夹
Process.Start("explorer.exe", @"c:\test");
```

对了，这里我同时说两个好用的string用法，他们分别是@和$:（语法糖)

```
@ 可以输出源字符串而不做转义，这对于string写文件目录很有用：
如果没有@ 系统会对\U \k \D \G 挨个转义，碰到转义失败的就报错了。
string a = @"C:\Users\kasusa\Documents\Gitee";

$ 可以快速的在一个字符串中插入一个变量而不需要用一堆的引号和加号
string b = "cake";
string c = $"i love eating {b}， and drink cola！";
```

