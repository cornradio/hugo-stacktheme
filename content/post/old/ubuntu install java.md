+++

title = "ubuntu上安装java"
date = "2021-05-29"
author = "kasusa"
cover = ""
tags = ["ubuntu", "命令行"]
keywords = ["", ""]
description = "可以玩mc的java"
showFullContent = false

+++
ubuntu 安装 java 最好的教程：https://docs.datastax.com/en/jdk-install/doc/jdk-install/installOracleJdkDeb.html

## steps
1. 去oracle下载你要的java
    ```
    https://www.oracle.com/java/technologies/javase-downloads.html
    ```
    1.1 一般来说你需要解压之后把文件放在 `/usr/lib/jvm` 这里是标准的java存放位置

2. 让系统知道你新装了 java 还有他的位置 (更改后半句的目录为你的java解压路径 最后面的是java config编号)
    ```
    sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk-15.0.1/bin/java" 1
    ```
3. 选择你的新java版本
    ```
    sudo update-alternatives --config java
    ```
4. 测试是否成功
    ```
    java -version
    ```

