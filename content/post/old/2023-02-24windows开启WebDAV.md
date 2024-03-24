+++
title = "windows开启WebDAV"
description = ""
date = 2023-02-24T19:56:44+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "windows"
]
series = []
images = []
+++
开启 WebDAV 可以让你的 windows 设备变成家庭媒体服务器。

这是一个替代选项，毕竟ftp已经过时（无安全性）、文件夹共享简直是太烂了

## 开启系统功能
- 搜索：启用或关闭 Windows 功能
- 勾选并开启下列功能
```
- Internet Information Services 功能（全选）

  （Internet Information Services 中下列功能需要手动打勾，默认不选）
  - 万维网服务功能
    - 安全性
      - 基本身份验证
    - 常见HTTP功能
      - Webdav发布
```

## 创建 webDAV 站点
1. 添加网站
   
   ![](https://raw.githubusercontent.com/cornradio/imgs/main/20230224201122.png)
2. 开启下列功能
   
   ![](https://raw.githubusercontent.com/cornradio/imgs/main/20230224201149.png)
3. webdav - 右侧 - 启用`webdav`
4. webdav - 添加创作功能 - 允许所有用户，分配读写权限
5. 目录浏览 - 打开功能
6. 身份验证 - 基本身份验证 - 启用（其他选项禁用）

- ✨右键重启网站

## 准备要分享的文件夹

> 针对错误：无权访问`web.config`

- 在任何目录下新建一个文件夹，比如：`e:本地影视`
- 确保添加`everyone`用户组的完全控制权限
  ![](https://raw.githubusercontent.com/cornradio/imgs/main/20230224201314.png)


## 打通网络
> 针对问题：在其他电脑上无法连接到 8090 端口


搜索并打开：防火墙

新增一条入站规则、一条出站规则，允许端口8090的所有通信。

![](https://raw.githubusercontent.com/cornradio/imgs/main/20230224202305.png)


## 设置mime类型

> 解决特殊格式视频403错误

可以手动添加一条mime类型

![](https://raw.githubusercontent.com/cornradio/imgs/main/20230224204437.png)

或者可以在 `web.config` （会自动的在根文件夹生成）添加如下配置

```xml
<configuration>
    <system.webServer>
    <!-- 添加了支持浏览器查看目录的功能 -->
        <directoryBrowse enabled="true" />
        <staticContent>
            <!-- 解决 rmvb格式  404.3 mime格式不支持的问题 -->
            <mimeMap fileExtension=".*" mimeType="video/mpeg" />
        </staticContent>
    </system.webServer>
</configuration>

```

## 登录用的账号

微软账号：邮箱 + 密码