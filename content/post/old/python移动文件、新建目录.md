+++
title = "Python移动文件、新建目录"
description = ""
date = 2021-12-11T12:23:30+08:00
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

使用python移动文件和新建目录主要是用于大量的文档分类工作，以下是代码部分:

```python
import os #新建目录
import shutil #复制文件
# 新建一个文件夹out 然后把f.txt复制到out文件夹中：
# r字符串可以不需要写\\，对于windows目录操作比较实用
original = r'f.txt'
target = r'out\f.txt'

if not os.path.exists('out'):  #当文件已存在时，无法创建该文件所以需要先检查
    os.mkdir(r'out')
shutil.copyfile(original,target) #复制文件
```

下面来一个实用的例子，把一个文件夹中，文件名称包含了“xxx系统”的文件都放到指定文件夹中：

```python
mylist = os.listdir('文件目录') # 获取某个目录下的全部文件名称

for item in mylist:
    if item.__contains__('系统名称'):
        shutil.copy('文件目录' + '\\' + item, '输出目录' + "\\" +item )
```

它最大的实用性就在对于多个文件的自定义命名。很方便。
