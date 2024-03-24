+++
title = "Tar的用法、常见的linux压缩解包方法"
description = ""
date = 2022-05-22T16:45:55+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "linux","tar"
]
series = []
images = []

+++

# 常见的linux 压缩解包方法

```
gzip xxx
gunzip xxx

tar zcvf 压缩文件名 压缩文件
tar zxvf 解压包名 解压文件

tar jcvf renwolesshel.tar.bz2 打包
tar jxvf renwolesshel.tar.bz2 解压

zip -q a.zip a.txt 
unzip a.zip 
  -q “安静模式”
```
# tar的用法

## 打包	

打包（多个文件）：

```bash
tar -cf my.tar 1.txt 2.txt 3.txt
```

打包（文件夹）：

```bash
tar -cf dir1.tar dir1
```

---

## 看包	

看包/预览包内容：

```bash
tar -tvf dir1.tar
```

---

## 解包	

解包：会自动解压到当前目录的同名文件夹下面

```bash
tar -xf dir1.tar
```

解包（到指定的位置）：解压后会在`dir2`里面看到一个`dir1`

```bash
tar -xf dir1.tar -C dir2/
```

# tar与文件类型

一般来说 `.tar` 就是我们说的打包的包了，用上述命令就可以操作。

常见 `.tar.gz` 格式，它是打包后又进行了压缩。可以使用 `-zxf` 来解压。

需要根据自己需要来决定要不要开`-v` ，不开的话，解压或者打包的时候系统看起来就像卡住了一样。

# 常用参数解释

- c create 创建
- x extract 解包
- v verbose 显示更多废话
- f file=ARCHIVE 要操作的对象放在f后面
- z zip 压缩功能

## 官方的话

> GNU 'tar' saves many files together into a single tape or disk archive, and can
> restore individual files from the archive.

```
Examples:
  tar -cf archive.tar foo bar  # Create archive.tar from files foo and bar.
  tar -tvf archive.tar         # List all files in archive.tar verbosely.
  tar -xf archive.tar          # Extract all files from archive.tar.
```

