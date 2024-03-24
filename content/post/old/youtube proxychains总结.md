+++

title = "proxychains 使用教程"
date = "2021-05-29"
author = "kasusa"
cover = ""
tags = ["ubuntu", "命令行"]
keywords = ["", ""]
description = ""
showFullContent = false

+++
1. 安装proxychains sudo apt install proxychains4

2. 配置他的配置文件：sudo vim /etc/proxychains4.conf 
    - 取消掉的注释 dynamic_chain

   - 将底部的网络协议和代理端口和ip改成你翻墙软件提供的:

   - ```
     socks5  127.0.0.1 1089
     http    127.0.0.1 8889
     ```

3. 通过proxychains4 来在bash启动其他程序：proxychains4 <程序名>

ps：可以去 `/.bashrc` 给`proxychains`起一个别名，比较方便



