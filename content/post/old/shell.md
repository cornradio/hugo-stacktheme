+++

title = "shell"
date = "2021-05-29"
author = "kasusa"
cover = ""
tags = ["ubuntu", "命令行"]
keywords = ["", ""]
description = "自学shell脚本"
showFullContent = false

+++


[菜鸟shell教程](https://www.runoob.com/linux/linux-shell-variable.html)

# Shell 命令脚本

Shell 脚本文件的名称可以任意，建议将.sh 后缀加上，以表示是一个脚本文件。

1. 创建脚本：`vim example.sh`
2. 写好脚本的内容（就是连串的shell语句）
3. 执行脚本：（后面的是参数）
    * ` bash example.sh`
    * `sh example.sh`
    * `./example.sh ` （一般会有权限不足的报错，升权限就好了）

## 简单的脚本
```sh
#!/bin/bash
#For Example BY linuxprobe.com
pwd
ls -al
```

在上面的这个 example.sh 脚本中实际上出现了三种不同的元素：
* 第一行的脚本声明（#!）用来告诉系统使用哪种 Shell 解释器来执行该脚本；
* 第二行的注释信息（#）是对脚本功能和某些命令的介绍信息，使得自己或他人在日后看到这个脚本内容时，可以快速知道该脚本的作用或一些警告信息；
* 第三、四行的可执行语句也就是我们平时执行的 Linux 命令了。



 

## 带参数的脚本-接收参数

如何运行带参数的脚本：
```
sh example.sh one two three four five six
```

脚本内容：

```sh
#!/bin/bash
echo "当前脚本名称为$0"
echo "总共有$#个参数，分别是$*。"
echo "第 1 个参数为$1，第 5 个为$5。"
```

~|~
---|---
$0 | 对应的是当前 Shell 脚本程序的名称，
$# | 对应的是总共有几个参数
$* | 对应的是所有位置的参数值
$? | 对应的是显示上一次命令的执行返回值
$1、$2、$3 | 则分别对应着第 N 个位置的参数值

## 带参数的脚本-判断用户的参数

运算符 | 作用
----|---
-d |测试文件是否为目录类型
-e |测试文件是否存在
-f |判断是否为一般文件
-r |测试当前用户是否有权限读取
-w |测试当前用户是否有权限写入
-x |测试当前用户是否有权限执行
---|0代表存在，否则不存在

例子： 下面使用文件测试语句来判断/etc/fstab 是否为一个目录类型的文件，然后通过 Shell 解释器的内设$?变量显示上一条命令执行后的返回值。
```
root@KASUSA-cloud:~# [ -f mydir ]
root@KASUSA-cloud:~# echo $?
1
```
## `&&`符号,`||`符号
> &&，它表示当前面的命令执行成功后才会执行它后面的命令

判断目录是否存在：
```sh
[ -e mydir ] && echo "Exist"
```
> 表示当前面的命令执行失败后才会执行它后面的命令，

因此可以用来结合系统环境变量 USER 来判断当前登录的用户是否为非管理员身份：
```sh
[ $USER = root ] || echo "user"
```
一个复杂一点的判断用户的例子：
```sh
 [ ! $USER = root ] && echo "user" || echo "root"
```

## 运算比较符
运算符 |作用
---|---
-eq | 是否等于
-ne | 是否不等于
-gt | 是否大于
-lt | 是否小于
-le | 是否等于或小于
-ge | 是否大于或等于

## 流程控制语句
### if 条件测试语句

![if](http://ww1.sinaimg.cn/large/0083vuQJly1gbmzfmixtrj30eh05t3z5.jpg)
![if else if](http://ww1.sinaimg.cn/large/0083vuQJly1gbmzhnsu8uj30g9074jsb.jpg)

### for 条件循环语句
![for1](http://ww1.sinaimg.cn/large/0083vuQJly1gbmzpen0wwj30ev05fmxp.jpg)

批量创建用户脚本：
创建 user.txt
```
vim users.txt
```

```
andy
barry
carl
duke
eric
george
```

创建脚本 Example.sh
```
 vim Example.sh
```

```sh
#!/bin/bash
read -p "Enter The Users Password : " PASSWD
for UNAME in `cat users.txt`
  do
  id $UNAME &> /dev/null
    if [ $? -eq 0 ]
      then
        echo "Already exists"
      else
        useradd $UNAME &> /dev/null
        echo "$PASSWD" | passwd --stdin $UNAME &> /dev/null
        if [ $? -eq 0 ]
          then
            echo "$UNAME , Create success"
          else
            echo "$UNAME , Create failure"
        fi
    fi
done

```
> 需要多说一句，/dev/null 是一个被称作 Linux 黑洞的文件，把输出信息重定向到这个文件等同于删除数据（类似于没有回收功能的垃圾箱），可以让用户的屏幕窗口保持简洁。

### while 条件循环语句
执行前并不确定最终执行的次数

![sshot-2020-02-15-[1].png](http://ww1.sinaimg.cn/large/006rgJELly1gbwy6ok0x4j306q04874d.jpg)

例子：
```sh
#!/bin/bash
#在CASE变量小于等于20的时候一直运行
CASE=0                  #初始化变量
echo "case = $CASE"     #显示变量
while [ $CASE -le 20 ]  #while条件
do                      #while开始
CASE=`expr $CASE + 1`   #相当于CASE++
echo "case = $CASE"     #显示下CASE的值
done                    #结束
```
