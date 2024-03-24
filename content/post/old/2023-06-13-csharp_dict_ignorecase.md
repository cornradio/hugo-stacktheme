+++
title = "csharp 字典 key 不区分大小写"
description = ""
date = 2023-06-13T10:41:53+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  ""
]
series = []
images = []
+++

Csharp_dict_ignorecase 
参考链接：

<https://www.tutorialspoint.com/case-insensitive-dictionary-in-chash?ranMID=49144&ranEAID=mP6UMnc5Ozo&ranSITEID=mP6UMnc5Ozo-0dXMNkfvS087.74Ygvbi7Q>

---

今天遇到一个问题，需要在C#中使用字典，但是字典的key是不区分大小写的，所以需要自己实现一个不区分大小写的字典，好在 c# 提供这项功能。


核心代码：

      Dictionary <string, int> dict = new Dictionary <string, int>(StringComparer.OrdinalIgnoreCase);

例子
```csharp
using System;
using System.Collections.Generic;
public class Program {
   public static void Main() {
      Dictionary <string, int> dict = new Dictionary <string, int>(StringComparer.OrdinalIgnoreCase);
      dict.Add("cricket", 1);
      dict.Add("football", 2);
      foreach (var val in dict) {
         Console.WriteLine(val.ToString());
      }
      // case insensitive dictionary i.e. "cricket" is equal to "CRICKET"
      Console.WriteLine(dict["cricket"]);
      Console.WriteLine(dict["CRICKET"]);
   }
}
```

输出

    1
    1