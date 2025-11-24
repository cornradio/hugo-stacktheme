---
title: AI 编程软件大排名 # 标题
slug: vibecodingtools # url(注释掉 和标题相同)
image: https://i.imgur.com/fQz5oey.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2025-11-24 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

tags: # 只能在侧面看到的标签,会显示在文章的底部
    - AI
    - coding
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---


![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fvibecodingtools&label=&icon=check-all&color=%23198754)

本次介绍中只包含类似cursor形式的AI编程工具(IDE tools)~~~~，因为我认为这是最好用的 AI 编程工具形态。

首先介绍一下 AI 编程工具的用法：
- 给他提示词告诉他要做什么（指定编程语言模式功能内容等）
- 等待它生成代码
- 运行代码查看是否正确，不正确则修改提示词让它在现有的基础上继续有修改
- 重复以上步骤直到满意
但是他们也有一些普遍的缺点：
- 经常犯一些低级代码错误，比如说括号对不齐
- 引用一些根本不存在的虚空库
- 把所有的代码都喜欢放在一个文件，然后每次再全部重新读取，导致上下文非常长，非常的浪费token


# AI 编程工具大排名

ide级别，不考虑价格，仅考虑智商：
cursor > Qoder > antigravity 

考虑价格和轻度使用：
antigravity > Qoder > gitHub Copilot > cline 

## cursor
官网：https://cursor.com/  

>这是我最喜欢的 AI 编程工具之一，他是最早做这种模式的工具，据说他的创始人也赚了很多钱。
我一开始用的时候它的功能还比较单一，只能编辑的代码、还有自动创建文件之类的。然后也没有执行命令的能力。
现在它甚至会自动去编译命令,运行代码，查看错误信息然后自己debug。不过说实话我觉得他的审美还是比较糟糕的，一般的前端界面生成都比较丑。
我白嫖了他家好久，最后他们家增加了一些限制导致我白嫖不了了，然后我就弃坑了因为会员太贵了。

我还用这个软件做出了几个项目的。比如 [youlog](https://apps.apple.com/us/app/youlog/id6743986266)


价格参考：
![picture 0](https://i.imgur.com/pDj1AVP.png)  



## trae
官网：https://www.trae.ai/

>cursor 的仿品, 好像是字节跳动出的,功能和 cursor 差不多,但是界面更好看一些,而且价格也更便宜一些。还有比较没用的内置浏览器功能啥的。
有个问题它就是没有 claude 的大模型，可以说是非常笨了。
不过他的优点是你可以轻松的在闲鱼上买到他的账号能用一个月。

> 我给他排名很低是因为1.他太笨了 2.我之前买的账号但是用完一个月之后,他每天连送的额度都没有。你要打点什么代码一直让你在那排队排个一个小时都不给你用。

价格参考：
![picture 3](https://i.imgur.com/nwOJzLo.png)  

## antigravity
官网：https://antigravity.google/  
名字非常的奇怪，叫做反重力。

>这是 google 出的 AI 编程工具,非常非常的新，跟cursor相比有一些特立独行的功能，比如说他会先写一个 Markdown 的设计文档，然后再根据设计文档来写代码。并且你可以对这个 Markdown 进行备注，提要求，让他在开始行动之前有更好的参考。
使用起来比较费劲非得要挂梯子的TUN模式才行。
而且他使用的模型是他自己加的 gemini，目前gemini3也是大模型里面霸榜的存在。 
但是他这个有一个非常大的缺点，就是他的提示词你即使跟他说中文他给你回复也都是完全英语的。

价格参考：
免费（个人使用是免费的，但是使用的次数多了会有请求频率限制）
![picture 4](https://i.imgur.com/ALR8nqv.png)  

## qoder
官网：https://qoder.com/  
邀请码：https://qoder.com/referral?referral_code=I1HR3gB7h5TKqitqk23aA6s0aEXggqm8

> 阿里出的 AI 编程工具,我认为他比 trae 要聪明多了,默认模型是阿里的 Qwen 模型,中文支持比较好其他的工具基本都是纯英文界面。而且使用下来感觉非常聪明编程能力比较强。目前我使用它还没有到两周还在pro试用期内。点击邀请码送我credit，并且你也可以得到一些优惠。而且我感觉他的鼠标比较好看。名字也不像 trae 那么绕口

价格参考：
![picture 7](https://i.imgur.com/I0lulgI.png)  


## GitHub Copilot
官网：https://copilot.github.com/  
>它是以插件形式存在的,可以安装在 VSCode 里面使用。而且他还支持很多其他的平台。
它的功能和 cursor 差不多,但是没有 cursor 那么强大,总之就是感觉挺笨的, 不过它才是最早最早做 AI coding 补全功能的软件。
当时他还是收费的,现在他已经完全免费了。
不过它的功能也确实有点跟不上这些最激进的厂商了,在易用性方面上。虽然功能都有但是用起来就是很难受。
但是它还是有很多好用的点，比如说他可以补全 Markdown 然后你就是让他来帮你写笔记什么的。所以它也是我的 VSCode 的常驻插件之一。

价格参考：
免费

另外值得一提的是它的页面上可以免费的使用最新的 GPT 模型，作为交互式问答。
![(image.png) 1](https://i.imgur.com/2yJ76F8.png)  

## cline
官网：https://cline.bot/
>他是一个 VSCode 的集成插件,可以在 VSCode 里面直接使用 AI 来编程。就好像是开源版的 curson 一样,他本体是免费的,它主要是靠模型赚钱. 比如你可以选择使用它内置的模型它就会收费,你也可以选择免费的模型比如说你自己去用 gemini 的 key，日常完成轻度编程都不会超限的。重度使用的话那应该是需要付费的。

>关于怎么找到各种 AI 模型的key，可以使用cherrystudio，他这个工具里边会有配置模型的部分有教程告诉你去哪里找 key 还有链接。

价格参考：大部分时候是免费的。
![picture 8](https://i.imgur.com/4esqbrL.png)  

## 结语

有时候很庆幸我们生在这个 AI 的时代, 可以用 AI 来帮我们写代码,效率提升真的是非常大.甚至都不需要学习这个语言就可以使用它.比如youlog 这个项目,我完全不会 swift 语言,但是我用 AI 帮我写代码,然后我只需要负责调试和提需求就行了，虽然过程也有点痛苦的因为他总是写的东西不对，我最终的成果是满意的这个软件我也经常在使用。

对我个人来说，有 AI 工具之后我的 GitHub 上进行了一波小的项目爆发，因为我可以快速的用 AI 来帮我写代码，然后我只需要负责调试和提需求就行了。但是用 AI 开发的项目总的来说没有我之前自己开发的那些那么精细打磨，所以质量上还是有差距的。不过对于一些小工具和脚本来说已经足够了。

更多工具可以参考: https://github.com/filipecalegario/awesome-vibe-coding
