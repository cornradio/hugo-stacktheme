+++

title = "自学 linux 命令"
date = "2022-08-18"
author = "kasusa"
cover = ""
tags = ["ubuntu", "命令行"]
keywords = ["", ""]
description = "自学 linux 命令"
showFullContent = false

+++

[官方培训课程](https://www.linuxprobe.com/training)

## 控制台常用快捷键
按键 | 作用
---|---
Ctrl+d | 键盘输入结束或退出终端
Ctrl+s | 暂停当前程序，暂停后按下任意键恢复运行
Ctrl+z | 将当前程序放到后台运行，恢复到前台为命令fg
Ctrl+a | 将光标移至输入行头，相当于Home键
Ctrl+e | 将光标移至输入行末，相当于End键
Ctrl+k | 删除从光标所在位置到行末
Alt+Backspace	| 向前删除一个单词
Shift+PgUp	| 将终端显示向上滚动
Shift+PgDn	| 将终端显示向下滚动

## 一次性创建多个文件
```
#实际上是一个简单的shell loop
$ touch love_{1..10}_shiyanlou.txt
```

## 常用通配符

字符 |含义
---|---
* |匹配 0 或多个字符
? |	匹配任意一个字符
[list] |	匹配 list 中的任意单一字符
[^list] |	匹配 除 list 中的任意单一字符以外的字符
[c1-c2] |	匹配 c1-c2 中的任意单一字符 如：[0-9][a-z]
{string1,string2,...} |	匹配 string1 或 string2 (或更多)其一字符串
{c1..c2} |	匹配 c1-c2 中全部字符 如{1..10}

# 用户管理

创建用户(默认会让输入密码)
```
sudo adduser <USERNAME>
```
修改密码
```
sudo passwd <USERNAME>
```
切换用户
```
su <USERNAME>
```
查看当前用户是谁
```
whoami
```
查看用户组
```
cat /etc/group | grep -E "<USERNAME>"
```
给新建的用户sudo权限(第二条是centos里面的情况。)
```
usermod -G sudo <USERNAME>
usermod -aG wheel <USERNAME> 
```
删除用户(把它创建时自动创建的用户目录一并删除)
```
sudo deluser lilei --remove-home
```
 **adduser 和 useradd 的区别是什么**

> 答：useradd 只创建用户，不会创建用户密码和工作目录，创建完了需要使用 passwd <username> 去设置新用户的密码。adduser 在创建用户的同时，会创建工作目录和密码（提示你设置），做这一系列的操作。其实 useradd、userdel 这类操作更像是一种命令，执行完了就返回。而 adduser 更像是一种程序，需要你输入、确定等一系列操作
查看所有登录的用户（都有谁，都在哪里登录）

```
who
```

# 常用东西

## 配置主机名称

`4.1.2 配置主机名称`

1. 使用 Vim 编辑器修改“/etc/hostname”主机名称文件。
2. 把原始主机名称删除后追加你想要起的名字。注意，使用 Vim 编辑器修改主机名称文件后，要在末行模式下执行:wq!命令才能保存并退出文档。
3. 保存并退出文档，然后使用 hostname 命令检查是否修改成功。

> 不好用的时候试着重新启动

# 文件管理



![图像权限](https://doc.shiyanlou.com/linux_base/3-10.png/wm)
这个图是在使用`ls -l`时候前部的意义。

chmod 修改权限。每一个数字代表对应权限
```
rwx|r-x|r-x
111|101|101 = 755
```

chown 修改所有者
```
chown <usrname> <filename>
```
## 在目录间移动

```sh
#去tmp目录
cd /tmp
#去上一层目录
cd ..
#去当前用户的home（无参数cd）
cd 
```



## 创建文件和目录

touch 可以创建文件/更新文件时间戳。
mkdir 可以创建目录
mkdir -p 可以创建多级目录
```
 mkdir -p father/son/grandson
```
## 复制文件/目录
复制文件 
```
cp <文件> <目的地>
```
复制目录
```writer
cp <要复制的目录> <目的地>
```

## 删除文件
```
rm <文件>
rm -r <目录>
rm -f <文件> (包括有写保护的文件)
rm -rf <任何东西>
```

## 移动和重命名

```
mv <原文件> <新位置>
mv <原文件名> <新文件名字>
```

批量重命名

```
rename <'正则'> <通配符>
```
## linux文件目录结构
![目录结构](https://doc.shiyanlou.com/linux_base/4-1.png/wm)

# shell script



## 变量

声明变量
```
declare tmp
```
直接用=赋值同时也可以新建变量,注意不要在等号左右使用空格
```
tmp=helloyou
```
拿出变量tmp
```
echo $tmp
```
删除变量tmp
```
unset tmp
```

## 环境变量
暂时设置一个环境变量
```
tmp=helloyuoman
export tmp
```
永久设置一个环境变量
```
/etc/bashrc         shell变量（有的 Linux 没有这个文件） 
/etc/profile        环境变量
/home/usr/.profile  用户变量
```
shiyanlou的环境用的是zsh命令行，在根目录有一个`.zshrc`文件是初始化配置文件。
可以使用这句来把 /home/shiyanlou/mybin 添加到path中

> 注意,这里是用的 >> 它意味"追加" , > 是覆盖的意思
```
$ echo "PATH=$PATH:/home/shiyanlou/mybin" >> .zshrc
```
直接刷新环境变量(无需开新的zsh)**两种等效**
```
source .zshrc
. .zshrc
```


## 修改已有变量
变量设置方式 |	说明
---|---
${变量名#匹配字串} |	从头向后开始匹配，删除符合匹配字串的最短数据
${变量名##匹配字串} |	从头向后开始匹配，删除符合匹配字串的最长数据
${变量名%匹配字串} |	从尾向前开始匹配，删除符合匹配字串的最短数据
${变量名%%匹配字串} |	从尾向前开始匹配，删除符合匹配字串的最长数据
${变量名/旧的字串/新的字串} |	将符合旧字串的第一个字串替换为新的字串
${变量名//旧的字串/新的字串} |	将符合旧字串的全部字串替换为新的字串


## 搜索文件
whereis 简单快速

> whereis 只能搜索二进制文件(-b)，man 帮助文件(-m)和源代码文件(-s)。如果想要获得更全面的搜索结果可以使用 locate 命令。

locate快而全 使用要先安装,并且更新索引数据库
```
sudo apt-get update
sudo apt-get install locate
sudo updatedb
```

find 超强大
> 寻找/etc中(包括子目录)名为的 sources.list文件
```
find /etc -name sources.list
```


## man 命令中常用按键以及用途

按键 |用途
---|---
空格键 | 向下翻一页
/ |从上至下搜索某个关键词，如“/linux”
? |从下至上搜索某个关键词，如“?linux”
n | 定位到下一个搜索到的关键词
N | 定位到上一个搜索到的关键词

# 系统状态
## ps aux命令
状态值|意义
---|---
R（运行）| 进程正在运行或在运行队列中等待。
S（中断）| 进程处于休眠中，当某个条件形成后或者接收到信号时，则脱离该状态。
D（不可中断）| 进程不响应系统异步信号，即便用 kill 命令也不能将其中断。
Z（僵死）| 进程已经终止，但进程描述符依然存在, 直到父进程调用 wait4()系统函数后将进程释放。
T（停止）| 进程收到停止信号后停止运行。

如果我们在系统终端中执行一个命令后想立即停止它，可以同时按下 ` Ctrl + C` 组合
键（生产环境中比较常用的一个快捷键），这样将立即终止该命令的进程。或者，如果
有些命令在执行时不断地在屏幕上输出信息，影响到后续命令的输入，则可以在执
行命令时在末尾添加上一个 `&` 符号，这样命令将进入系统后台来执行。

## ifconfig 命令
ifconfig 命令用于获取网卡配置与网络状态等信息，格式为“ifconfig [网络设备] [参数]”。使用 ifconfig 命令来查看本机当前的网卡配置与网络状态等信息时，其实主要查看的就是网卡名称、inet 参数后面的 IP 地址、ether 参数后面的网卡物理地址（又称为 MAC 地址）

## uptime 命令
uptime 用于查看系统的负载信息，格式为 uptime。

uptime 命令真的很棒，它可以显示当前系统时间、系统已运行时间、启用终端数量以及平均负载值等信息。平均负载值指的是系统在最近 1 分钟、5 分钟、15 分钟内的压力情况（下面加粗的信息部分）；负载值越低越好，尽量不要长期超过 1，在生产环境中不要
超过 5。

## uname -a
查看计算机的系统类型
## free -h
查看内存
## last 命令
last 命令用于查看所有系统的登录记录，格式为“last [参数]”。
## history
查看历史命令记录。
`history -c` 清空记录

# 切换目录
## pwd 命令
pwd 命令用于显示用户当前所处的工作目录，格式为“pwd [选项]”。
## cd 命令
cd| 命令用于切换工作路径，格式为“cd [目录名称]”。
---|---
`cd -` |命令返回到上一次所处的目录
`cd ..` |命令进入上级目录
`cd ` |命令切换到当前用户的家目录
`cd ~username` |切换到其他用户的家目录。

## ls
命令|~
---|---
ls -a  | 查看隐藏文件
ls -l  | 查看文件详细信息
ls -la | 查看隐藏文件以及显示详细

# 查看文件
## cat 命令
用来查看比较小的文本文件

`cat -n`  查看文本内容时还想顺便显示行号
`tac` 可以倒序输出文件.

## more 命令

```
more <文件名>
```
more更加适合阅读长文件

可以使用
* <kbd>enter</kbd> 向下一行
* <kbd>space</kbd> 向下一屏
> Less 比more强多了

## head 和 tail
默认查看文件头部/尾部的10行。参数 -n 可以控制行数。

tail可以使用 -f 查看最新一行.
```
head -n 1 <文件名>
tail -f <文件名>
```
## wc 命令
wc 命令用于统计指定文本的行数、字数、字节数，格式为“wc [参数] 文本”。

` file` 命令来查看文件类型

## 压缩
`tar -czvf 压缩包名称.tar.gz 要打包的目录`

- 打包-压缩-显示废话-选择目录

x：解包

c：打包

## 搜索
`grep` 命令用于在文本中执行关键词搜索，并显示匹配的结果，通常和别的命令结合使用，如cat、ps等

~|~
---|---
 -b    |将可执行文件（binary）当作文本文件（text）来搜索
 -c    |仅显示找到的行数
 -i    |忽略大小写
 -n    |显示行号
 -v    |反向选择 — 仅列出没有“关键词”的行

```
root@iZ2ze1hf17j9hv44rdpmaaZ:~# grep -n Jan you
2:-rw-r--r-- 1 root root   17 Jan 12  2000 kasusa
3:drwxr-xr-x 2 root root 4096 Jan 30 10:15 mydir
4:drwxr-xr-x 2 root root 4096 Jan 30 10:16 mydir2
5:drwxr-xr-x 2 root root 4096 Jan 30 11:47 ooo
6:-rw-r--r-- 1 root root    0 Jan 30 11:51 you 

# you是一个文件。用显示行号的模式在you里面寻找 Jan 关键字 。在控制台里面会有高亮显示

```

## 别名
可以用 `alias` 命令来创建一个属于自己的命令别名，格式为“`alias 别名=命令`”。

若要取消一个命令别名，则是用 unalias 命令，格式为“unalias 别名”。

可以写入.bashrc文件，或者是.zshrc文件，取决于你用的是啥shell，然后就可以永久用这些别名了。

下面是一个我在macos上面使用的例子：

```
#显示有颜色的用户（不适合白色背景）
export PS1="%10F%m%f:%11F%1~%f \$ "
#online
alias f="top -l 1 | head -n 10 | grep PhysMem" # 查看可用内存
alias p="sudo purge" # 整理释放内存
alias v="export http_proxy=http://127.0.0.1:7890;export https_proxy=http://127.0.0.1:7890" # 终端设置翻墙
alias nv="unset http_proxy; unset https_proxy;" # 终端设置不翻墙
alias ip="curl cip.cc" # 查看ip和是否翻墙
alias py=python3

```



## 变量和全局
一般来说，变量都是用大写的。

有一些|常用的全局变量：
---|---
HOME |用户的主目录（即家目录）
SHELL| 用户在使用的 Shell 解释器名称
HISTSIZE |输出的历史命令记录条数
HISTFILESIZE |保存的历史命令记录条数
MAIL |邮件保存路径
LANG |系统语言、语系名称
RANDOM |生成一个随机数字
PS1 Bash |解释器的提示符
PATH |定义解释器搜索用户执行命令的路径
EDITOR |用户默认的文本编辑器

自己创建一个变量/读取它：
```
root@iZ2ze1hf17j9hv44rdpmaaZ:~# MYVAR="hello"
root@iZ2ze1hf17j9hv44rdpmaaZ:~# echo "$MYVAR"
hello
```

提升位全局变量：
```
root@iZ2ze1hf17j9hv44rdpmaaZ:~# export MYVAR
```

# VIM

## Vim 中常用的命令

命令| 作用
---|---
dd  |删除（剪切）光标所在整行
5dd |删除（剪切）从光标处开始的 5 行
yy |复制光标所在整行
5yy |复制从光标处开始的 5 行
n |显示搜索命令定位到的下一个字符串
N |显示搜索命令定位到的上一个字符串
u |撤销上一步的操作
p |将之前删除（dd）或复制（yy）过的数据粘贴到光标后面



## 末行模式中可用的命令
**要想切换到末行模式，在命令模式中输入一个冒号就可以了。**
末行模式主要用于保存或退出文件，以及设置 Vim 编辑器的工作环境，还可以让用户执
行外部的 Linux 命令或跳转到所编写文档的特定行数。

命令 |作用
---|---
:w |保存
:q |退出
:q!|强制退出（放弃对文档的修改内容）
:wq!| 强制保存退出
:set| nu 显示行号
:set| nonu 不显示行号
:命令| 执行该命令
:整数| 跳转到该行
:s/one/two |将当前光标所在行的第一个 one 替换成 two
:s/one/two/g |将当前光标所在行的所有 one 替换成 two
:%s/one/two/g |将全文中的所有 one 替换成 two
?字符串 |在文本中从下至上搜索该字符串
/字符串 |在文本中从上至下搜索该字符串

# append

查看命令的来源：type

```
kasusadeMacBook-Pro:~ $ type who
who is /usr/bin/who
kasusadeMacBook-Pro:~ $ type cd
cd is a shell builtin
```

输入输出导向：

其中输出分成 普通输出、错误输出

```sh
any command < infile
any command > outfile #Create/overwrite outfile 
any command >> outfile #Append to outfile
any command 2> errorfile
#普通输出、错误输出 同时输出到两个文件
any command > outfile 2> errorfile 
#普通输出、错误输出合并输出到1个文件
any command >& outfile
any command &> outfile
```

一行执行多个命令

```
# 直接按顺序执行
command1 ; command2 ; command3
# 按顺序执行但是如果遇到错误会停止
command1 && command2 && command3
# 按顺序执行但是如果遇到成功的直接退出
command1 || command2 || command3
```

引号

> 一般来说空格作为分隔符，如果输入中要带空格需要用单or双引号把它扩起来

- 单引号：原样输出
- 双引号：可以在其中加入变量等
- 反引号（tilda）：反引号之中的字符串会作为变量来执行

```
→ echo 'The variable HOME has value $HOME' 
The variable HOME has value $HOME
→ echo "The variable HOME has value $HOME" 
The variable HOME has value /home/smith
→ echo This year is `date +%Y` 
This year is 2021
→ echo hello `expr $(date +%Y) + 1` # expr可以用来做运算，但是要在运算符号之间加空格
This year is 2023
```

