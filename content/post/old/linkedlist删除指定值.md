+++

title = "linkedlist删除指定值"
date = "2021-06-01"
author = "kasusa"
cover = ""
tags = ["csharp"]
description = "如何删除linked list中的指定值"
showFullContent = false

+++

info是我自己定义的一个类。

下面是如何删除linklist中指定item的办法。

```cs
LinkedList<info> infolist = new LinkedList<info>();

string todelete = "1";

info tmpitem = new info();
foreach (var item in infolist)
{
    if (item.no == todelete)
        tmpitem = item;
}
infolist.Remove(tmpitem);
```

