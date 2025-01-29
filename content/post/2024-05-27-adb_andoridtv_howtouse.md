---
title: adb 绕过限制安装电视软件 # 标题
slug: adb_andoridtv_howtouse # url(注释掉 和标题相同)
image: adb.jpg # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2024-05-27 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/adb_andoridtv_howtouse/&count_bg=%230C0E0A&title_bg=%23000000)](https://hits.seeyoufarm.com)



> 注：除此之外还有一个方式 下载 [小米电视助手](https://m.app.mi.com/details?id=com.xiaomi.mitv.phone.tvassistant)  
在安卓机上可以远程可以电视安程序。

以下操作需要一台电脑：

## 首先下载并解压 adb 工具
https://dl.google.com/android/repository/platform-tools-latest-windows.zip 
电脑上用命令行打开解压后的文件夹位置

## 在电视上开启 adb 功能
电视-设置 -WiFi -详情里面能看到 IP 地址： 192.168.31.172  
电视-关于 - 产品型号，连续点击就可以打开 【开发者模式】  
在账号与安全 - adb 调试开关，打开开关 


```
连接设备
adb connect 192.168.31.172:5555
查看设备列表
adb devices 
如果有连接失败的记录要 删除,保持连一个设备
adb disconnect xxxx
```


如果提示unauthorized（第一次连接后会显示成unauthorized)

```
需要执行下面两个命令:
adb kill-server
adb start-server

然后再次连接
adb connect 192.168.31.172:5555

这次连接的时候电视上应该跳出一个弹窗,你要允许调试
```

## 安装程序

```
第一次安装
adb install "c:/xxx/xxx.apk"
重装
adb install -r "c:/xxx/xxx.apk"
查看所有已装程序
adb shell pm list packages
删除程序
adb shell pm uninstall -k --user 0 <package_name>
```

这个命令可以解除安装限制: 
```
adb shell
darwin:/ $ settings put global package_verifier_enable 0
darwin:/ $ exit
```

顺便推荐一些好用软件  
https://github.com/xiaye13579/BBLL   哔哩哔哩客户端
https://github.com/lizongying/my-tv  最近没更新了 tv直播软件 ，不推荐。

春节到了，推荐一些免费的安卓电视直播软件 
## 软件推荐
https://github.com/andandroidor/ourtv  电视直播软件
https://github.com/sakana164/mytv-android ipv6 电视直播软件
