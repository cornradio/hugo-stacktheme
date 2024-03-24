+++
title = "传入参数ARGV"
description = ""
date = 2022-09-10T20:03:01+08:00
categories = [
  ""
]
tags = [
  ""
]
series = []
+++

# 传入参数

在使用linux命令的时候，很多命令都能传入参数比如 ls -l。

这次使用的例子是我之前写过的me_in_jandan.py，他的功能是通过爬虫爬去取jandan的某一个用户的所有发帖，并返回相关的链接。

但是这个用户名是写死在py脚本里面的，如果想要修改的话还要修改代码，不太方便，所以需要通过穿参数的方法可以直接临时更换要查询的用户名。

这里介绍py脚本、shell脚本、bat脚本的参数，非常简单但是是一个小知识点！



## python 命令行参数

```
if len(sys.argv) == 2:
    TARGET_USER_NAME = sys.argv[1] #传入的第一个参数，设置为用户名
```

对于python来说，一号是脚本文件名称（很合理），二号开始参数字符串，更好的例子可以看看下面的简单脚本和执行结果：

```
import sys
print(sys.argv)
```

```
kasusadeMBP:me_in_jandan $ python3 args.py v1 v2    
['args.py', 'v1', 'v2']
```



## shell参数(.sh文件)

```
echo $1
echo $2
```

```
kasusadeMBP:me_in_jandan $ ./a.sh v1 v2
v1
v2
```



## bat参数

```
echo %1
echo %2
```
