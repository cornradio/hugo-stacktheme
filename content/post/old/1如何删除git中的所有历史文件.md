+++
title = "如何删除git中的所有历史文件"
description = "111"
date = 2022-12-03T12:18:50+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "git"
]
series = []
images = []
+++

# 需要工具
- gitbash 用于快速操作
- githubDesktop 用于查看文件历史等

# 注意
此操作不可撤销，如果你的历史记录中有着不想要被删除的重要数据，请务必提前备份。

适用情况：清理git文件夹，让git每次clone下来更轻松。有可能项目中留存着一些没有用的垃圾，比如很大的图片、视频等。虽然目前已经删除。但这些内容实际上仍然保留在隐藏的`.git`文件夹中。

# 操作
1. 从git平台下拉目前的全部代码，删除原repo。
   > 删除在repo - settings - dangerzone最下面

    ![Imgur](https://i.imgur.com/a5zdkEs.png)
2. 进入本地repo，打开gitbash，执行下列指令
    ```
    rm -rf .git
    git init
    git add .
    git commit -m "init"
    git status
    ```
3. 使用github desktop检查是否有残留
  ![Imgur](https://i.imgur.com/X3R65UB.png)
4. 重新push repo到git平台

> 网上有一些很乱七八糟的方法，又要head，又要forcepush，又要orphan branch之类的，说实话我有些看不懂，我这个方式绝对简单又高效（粗暴rm -rf） 嘿嘿。
> 
## 其他提示
`insights - traffic` 可以查看到public项目的所有访问记录。数据为0的话不会展示；对于github博客来说，这里还是很有用的。
![Imgur](https://i.imgur.com/cVjIKyn.png)