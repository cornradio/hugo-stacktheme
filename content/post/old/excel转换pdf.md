+++
title = "Excel转换pdf"
description = ""
date = 2022-01-09T20:44:16+08:00
featured = false
draft = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "csharp","excel","PDF"
]
series = []
images = []

+++

这个函数可是费我老大劲了。

我可以保证，你无法在除了我发的——互联网任何一个地方找到这段代码。

使用的dll需要在安装了ms office的电脑上才能找到。

## 例子

```cs
//测试：转换为pdf
//在下面两个文件夹中找到 office 和 Microsoft.Office.Interop.Excel 两个dll
//C:\Windows\assembly\GAC_MSIL\Microsoft.Office.Interop.Excel\15.0.0.0__71e9bce111e9429c
//C:\Windows\assembly\GAC_MSIL\office\15.0.0.0__71e9bce111e9429c
private void button2_Click(object sender, EventArgs e)
{
    string filePath  = Environment.GetFolderPath(Environment.SpecialFolder.Desktop) + @"\Sample\wb.xlsx";
    string filePath2 = Environment.GetFolderPath(Environment.SpecialFolder.Desktop) + @"\Sample\wb.pdf";
    //List<string> files = new List<string>();
    //files.Add(filePath);
    Application application = new ApplicationClass();
    Workbook workbook = application.Workbooks.Open(filePath);
    workbook.ExportAsFixedFormat(XlFixedFormatType.xlTypePDF, filePath2, XlFixedFormatQuality.xlQualityStandard);
}
```

## 封装函数
```cs
public static void ConvertExcelToPDF(string sourcePath,string targetPath)
{
    Application application ;
    Workbook workbook ;
    try
    {
        application = new ApplicationClass();
        workbook = application.Workbooks.Open(sourcePath);
        workbook.ExportAsFixedFormat(XlFixedFormatType.xlTypePDF, targetPath, XlFixedFormatQuality.xlQualityStandard);
    }
    catch (Exception e)
    {
        ConsoleWriter.WriteErrorMessage("pdf输出 出错");
    }
}

```

那个叫做Spire的库可真是害惨我了。

Spire.XLS提供了很简单的例子，但是报错却非常非常的诡异。网上没有任何相关信息。

一看实现，好家伙，一堆`goto`

而且Spire还有不支持excel默认编码的问题`IBM 472` 

Spire在读取xlsx的时候报编码错误可以用`nuget`安装这个包来解决：

```
system.text.encoding.codepages
```

```
Encoding.RegisterProvider(CodePagesEncodingProvider.Instance);//增加编码支持。
```

Spire 我用来调整了一下表格列宽什么的，还是挺好用的，但是它内部肯定有问题。另存为PDF根本就是一坨屎。



[更多代码可以参考我的github](https://github.com/kasusa/ExcelSignToPDF)



