+++

title = "winform适配dpi"
date = "2021-06-02"
author = "kasusa"
cover = ""
tags = ["csharp", "winform","dpi"]
keywords = ["", ""]
description = "winform程序应该高清的显示在笔记本上"

+++

[https://zhuanlan.zhihu.com/p/128588859](https://zhuanlan.zhihu.com/p/128588859)

在项目中添加一个：**应用程序清单文件**

在清单文件`app.manifest`的 `</assembly>` 标签下添加

```xml
  <application xmlns="urn:schemas-microsoft-com:asm.v3">
    <windowsSettings>
      <dpiAware xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">false</dpiAware>
      <longPathAware xmlns="http://schemas.microsoft.com/SMI/2016/WindowsSettings">true</longPathAware>
    </windowsSettings>
  </application>
```

参阅 https://docs.microsoft.com/windows/win32/fileio/maximum-file-path-limitation 

适配DPI之后，即便是电脑dpi为缩放的情况下， 仍然可以清晰的显示文字。

