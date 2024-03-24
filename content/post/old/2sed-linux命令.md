+++
title = "sed Linux命令"
description = ""
date = 2022-12-06T20:14:59+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "linux"
]
series = []
images = []
+++


参考链接：
https://www.youtube.com/watch?v=nXLnx8ncZyE

# sed命令
sed据我了解是linux中用于替换的一个命令。

# 使用方法

仅替换第一次出现的：
```
# 把a.txt中的 abc 换成 def 并打印出来。
sed 's/abc/def/' a.txt

# 把a.txt中的 abc 换成 def ，替换到源文件内
sed -i 's/abc/def/' a.txt

# 使用/之外的分隔符也可以搜索,只要你把分隔符放在s后面，比如这里用英文点号
sed -i 's.abc.def.' a.txt

```

替换所有出现的：
```
# 把a.txt中的 abc 换成 def 并打印出来。
sed 's/abc/def/g' a.txt
```