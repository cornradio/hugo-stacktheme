+++

title = "word小工具开发"
description = ""
date = 2022-03-31T15:44:16+08:00
featured = false
draft = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "c#","word","开发"
]
series = []
images = []

+++

> 本期是发到公众号上的技术分享，分享的内容就是之前我的Docx相关东东，但是本篇除了介绍代码方便、会更加全面的讲解程序搭建的思路、以及myutil（我写的关于Docx的库）的使用。

# word小工具开发

## 前情提要

自从去年9月份至今，我已经做过很多的小工具了，从最开始的完全不涉及文档操作，到丰富的docx查询编辑，积累了不少的经验，如果你也有一些点子、想开发一些小程序简化自己的工作（特别是和word操作相关的），那么本文会对你有些许帮助！

## 信心

首先我们不要对开发这件事情抱有很大的抵触心理，不要认为这是一件很难的事情。

如果是一个学习过C语言课程的人，那么他上手会是很简单的。

如果是一个学过桌面程序开发的人，那么他应该可以秒上手！

本文主要使用的编程语言是C#，相对于python他有如下优点：

1. 拖拽式的界面设计非常简便
2. 少量信息的存储甚至不需要学习操作文件
3. C#操作Docx的库相对于python来说更加好用，且有丰富的官方例子（python-docx库会存在有无法读取到某些表或者段落、无法正常修改页眉内容等问题）

一般来说在思路清晰清晰的，根据功能复制程度、实现难度区别，开发时间应该是 1天~2天，相对于后续他为你提供的便利来说，真的是“磨刀不误砍柴工”。

## 主要原子功能

- 多个文件的选择和排除
- word文件的读取
- word文件的段落内容搜索
- word文件的表格内容搜索
- word内容的批量替换
- 少量数据的存储
- 字符串操作

## 例子“生成《出报告申请》”介绍

> ​	首先我会讲解一下这个程序的使用方法，通过这个真实的例子来分解程序的制作过程和开发思路

**使用方法：**

1. 报告拖放到textbox内（自动获取路径）
2. 通过自动模式/手动模式进行出报告申请的生成
3. 手动输入项目经理、成员
4. 检查输出是否有误 —— 完成

