---
title: 命令行艺术 # 标题
slug: TheArtOfCli # url(注释掉 和标题相同)
image: theartofcli.jpg # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2024-07-25 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/TheArtOfCli/&count_bg=%230C0E0A&title_bg=%23000000)](https://hits.seeyoufarm.com)

https://www.youtube.com/watch?v=KdoaiGTIBY4

## fortune
随机来一个幸运饼干
```
sudo apt install fortune-mod -y
```

```
kali@DESKTOP-VNH6GDI:~$ fortune
If one cannot enjoy reading a book over and over again, there is no use
in reading it at all.
                -- Oscar Wilde
```


## figlet
字符画
```
sudo apt install figlet -y
```

```
kali@DESKTOP-VNH6GDI:~$ figlet fuck
  __            _
 / _|_   _  ___| | __
| |_| | | |/ __| |/ /
|  _| |_| | (__|   <
|_|  \__,_|\___|_|\_\

```

## cowsay
牛牛说话
```
 sudo apt install cowsay -y
```


```
kali@DESKTOP-VNH6GDI:~$ fortune |cowsay
 _________________________________________
/ Whenever the literary German dives into \
| a sentence, that is the last you are    |
| going to see of him until he emerges on |
| the other side of his Atlantic with his |
| verb in his mouth.                      |
|                                         |
| -- Mark Twain "A Connecticut Yankee in  |
\ King Arthur's Court"                    /
 -----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

还能换角色 


```
kali@DESKTOP-VNH6GDI:~/cowsay/cows$ cowsay -f eyes.cow  aaa
 _____
< aaa >
 -----
    \
     \
                                   .::!!!!!!!:.
  .!!!!!:.                        .:!!!!!!!!!!!!
  ~~~~!!!!!!.                 .:!!!!!!!!!UWWW$$$
      :$$NWX!!:           .:!!!!!!XUWW$$$$$$$$$P
      $$$$$##WX!:      .<!!!!UW$$$$"  $$$$$$$$#
      $$$$$  $$$UX   :!!UW$$$$$$$$$   4$$$$$*
      ^$$$B  $$$$\     $$$$$$$$$$$$   d$$R"
        "*$bd$$$$      '*$$$$$$$$$$$o+#"
             """"          """""""
```

## wtf
wtf is this 
wtf is that?
```
 sudo apt install bsdgames
```


```
kali@DESKTOP-VNH6GDI:~/cowsay/cows$ wtf is passwd
passwd: passwd (1ssl)        - OpenSSL application commands
passwd (1)           - change user password
passwd (5)           - the password file
kali@DESKTOP-VNH6GDI:~/cowsay/cows$ wtf is man
man: man (7)              - macros to format man pages
man (1)              - an interface to the system reference manuals
```

##  neofetch
显示一个 logo 和 pc 基础信息
```
sudo apt install neofetch -y
```


```
kali@DESKTOP-VNH6GDI:~$ neofetch
            .-/+oossssoo+/-.               kali@DESKTOP-VNH6GDI
        `:+ssssssssssssssssss+:`           --------------------
      -+ssssssssssssssssssyyssss+-         OS: Ubuntu 22.04.3 LTS on Windows 10 x86_64
    .ossssssssssssssssssdMMMNysssso.       Kernel: 5.15.133.1-microsoft-standard-WSL2
   /ssssssssssshdmmNNmmyNMMMMhssssss/      Uptime: 27 mins
  +ssssssssshmydMMMMMMMNddddyssssssss+     Packages: 538 (dpkg), 7 (snap)
 /sssssssshNMMMyhhyyyyhmNMMMNhssssssss/    Shell: bash 5.1.16
.ssssssssdMMMNhsssssssssshNMMMdssssssss.   Terminal: Windows Terminal
+sssshhhyNMMNyssssssssssssyNMMMysssssss+   CPU: 11th Gen Intel i5-1135G7 (8) @ 2.419GHz
ossyNMMMNyMMhsssssssssssssshmmmhssssssso   GPU: 7eaa:00:00.0 Microsoft Corporation Device  ossyNMMMNyMMhsssssssssssssshmmmhssssssso   Memory: 699MiB / 15827MiB
+sssshhhyNMMNyssssssssssssyNMMMysssssss+
.ssssssssdMMMNhsssssssssshNMMMdssssssss.
 /sssssssshNMMMyhhyyyyhdNMMMNhssssssss/
  +sssssssssdmydMMMMMMMMddddyssssssss+
   /ssssssssssshdmNNNNmyNMMMMhssssss/
    .ossssssssssssssssssdMMMNysssso.
      -+sssssssssssssssssyyyssss+-
        `:+ssssssssssssssssss+:`
            .-/+oossssoo+/-.
```

## cbonsai
c-盆栽,在你的命令行生成一个随机的盆栽...
```
sudo apt install cbonsai -y
```
-l 参数可以看生成过程

```
cbonsai -l

                                            & & &&&   &
                                             &&&&|/ &&&&
                                       &&    &&&&|\&&&&& &
                                     && &/~&\&& /|\&&&&&&
                                        &&&/  & &|&|&&
                              &         \&~&&   /~|/
                           &&&           \|& &   |/
                             &&&       \_ |&    \|
                           &&& &&& & \  \&&&&&_\|/|\
                            &&&\_&&__&   \/&&&& //|\
                          &&&         &&&&\&&   /|/       &
                             &         &&|&&&   \|       & &
                                        \&&&     \|    && &&&
                                         \|       \|  &  & &&&&&& &
                                          /~||  / _//~&&&&& &&_&_&&&
                                            //_/  |___/&&_/__/_&&& &&
                                           _/|/~|/~&//& /&//&   &
                                            /~ /~  & &    &
                                              /~/~/
                                              ///~
                              :___________./~~~\.___________:
                               \                           /
                                \_________________________/
                                (_)                     (_)
```
