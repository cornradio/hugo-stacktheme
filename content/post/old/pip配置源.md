+++
title = "pip配置源"
description = ""
date = 2022-05-19T10:21:58+08:00
featured = false
draft = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "python"
]
series = []
images = []

+++

如何给pip配置代理；

# 将pip加入环境变量

可以通过下面的指令来查看自己的python安装在什么位置：

```shell
python -c "import sys; print(sys.executable)"
```

![image](https://image.baidu.com/search/down?url=https://tva1.sinaimg.cn/large/006rgJELly1h2di42uwzmj30ux0heah6.jpg)

应该会存在这样一个目录：`...\Python310\Scripts\`，里面会有好多pip相关的exe，我们要把这scripts文件夹加到`环境变量（user）`里面去就好了！

# pip 配置源

你需要进入用户目录，然后建立一个pip文件夹，例如这样：`C:\Users\kasusa\pip`

这个目录下，需要新建一个`pip.ini`文件

```ini
[global]
index-url = http://mirrors.cloud.tencent.com/pypi/simple/
[install]
trusted-host=mirrors.cloud.tencent.com
```

# 速度测试

![image](https://image.baidu.com/search/down?url=https://tva4.sinaimg.cn/large/006rgJELgy1h2dic1br59j30ux0dp49t.jpg)

好快呀！

