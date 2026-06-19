---
title: WinTranslator ，按下快捷键，立即用ai分析选中文字 # 标题
slug: WinTranslator # url(注释掉 和标题相同)
image: https://wcp.cornradio.org/images/WinTranslator/image-4.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2026-06-19 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fwintranslator&label=&icon=check-all&color=%23198754)

b站视频： https://www.bilibili.com/video/BV1xnji6pEz
github: https://github.com/cornradio/WinTranslator


## 写这个工具的理由：

昨天在小众论坛上看到一篇关于翻译软件的帖子，觉得不错，但对方只发了截图，没把软件放出来。于是我就想自己写一个。  

当时就想到应该用AI来做翻译，因为AI特别适合这个任务。  

写翻译工具的过程中，我加了一个润色功能。因为我平时经常让AI帮我润色语音输入的语句。  

加了润色功能之后，我发现这其实是一个非常实用的基础流程：选中文本 → 按快捷键 → 调用预设的prompt → AI分析文本 → 返回结果。这个流程有无限的扩展可能。  

于是就做成了现在这个工具。虽然名字还是叫win translator，但它的功能已经不限于翻译了。

---

- 关于如何写工具：不作详细讨论
  - 使用的并非最先进模型
  - 实际使用过程中较为繁琐
  - 最终功能已完全实现

- 关于技术栈：建议自行分析
  - 直接拉取项目代码
  - 借助AI进行分析
  - 不再具体阐述，认为无实际意义


---

## 截图展示：

### 翻译文本（自动识别中英文）：

![alt text](https://wcp.cornradio.org/images/WinTranslator/image.png)

### 优化表达（可以同时内置多种AI润色模板）：

![alt text](https://wcp.cornradio.org/images/WinTranslator/image-1.png)

### ai查询：
这个是我自己后加的一个小功能。
你可以照抄我的模板

```
帮我解释下面内容，回复不要超过1000字。
{text}
```

![alt text](https://wcp.cornradio.org/images/WinTranslator/image-2.png)


### 强大的自定义模板：
你可以添加任意数量的模板，设置不同的快捷键，满足不同的需求。  
也可以不设置快捷键，直接右键点击trayicon使用相关模板。

![alt text](https://wcp.cornradio.org/images/WinTranslator/image-3.png)