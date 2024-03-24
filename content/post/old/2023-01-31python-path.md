+++
title = "使用标准的path处理方法 (Python)"
description = ""
date = 2023-01-31T15:26:05+08:00
featured = false
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


标准方法可以兼容不同系统，并且有一定的容错性（比如在目录末尾写不写/）

* `os.path.split(path)` 分割路径和文件名
* `os.path.join()` 合并路径和文件名
* `os.path.dirname()` 方法可以获取目录名
* `os.path.basename()` 方法可以获取文件名
* `os.path.splitext()` 方法可以分离文件名和扩展名

<!--more-->
---


* `os.path.split(path)` 分割路径和文件名
* `os.path.join()` 合并路径和文件名

```python
import os

path = '/home/User/Desktop/file.txt'
os.path.split(path) 
```




    ('/home/User/Desktop', 'file.txt')




```python
path = '/home/User/Desktop'
file = 'file.txt'
os.path.join(path,file) 
```




    '/home/User/Desktop/file.txt'



`os.path.normpath()` 可以规范化路径，比如把多个/合并成一个，把.和..去掉


```python
path = '/home/User/Desktop//..//file.txt'
os.path.normpath(path)
```




    '/home/User/file.txt'



# 路径、文件名、扩展名

* `os.path.dirname()` 方法可以获取目录名
* `os.path.basename()` 方法可以获取文件名
 * `os.path.splitext()` 方法可以分离文件名和扩展名


```python
path = '/home/User/Desktop/file.txt'
os.path.dirname(path)
```




    '/home/User/Desktop'




```python
path = '/home/User/Desktop/file.txt'
os.path.basename(path)
```




    'file.txt'




```python
path = '/home/User/Desktop/file.txt'
os.path.splitext(path)
ext = os.path.splitext(path)[1]
```




    ('/home/User/Desktop/file', '.txt')


