+++
title = "把doc文件转换成docx"
description = ""
date = 2022-05-12T16:52:49+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "docx"
]
series = []
images = []

+++


在word中开启开发者模式，新建一个宏（快捷键 alt F11），使用下面的代码，然后双击运行宏。

会让你选择多个文件，然后系统会把他们都转换成docx文件，并保存到源文件夹！

> 如果你只是单纯吧doc后缀改成docx的话，会出现打不开、文件损坏的问题哦。

```vb
Sub doc2docx()  'doc文件转docx文件
Dim myDialog As FileDialog, oFile As Variant
Set myDialog = Application.FileDialog(msoFileDialogFilePicker)
With myDialog
        .Filters.Clear    '清除所有文件筛选器中的项目
        .Filters.Add "所有 WORD97-2003 文件", "*.doc", 1    '增加筛选器的项目为所有WORD97-2003文件
        .AllowMultiSelect = True    '允许多项选择
        If .Show = -1 Then    '确定
            For Each oFile In .SelectedItems    '在所有选取项目中循环
                With Documents.Open(oFile)
                .SaveAs FileName:=Replace(oFile, ".doc", ".docx"), FileFormat:=12
                .Close
                End With
            Next
        End If
End With
End Sub
```


