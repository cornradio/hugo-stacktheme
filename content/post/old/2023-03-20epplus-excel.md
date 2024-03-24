+++
title = "csharp 使用 Epplus 读写 excel表格"
description = "epplus是一个读写xlsx的csharp库"
date = 2023-07-11T16:33:34+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "csharp","excel"
]
series = []
images = []
+++
> 📅 2023-03-20 首发
> 
> 📅 2023-07-11 更新 - 从excel反序列化到内存 //

epplus是一个读写excel表格的 csharp库。[官网教程](https://epplussoftware.com/zh/Developers/ ) 

官方教程中使用 using 语法，我不喜欢多层级括号，[using不使用多层级括号参考](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/using-statement)


## 基础（写文件）
> 基础的方法我已经提取成了库文件 myExcel.cs 放在最后面：
> 包括读取excel、新建excel、新建sheet、修改cell内容、保存collectionx
> 

### 新建excel

传入 string 路径读取excel，如果传入的是空的就新建一个。

```cs
using var package = new ExcelPackage(@"myWorkbook.xlsx");
```

### 新建sheet

```cs
var sheet = package.Workbook.Worksheets.Add("My Sheet");
```

### 修改cell内容

修改指定名字的sheet

```cs
package.Workbook.Worksheets["Worksheet1"].Cells["A3"].Formula = "SUM(A1:A2)"
```

修改上面提到的sheet，支持excel语法，框选范围,
比如单个单元格、长方形范围、A列到B列等

```cs
sheet.Cells["A1"].Value = "Hello World!";
sheet.Cells["A2:E8"].Value = "xxx";
worksheet.Cells["A:B"].Value = "xxx";
```

### 修改style

主要包括修改数字格式、修改字体

```cs
worksheet.Cells["A1:B3,D1:E57"].Style.NumberFormat.Format = "#,##0"; 
//Sets the numberformat for a range containing two addresses.
worksheet.Cells["A:B"].Style.Font.Bold = true; //Sets font-bold to true for column A & B
worksheet.Cells["1:1,A:A,C3"].Style.Font.Bold = true; //Sets font-bold to true for row 1,column A and cell C3
worksheet.Cells["A:XFD"].Style.Font.Name = "Arial"; //Sets font to Arial for all cells in a worksheet.
worksheet.Cells.Style.Font.Name = "Arial"; //This is equal to the above.
```

### 保存

例如保存到 `桌面/out/myWorkbook.xlsx`

```cs
var desktopurl = Environment.GetFolderPath(Environment.SpecialFolder.Desktop) + '/' + "out" + '/';
workbook.SaveAs(@$"{desktopurl}myWorkbook.xlsx")
```

## 序列化和反序列化
支持从下面的中导入

* `csv`（其他的导出数据）

* `List<T>`（内存中的数据）

* `datatable`（数据库中的数据）

获取数据然后变成 `ExcelPackage`

### 把collection（`List<T>`） 存储到 excel
首先创建一个class，并生成一些实例，保存到一个列表中。

```cs
public class MyClass
{
    public string Id { get; set; }
    public string Name { get; set; }
    public int Number { get; set; }
}
```

```cs
var items = new List<MyClass>()
{
    new MyClass(){ Id = "123", Name = "Item 1", Number = 3},
    new MyClass(){ Id = "456", Name = "Item 2", Number = 6}
};
```

然后把它变成一个`ExcelPackage`，这里例如以`C1`为左上角顶点。

```cs
using (var pck = new ExcelPackage())
{
    var sheet = pck.Workbook.Worksheets.Add("sheet");
    var range = sheet.Cells["C1"].LoadFromCollection(items,c => {c.PrintHeaders = true;});
}
```

可以打印表头，默认不打印
可以设置主题，比如弄一额黑色主题
可以设置表头，比如只要id、name两列

```cs
var tableRange = sheet.Cells["C1"].LoadFromCollection(items, c => {
    c.PrintHeaders = true;
    c.TableStyle = TableStyles.Dark1;
    c.Members = new MemberInfo[]
    {
        t.GetProperty("Id"), 
        t.GetProperty("Name")
    }
});
```

###  反序列化excel到内存


可以把指定sheet 的数据反序列化到内存中（表格数据 -> `list<Vulnerability>`）。

> 为了正常识别，需要在excel中顶着左上角开始写表格。
> 
> 常见错误是表格中有空行，会造成读取失败，程序闪退。 所以一定要保证xlsx内容正确。

#### 例表（漏洞名称和简述）

漏洞名称|漏洞类型|	漏洞危害|	修复方案|
--- | --- | --- | ---
SQL注入|注入攻击|数据泄露、数据篡改|使用参数化查询或ORM框架，避免直接拼接SQL语句
跨站脚本攻击（XSS）|跨站攻击|窃取用户Cookie、会话劫持|过滤特殊字符，使用CSP、HttpOnly等安全头部，对用户输入进行转义
文件包含漏洞|访问控制|读取任意文件、执行任意命令|对用户输入的路径进行限制，并增加白名单过滤，避免使用动态文件包含
未授权访问漏洞|访问控制|窃取数据、篡改数据|对所有敏感操作进行身份验证与授权，禁止使用默认密码
 

####  创建数据结构class 
我创建了  `Vulnerability` class，包含了漏洞的信息。

```cs
public class Vulnerability
{
    public string Name { get; set; } // 漏洞名称
    public string Type { get; set; }// 漏洞类型
    public string Impact { get; set; }// 漏洞危害
    public string Fix { get; set; }// 修复方案
}
```

####  遍历excel，把数据存储到list中

注释位置的内容按照需要修改即可。
`//修改下面，改成自己的类，赋值自己的数据。`

```cs

public list<Vulnerability> vulDB_list ; //数据会存储到这个外部list中

/// <summary>
/// 从指定路径初始化漏洞数据库，将漏洞信息添加到vulDB_list中
/// </summary>
/// <param name="filePath"></param>
private void vulDB_init(String filePath = "漏洞数据库.xlsx")
{
    var 漏洞数据库xls = new myExcel(filePath);//使用了我的myExcel 库，获取package
    var worksheet = 漏洞数据库xls.ReadSheet("Sheet1");//使用了我的myExcel 库，获取sheet
    if (worksheet != null)
    {
        for (int i = worksheet.Dimension.Start.Row + 1; i <= worksheet.Dimension.End.Row; i++)
        {
            //修改下面，改成自己的类，赋值自己的数据。
            vulDB_list.Add(new Vulnerability()
            {
                Type = worksheet.Cells[i, 1].Value.ToString(),
                Name = worksheet.Cells[i, 2].Value.ToString(),
                Impact = worksheet.Cells[i, 3].Value.ToString(),
                Fix = worksheet.Cells[i, 4].Value.ToString()
            });
        }
    }
    if (vulDB_list.Count == 0)
    {
        ConsoleWriter.WriteRed("漏洞数据库为空，请检查漏洞数据库文件是否存在,请放在和exe同一目录下");
    }
}
```


## ExportData
支持把`ExcelPackage`保存成csv、Datatable、json、html格式。

## Encryption
可以给文件加密！

```cs
//Set a password for the workbookprotection 
workbook.Protection.SetPassword("EPPlus");
```


## myExcel.cs
这个类库可以方便我以后使用！
```
using System;
using OfficeOpenXml;

namespace reformat_report_console.mylibs
{
    public class myExcel
    {
        ExcelPackage package;
        ExcelWorksheets? worksheets;

        /// <summary>
        /// 输入url，读取 excel，返回 ExcelPackage
        /// </summary>
        /// <param name="filepath"></param>
        public myExcel(string filepath)
        {
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;//设置为非商业使用
            this.package = new ExcelPackage(filepath);//读取文件
            this.worksheets = package.Workbook.Worksheets;//获取工作表
            if (worksheets.Count == 0) ConsoleWriter.Writedebug($"这是一个空excel:{filepath}");	//如果工作表为空，输出提示
        }
        // 读取excel指定sheet到内存
        public ExcelWorksheet ReadSheet(string sheetname)
        {
            ExcelWorksheet sheet = package.Workbook.Worksheets[sheetname];
            return sheet;
        }
        /// <summary>
        /// 添加一个sheet（输入sheet名）
        /// </summary>
        /// <param name="sheetname"></param>
        /// <returns></returns>
        public ExcelWorksheet Addsheet(string sheetname)
        {
            ExcelWorksheet sheet = package.Workbook.Worksheets.Add(sheetname);
            return sheet;
        }
        /// <summary>
        /// 写入collection数据 到指定sheet
        /// 同时展示表头，表头是类的属性名
        /// </summary>
        /// <param name="sheet"></param>
        /// <param name="items"></param>
        /// <typeparam name="T"></typeparam>
        public void WriteCollectionToSheet<T>(ExcelWorksheet sheet, IEnumerable<T> items)
        {
            var range = sheet.Cells["A1"].LoadFromCollection(items, c => c.PrintHeaders = true);
        }

        /// <summary>
        /// 检查out文件夹是否存在，out用于输出
        /// </summary>
        /// <returns></returns>
        private string checkoutdir()//检查out文件夹是否存在，不存在则创建
        {
            string outpath = Environment.GetFolderPath(Environment.SpecialFolder.Desktop) + '/' + "out";
            if (!Directory.Exists(outpath))
                Directory.CreateDirectory(outpath);
            return outpath;
        }
        /// <summary>
        /// excel保存到桌面out文件夹下
        /// 默认指定保存到 out/finlename
        /// 否则以filename为路径保存
        /// </summary>
        /// <param name="filename">xxx.xlsx</param>
        /// <param name="savetype">url / file</param>
        public void Save(string filename, string savetype = "file")
        {
            try
            {
                if (savetype.Equals("file"))//file类型保存，保存到out文件夹下
                {
                    string savepath = checkoutdir() + "/" + filename;//获得保存路径，如果已经存在则提示是否保存以防工作丢失
                    if (File.Exists(savepath))
                    {
                        ConsoleWriter.WriteCyan($"已经存在相同文件，{filename}，确认要覆盖？(Y/n)");
                        if (Console.ReadLine() == "n")
                        {
                            Console.WriteLine("已经取消保存");
                            return;
                        }
                        else
                        {
                            Console.WriteLine("已经覆盖保存");
                        }
                    }
                    var desktopurl = Environment.GetFolderPath(Environment.SpecialFolder.Desktop) + '/' + "out" + '/';
                    this.package.SaveAs(desktopurl + filename);
                    ConsoleWriter.WriteGreen("[ok] 保存到桌面out文件夹/" + filename);
                }
                else if (savetype.Equals("url"))//url类型保存，保存到指定路径
                {
                    this.package.SaveAs(filename);
                    ConsoleWriter.WriteGreen("[ok] 保存到:" + filename);
                }
            }
            catch (Exception e)
            {
                ConsoleWriter.WriteRed($"[-] 无法保存：{e}");
            }
        }

        
    }
}

```