![image](https://tva2.sinaimg.cn/large/006rgJELly1h0rqww221gj30aw07q75f.jpg)

如上图所示，本程序有两种信息输入方式

- 从报告中读取
- 手工录入

![image](https://tva1.sinaimg.cn/large/006rgJELly1h0rqvro6gfj30dg0bwabq.jpg)

上图则是从报告中提取到的数据展示，展示后还需要手动输入“我方人员”，因为这些内容无法从源文件中读取到。

最后生成的成品文件则会保存到桌面指定的文件夹中（由于有敏感信息不做展示）。

## 界面设计

![image](https://tvax4.sinaimg.cn/large/006rgJELly1h0rr4lb1msj30hq0hkjz6.jpg)

对于不同功能的应用，要活用`radiobutton`、`listbox`等控件简化开发流程和用户的操作门槛，虽然界面可能看起来有些许“过时”，但是诸如`treeview`、`checkbox`、`radiobutton`、`listbox`等都是微软默认提供且非常强大且易用的控件。



同时在界面展示也要做的合理，如锚点的设置、按钮的摆放等

- 对于有大量内容的中心控件（如上图中的文件选取栏），推荐设置就是上下左右都配置锚点，这样用户在使用的时候可以通过手工把窗口拉大的方式来让选取栏变大，从而方便操作；

![image](https://tvax2.sinaimg.cn/large/006rgJELly1h0rr8bg656j30cb0420te.jpg)

- 对于底部的按钮则应该选择向下锚点，否则用户将窗体放大的时候就会变成这个样子

![image](https://tvax2.sinaimg.cn/large/006rgJELly1h0rrdstb3aj30ox0lfwhj.jpg)



## 程序思路

一个程序的开发可以简单的分成这三个步骤：

1. 需求的分析和程序开发可行性判断
2. 程序开发
3. 进行一些测试确保程序的可用性和稳定性

### 需求的分析和程序开发可行性判断

首先想让机器帮自己做某件麻烦事、或者是某些事情让机器做更好更快，这些想到的电子就是所谓的需求了。

如果产生了一个点子，作为程序的开发人员首先就要大致的思考一下怎么样把这个点子变成现实——用什么方式、用什么现在自己会的技术来做这件事。

从上面这个小程序的角度来看，脑内出现的过程是：

```
从报告中提取出信息 → 把信息存储到字典中 → 将字典中的对应字符串替换到新文件中 → 完成！
```

作为个人开发者，如果某些功能要实现可能需要耗费非常多的时间、精力，或者根本想不到实现的办法，那么可以认为开发可行性是不佳的，可以考虑放弃这个点子。

### 程序开发

1. 明确思路，制定操作LIST如：xxx → xxx (较小的项目可以略过这步)
2. 通过搜索、表格定位等方式用程序获取所需数据
3. 根据需要替换的位置制作模板
4. 逐一实现
5. 通过实际使用等方式进行测试

写一个大号的程序经常会有无从下手的感觉，所以第一个任务是把任务分成最小的“分子”。

如下图是另一个程序的操作LIST，它确实很有用，可以清晰的看到是否有遗漏，以及完成了哪些部分，可以对自己的进度有一个大概的掌握，后期还可以用于程序的功能描述。

这里使用的是markdown语法，对于每一个操作，如果实现了就在左边打一个x，如果没有则是空白的。

![image](https://tva1.sinaimg.cn/large/006rgJELly1h0s4rja7inj310a0nuaqq.jpg)

### 语言和调用库文件

读取文件方面，我采用了Docx开源库，可以在[xceedsoftware/DocX:(github.com)](https://github.com/xceedsoftware/DocX)上下载。他速度很快，仅支持C#语言，同时官方提供了详细的文档，可以在[/Xceed.Words.NET.Examples (github.com)](https://github.com/xceedsoftware/DocX/tree/master/Xceed.Words.NET.Examples/Samples)下载实验。

在[ kasusa/archiver (github.com)](https://github.com/kasusa/archiver/blob/master/archiver/myutil.cs)有我编写一个实用库，注释较全，本文中会大量使用库中实现的函数。

至于支持python的docx库，我使用过他们一段时间，提供的支持不好，如页眉页脚无法轻易修改、部分存在的段落无法读取、多个相连的表格无法读取到后面的表格等问题，如果有人想要用python开发一个操作word的程序可以适度参考和避坑。

### 文件读入、结构理解

文件读入是指把整个docx文件读到内存中，变成一个可以操作的对象：

```csharp
//使用工具类“myuitl”一句话读取文件
//path为docx文件的目录
doc = new myutil(path);
```


```cs
public myutil(string str_path)
{
    …
    var document = DocX.Load(path);//读取document
    this.document = document;//document本体获取
    this.tables = document.Tables;//主要元素之一：表格
    this.Paragraphs = document.Paragraphs;//主要元素之一：段落
    …  
}
```

一个word文件被读取之后，主要可以操作的部分分为三块：

- 段落（paragraph）

  - 段落在文档中是以类似链表的方式存储。

  - 获取的结果是`paragraph`对象，它存储段落内容字符串、段落的样式（如字体、对其格式、字号等）。

  - ```csharp
    //获取段落的文字内容
    string a = document.Paragraphs[0].Text;
    //调整段落为两端对齐
    document.Paragraphs[0].Alignment = Alignment.both;
    //调整颜色
    document.Paragraphs[0].Color(Color.Red);
    ```

- 表格（tables）

  - 表格在文档中是以类似链表的方式存储。

  - 表格的访问按照行、列进行，如果要访问指定表格，需要知道表格的索引、单元格相对于表格所在的行、列。

  - 每个单元格中可以包含多个段落，对于单元格的内容提取其中包含的段落内容。

  - ```csharp
    //文章中 第一个表格 第一行 第二个单元格（第二列）的内容
    document.Tables[0].Rows[0].Cells[1].Paragraphs;
    //获取总列数
    document.Tables[0].ColumnCount;
    //还有更多如多个单元格融合、增加行/列等
    ```

- 图片（images）

  - 图片分为Pictures、Images
  - Images是真正的图片，如果你用zip打开word文件，可以发现存在一个文件夹放置所有图片的源文件
  - Pictures是图片在word文档中的一种“引用”，他引用了Images中的图片，并显示在word文档的指定位置上
  - ![image](https://tvax4.sinaimg.cn/large/006rgJELly1h0sv8sgajgj30le0ca43b.jpg)

### 段落搜索

段落的搜索是很必要的，我们毕竟不能直接根据段落的序号来获取数据，因为很多时候中间的段落数量是不确定的，所以绝对索引有很大的概率拿到错误的段落。

搜索可以：

- 直接搜索段落必然包含的内容来找到段落
- 搜索段落附近的章节标题，通过段落相对序号来获取附近位置的段落
- 对于会有多个搜索结果的，返回list，或者指定要求获得第几个搜索结果

```csharp
//列举一些实搜索现的例子
public string Find_Paragraph_for_text(string v,int count = 1)
public List<Paragraph> Find_Paragraph_for_plist( string v)
public List<int> Find_Paragraph_for_ilist( string v)
    
//用搜索的方式获取段落
 tmpstr = doc.Find_Paragraph_for_text("本报告记录编号：");
//用搜索的方式获取段落,附加找到的个数,下方例子为第二个
tmpstr = doc.Find_Paragraph_for_text("记录编号：",2);
```

```cs
foreach (var p in document.Paragraphs)
{
    if (p.Text.Contains(v))
    {
        //Console.WriteLine("【找到:】" + p.Text + Environment.NewLine);
        return p;
    }
}
return null;
```

### 表格搜索

![image](https://tvax3.sinaimg.cn/large/006rgJELly1h0sy8718i9j30ux07rq4w.jpg)

![image](https://tva4.sinaimg.cn/large/006rgJELly1h0syiq0z24j30lc02oglw.jpg)

表格搜索功能是独创的，原理如下：

将表格第一行的内容字符串化，如“被测对象”、“序号机房名称物理位置重要程度备注”。

```csharp
//搜索表头为“被测对象”
var  table = findTableList("被测对象")[0];
//提供表格、行索引（row）、行内的单元格索引（cell),获取指定单元格内容
string text = table_Get_cell_text(table, 0, 1);
```

表格搜索的实现如下

```csharp
public List<Table> findTableList(string v1)
{
    v1 = v1.Replace(" ", "").Replace("\t", "");
    List<Table> tlist = new List<Table>();
    //Console.WriteLine("开始寻找表头是 :"+v1+ "的表格");
    for (int i = 0; i < tables.Count; i++)
    {
        string rowstring = "";
        for (int j = 0; j < tables[i].ColumnCount; j++)
        {
            rowstring += cell_get_text(table_Get_cell(tables[i], 0, j));
        }
        if (rowstring== v1)
        {
            //Console.WriteLine("找到了table"+i);
            tlist.Add(tables[i]);
        }
    }
    ConsoleWriter.Writehiddeninfo("找到table个数：" + tlist.Count);
    return tlist;
}
```

### 内容处理

能获取到的内容均以段落为最小单位，获取到了段落之后，由于段落的内容可能很多，不能直接使用，我们需要对其进行修改、删减、或者提取。

- 直接摘取整段
- 截取部分内容 （substring）
- 提取有用的固定格式内容（regex）

```csharp
//获取的内容 本报告记录编号：P2022XXXXX-GB01 ， 需要的部分是P2022XXXXX
 string a = doc.Find_Paragraph_for_text("本报告记录编号"); 
//本报告记录编号：P2022XXXXX-GB01
//从序号8开始，取长度为10的字符串
a = a.Substring(8,10); 
textBoxlog.Text = a;
```

如提取“测评准备过程的最后一天”时，因为存在多种书写格式、日期长短不一，需要使用正则表达式来提取内容、并且进行处理。

```
//多种情况例子
1、2021年12月28日～2021年12月29日，测评准备过程。
1、2021年12月28日～12月29日，测评准备过程。
1、2021年1月9日，测评准备过程。
```


```csharp
private string date_process(string a)
{
    //提取日期（结束日期）
    ConsoleWriter.WriteCyan("在字符串中寻找日期：" + a);

    string patternA = @"\d\d\d\d年(\d)*月(\d)*日";
    string patternB = @"(\d)*月(\d)*日";
    //如果获取的短日期个数为2，但是长日期仅有1个，那么就是如2021年12月1日～12月1日这种写法
    //如果长短日期都只有一个，那么就是2021年12月1日这种写法（只有一天之类的）

    int shortDcount = 0;
    int LongDcount = 0;

    Regex rg = new Regex(patternB);
    MatchCollection matchedShortDate = rg.Matches(a);
    shortDcount = matchedShortDate.Count;
    //Console.WriteLine("shortDcount" + shortDcount);
    rg = new Regex(patternA);
    MatchCollection matchedLongDate = rg.Matches(a);
    LongDcount = matchedLongDate.Count;
    //Console.WriteLine("LongDcount"+ LongDcount);

    if (shortDcount > LongDcount)
    {
        string year = matchedLongDate[LongDcount - 1].Value.Substring(0, 5);
        string MandD = matchedShortDate[shortDcount - 1].Value;
        a = year + MandD;
    }
    else if (shortDcount == LongDcount)
    {
        a = matchedLongDate[LongDcount - 1].Value;
    }
    Console.WriteLine(a);
    return a;
}
```

### 模板的制作和关键词替换

一般来说应用场景分为两种

- 修改源文件
- 从源文件中提取信息，制作其他文件

本次介绍的属于第二种，对于制作其他文件，首先需要制作一个模板。

![image](https://tvax3.sinaimg.cn/large/006rgJELly1h0t3f85uj1j30sj0fddjl.jpg)

然后我们只需要把【xxx公司】、【xxx系统】等内容替换为提取到的信息即可。

```csharp
//a是提取到的内容字符串，tempo是读进来的模板文档
a = doc.table_Get_cell_text(doc.tables[2], 1, 1);
str_公司 = a;
tempo.write_dictionary("xxx公司", a);

a = doc.table_Get_cell_text(doc.tables[1], 1, 1);
str_系统 = a;
tempo.write_dictionary("xxx系统", a);
...
 //写入
 tempo.ReplaceTextWithText_all();
//保存（myutil会默认保存到桌面 - out文件夹中）
tempo.save($"出报告申请_{str_公司}_{str_系统}.docx");
```

## 程序测试

程序编写完成后，需要进行测试，一般前几次的测试会发现很多的问题，大部分都很容易修复。

同时经过了自己的测试后，还可以吧自己的程序分享给他人使用、测试，因为不同人使用的习惯不同，让他人使用更容易发现一些自己发现不了的bug。

## 总结

如果你也想开发操作Docx相关的桌面程序，经过阅读上面的文章，应该已经可以了解其大概开发方法。同时也欢迎参考我的源码、使用我的库文件：[github/kasusa/archiver](https://github.com/kasusa/archiver)

