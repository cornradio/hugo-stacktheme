+++
title = "Excel黑色模式"
description = ""
date = 2022-06-22T19:03:01+08:00
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

OFFICE系列在最近增加了黑色模式支持，对于word来说非常好，他有做颜色映射，可以让一个本来是白色的文档变成黑色之后颜色也不显得奇怪。（word是一个“所见即所得”软件，为了保证打印效果和视觉效果一致，一直都不愿意加入黑色模式…

但是Excel就没有那么走运了，他的黑色模式只做了一半… 看看下图你就懂了，后面我用一种比较基础的方式教你怎么把他变成真正的“黑色模式”！
![image](https://image.baidu.com/search/down?url=https://tvax4.sinaimg.cn/large/006rgJELly1h3h8a26rooj30ub0i7gq8.jpg)


![image](https://image.baidu.com/search/down?url=https://tva3.sinaimg.cn/large/006rgJELly1h3h8cdw0kbj30uk0ihqal.jpg)

# 原理
本质上我们就是吧单元格颜色、文字颜色、线框颜色都修改掉。
缺点是影响打印，并且不是很自动化。
但是优点是你可以有非常高度的自定义效果！
- 选中全文
- 背景颜色
- 文本颜色
- 线框颜色

# 操作步骤
- 选中全文

- ![image](https://image.baidu.com/search/down?url=https://tvax2.sinaimg.cn/large/006rgJELly1h3h8drhru2j30ea0b641a.jpg)

- 背景颜色
- ![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/006rgJELly1h3h8e9ea2ij30bd0bx410.jpg)
- 文本颜色
- ![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/006rgJELly1h3h8er3dicj30do0cq41l.jpg)
- 线框颜色
- ![image](https://image.baidu.com/search/down?url=https://tvax1.sinaimg.cn/large/006rgJELly1h3h8fcbj9qj30nj0ry7ec.jpg)

# 用宏来操作

当然每个表格这么改一下,命都没了。

所以我还是推荐用宏来修改，一个表格点一下按钮就修改好了！

宏的话，自己录制比较好（更加安全也更加方便），但是你也可以用我的宏(是录制转换的，所以有很多没用的代码)：

```vb
Sub darkmode()
    Cells.Select
    With Selection.Interior
        .Pattern = xlSolid
        .PatternColorIndex = xlAutomatic
        .ThemeColor = xlThemeColorLight1
        .TintAndShade = 0.149998474074526
        .PatternTintAndShade = 0
    End With
    With Selection.Font
        .ThemeColor = xlThemeColorAccent1
        .TintAndShade = 0.799981688894314
    End With
    Cells.Select
    Selection.Borders(xlDiagonalDown).LineStyle = xlNone
    Selection.Borders(xlDiagonalUp).LineStyle = xlNone
    With Selection.Borders(xlEdgeLeft)
        .LineStyle = xlContinuous
        .ThemeColor = 2
        .TintAndShade = 0.349986266670736
        .Weight = xlThin
    End With
    With Selection.Borders(xlEdgeTop)
        .LineStyle = xlContinuous
        .ThemeColor = 2
        .TintAndShade = 0.349986266670736
        .Weight = xlThin
    End With
    With Selection.Borders(xlEdgeBottom)
        .LineStyle = xlContinuous
        .ThemeColor = 2
        .TintAndShade = 0.349986266670736
        .Weight = xlThin
    End With
    With Selection.Borders(xlEdgeRight)
        .LineStyle = xlContinuous
        .ThemeColor = 2
        .TintAndShade = 0.349986266670736
        .Weight = xlThin
    End With
    With Selection.Borders(xlInsideVertical)
        .LineStyle = xlContinuous
        .ThemeColor = 2
        .TintAndShade = 0.349986266670736
        .Weight = xlThin
    End With
    With Selection.Borders(xlInsideHorizontal)
        .LineStyle = xlContinuous
        .ThemeColor = 2
        .TintAndShade = 0.349986266670736
        .Weight = xlThin
    End With
End Sub
```
# 我的宏为什么不能运行？
微软最近的更新对宏进行了许多的限制（基于安全性原因和微软认为没啥人用这个东西），所以如果你想要运行宏，需要开一些设置：

1. 文件-选项-自定义功能区，勾选开启“开发工具功能区”
![image](https://image.baidu.com/search/down?url=https://tvax3.sinaimg.cn/large/006rgJELly1h3h8oj6zvwj30n80iuwks.jpg)

2. 文件 - 选项 - 信任中心 - 信任中心设置，然后勾选这样，然后重启软件。
![image](https://image.baidu.com/search/down?url=https://tvax3.sinaimg.cn/large/006rgJELly1h3h8lf9rg4j30mv0iitc0.jpg)

顺便玩了一会儿VisualBasic的开发界面，感觉上就像是一个上古时代的VisualStudio！
![image](https://image.baidu.com/search/down?url=https://tvax2.sinaimg.cn/large/006rgJELly1h3h8myxdd1j30vq0spgzm.jpg)

# 尾声
其实我当时想要编程的最主要原因就是感觉各种编辑器好酷啊，颜色花花的好看，黑色背景好酷！
虽然到目前位置也没去当一名全职开发，但是我对编辑器主题的爱永远不变！