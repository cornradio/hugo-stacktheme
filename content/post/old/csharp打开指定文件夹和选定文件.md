+++

title = "csharp文件管理器、读取文件列表"
date = "2021-06-04"
author = "kasusa"
cover = ""
tags = ["csharp", "winform"]
description = "csharp打开文件管理器、选取文件、获取文件列表"
showFullContent = false

+++

打开文件夹和选择其中某一项

```csharp
private void openExplorer()
{
  string FilePath = Directory.GetCurrentDirectory();
  //打开文件夹并选中文件
  System.Diagnostics.Process.Start("Explorer", "/select," + FilePath + "\\" + "infolist.xml"); 
  //仅打开文件夹
  System.Diagnostics.Process.Start(FilePath);
}
```

读取某位置的指定后缀文件（列表），把名字存入combobox

```cs
//读取xml文件，填充combobox列表
public void getCombobox()
{
  comboBox1.Items.Clear();
//获取当前程序目录，获取所有xml文件绝对地址
  var files = Directory
    .GetFiles(Directory.GetCurrentDirectory(), "*.xml");
  //提取路径地址+/为了在后面把完整路径剔除
  string pathstr = Directory.GetCurrentDirectory()+"\\" ;
  int count = 0;
  foreach (var file in files)
  {
    //逐个把文件名放在combox中
    comboBox1.Items.Add(file.ToString().Replace(pathstr, ""));
    count++;
  }
  toolStripStatusLabel1.Text = $"读取到了【{count}】个xml文件。";
}

```

