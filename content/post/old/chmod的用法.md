+++
title = "chmod的用法"
description = ""
date = 2022-04-22T15:30:54+08:00
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

+++

# chmod的用法

今天我们有一节技术分享，讲的是linux的文件和权限，学到了点有用的。

然后由于我自己的一些思考，我就觉得比如我把自己写文件的权限去掉了，这个时候我为什么还能够通过chmod来修改这个文件的权限呢？搞了一会儿chmod搞懂了，分享一下：

## ls -l：看权限

![image](https://image.baidu.com/search/down?url=https://tva1.sinaimg.cn/large/006rgJELly1h1ijxlim8tj30r30c8gp2.jpg)

这个权限一般是这样的 `rwx rwx rwx` 写了三遍是因为它对应着三个家伙的权限，分别是用户（文件拥有者）、组（文件拥有者的朋友们）、还有其他人。

linux系统是由文件组成的，文件就像一个物品，他是有归属的，图中`me.txt`这个文件就是属于`k`的用户的。

属于k的意思就是，`k`可以对这个文件使用`chmod`指令来改变文件的权限，就像你可以决定你的东西是否让别人使用一样。

对于文件 r（read）、w（write）、x（Excute）都很好理解，但是目录呢？什么叫执行目录？下面这个表可以参考一下：

| **-** | **r**            | **w**              | **x**            |
| ----- | ---------------- | ------------------ | ---------------- |
| 文件  | 读到文件内容     | 修改文件内容       | 执行文件         |
| 目录  | 读目录下的文件名 | 修改目录下的文件名 | 进入该目录的权限 |

> 注意：要开放目录给任何人浏览时，应该至少也要给予 r-x的权限，w 权限不可随便给

看了这个表你就能感觉到，目录的权限指的是你能不能看到、修改目录里面的文件名，文件的权限是管文件里的东西（文件的具体内容啥的），懂了这个道理你上面的表也就没有必要记了。

## 修改文件所属 

修改文件所属就像物品的转让，但是只能由`root`强制执行……hhh

```
chgrp：修改文件所属用户组
chown：修改文件拥有者()

chgrp [-R] <用户组名称> <文件或目录>
	chown [-R] <账号名称:用户组名称>  <文件或目录>
	chown [-R] <账号名称>  <文件或目录>
```

## chmod

chmod：修改文件的权限

```
chmod [-R] xyz 文件或目录
(r:4  w:2  x:1)
chmod 777 file1
```

但是这种操作多不直观！整几个数字看起来虽然非常极客，但是真的很不人性化。我还是更喜欢这种方式：

```
chmod a=rwx hi.txt 

a=rwx 意为：all（所有人）=（权限变成）rwx（读写执行）
a/u/g/o (all/user/group/others)
=/+/-						   (设置权限、增加某些权限、减少某些权限)
```

```
k@VM-12-6-ubuntu:~$ ls -l
----rwx--- 1 k    k    0 Apr 22 15:24 hi.txt

k@VM-12-6-ubuntu:~$ chmod a=rwx hi.txt 

k@VM-12-6-ubuntu:~$ ls -l
-rwxrwxrwx 1 k    k    0 Apr 22 15:24 hi.txt
```

如果用这个方式，看起来直观又容易记忆。

附加： SUID：4   SGID：2   SBIT：1

比如你要给一个目录的权限本来是774，但是你要给他加上SGID的特殊模式，你就直接赋权限 `chmod 2774 dir1`

## 高级：SUID、SGID、SBIT

有时候在`ls -l`的时候，你还会看到`s`、`t`这种奇葩的字母，不知为何意，下面就为你解惑。

不废话版：

符号：s（set xxx ID）

- SUID - 执行二进制文件的时候短暂获取文件**所有者**的权限
- SGID - 执行二进制文件的时候短暂获取文件**所属组**的权限
- SGID - 在某目录下时候短暂获取目录**所属组**的权限

符号：t （sticky）

![SBIT](https://image.baidu.com/search/down?url=https://tva4.sinaimg.cn/large/006rgJELgy1h1ilajxmd0j30n403e3zt.jpg)

![image](https://image.baidu.com/search/down?url=https://tva3.sinaimg.cn/large/006rgJELgy1h1illlnlslj30rb03775m.jpg)

![image](https://image.baidu.com/search/down?url=https://tvax1.sinaimg.cn/large/006rgJELgy1h1ilhuem4sj30t902ot9k.jpg)

### SUID 

>    当 **s** **这个标志出现在文件拥有者的** **x** **权限上**时，例如刚刚提到的 /usr/bin/passwd 这个文件的权限状态:【-rwsr-xr-x】，此时就被称为 Set UID，简称为 SUID 的特殊权限。
>
> 基本上 SUID 有这样的限制与功能：
>
> - SUID 权限仅对二进制程序 ( binary program ) 有效，不能用在 shell 脚本上；
> - 执行者对于该程序需要具有 x 的可执行权限；
> - 本权限仅在执行该程序的过程中有效；
> - 执行者将具有该程序拥有者 ( owner ) 的权限。
>
> **举个例子：**
>
> ​     Linux 系统中，所有账号的密码都记录在 /etc/shadow 这个文件里面，这个文件的权限为:【---------- 1 root root】，意思是这个文件仅有 root 可读且仅有 root 可以强制写入而已。既然这个文件仅有 root 可以修改，那么我们一般账号用户能否自行修改自己的密码？一般用户当然可以修改自己的密码。
>
> ​    可是明明 /etc/shadow 就不能让一般用户去读写的，为什么一般用户还能够修改这个文件内的密码？这就是 SUID 的功能。
>
> 借由前面提到的功能说明，我们可以知道：
>
> 1.一般用户对于 /usr/bin/passwd 这个程序来说是具有 x 的权限，表示一般用户能执行 passwd；
>
> 2.passwd 的拥有者是 root 这个账号；
>
> 3.一般用户执行 passwd 的过程中，会【暂时】获得 root 的权限；
>
> 4./etc/shadow 就可以被一般用户所执行的 passwd 所修改。
>
> 
>
> ​    但如果一般用户使用 cat 去读取 /etc/shadow 时，它能够读取吗？因为 cat 不具有 SUID 的权限，所以一般用户执行【cat /etc/shadow】时，是不能读取 /etc/shadow 的。

### **SGID**

与 SUID 不同的是，**SGID** **可以针对文件或目录来设置**。

> 除了二进制程序之外，事实上 SGID 也能够用在目录中，这也是非常常见的一种用途。当一个目录设置了 SGID 的权限后，它将具有如下的功能：
>
> - 用户若对于此目录具有 r 与 x 的权限时，该用户能够进入此目录；
> - 用户在此目录下的有效用户组 (effective group) 将会变成该目录的用户组；
> - 用途：若用户在此目录下具有 w 的权限(可以新建文件)，则用户所建立的新文件，该新文件的用户组与此目录的用户组相同。

### **SBIT**

Sticky Bit ( SBIT ) 只针对目录有效

> SBIT 对于目录的作用是：
>
> - 当用户对于此目录具有 w、x 权限，即具有写入的权限；
> - 当用户在该目录下建立文件或目录时，仅有自己与 root 才有权力删除该文件。
>
> 举例:
>
> 我们的 /tmp 本身的权限是【drwxrwxrwt】，在这样的权限内容下，任何人都可以在 /tmp 内新增、修改文件，但仅有该文件或目录建立者与 root 能够删除自己的目录或文件。
