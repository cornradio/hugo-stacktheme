---
title: macos tips # 标题
date: 2025-03-11 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
slug: macos-tips # url(注释掉 和标题相同)
# description: xxxx # 描述小字(注释掉 不显示描述)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)
image: 0HikPKN.jpg # 头图，注释掉，否则会有一个难看的呃加载不出来的图片

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

最近进入新公司工作后，使用的是macos笔记本办公，积累了很多的小技巧 可以帮助高效的使用macos

## 快捷键
https://support.apple.com/zh-cn/102650
### finder
- **按住 Option-Command 键拖移**：为拖移的项目制作替身。
- cmd + J 设置目录展示，可以按照不同的方式来分组和排序。
- Command + Shift + . 显示隐藏文件
- 
### 文本
- ctrl + D 、fn + 退格， 删除右边 相当于 win del
- cmd + shift + 方向 快速选中一行。

## 任务栏缩放加速
https://www.sqlsec.com/2023/07/ventura.html

```
# 设置启动坞动画时间设置为 0.5 秒 
defaults write com.apple.dock autohide-time-modifier -float 0.5 && killall Dock
defaults write com.apple.dock autohide-time-modifier -float 0 && killall Dock


# 设置启动坞响应时间最短
defaults write com.apple.dock autohide-delay -int 0 && killall Dock

# 恢复启动坞默认动画时间
defaults delete com.apple.dock autohide-time-modifier && killall Dock

# 恢复默认启动坞响应时间
defaults delete com.apple.Dock autohide-delay && killall Dock
```

## 信任证书

1. 下载证书
	1. chrome - 左上角-证书查看
	2. 找到第二页tab , 下载
2. 钥匙串访问 app - 文件-加入项目
3. 找到新增的证书 , cmd + i 修改权限 全部允许

## 安装brew 

```
bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

```
brew --version
```

## 临时替换brew源

修改 .zshrc 文件 创建命令vbrew ， 使用ali源
```sh
alias vbrew='
export HOMEBREW_INSTALL_FROM_API=1
export HOMEBREW_API_DOMAIN="https://mirrors.aliyun.com/homebrew-bottles/api"
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.aliyun.com/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.aliyun.com/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.aliyun.com/homebrew/homebrew-bottles"
brew update
'
```

## 右键文件-用vscode打开

https://homeboyc.cn/blog/把用vscode打开按钮加入macos右键菜单/
需要使用applescript 这个东西我不太懂 但是能用就行！

## one key hi-dpi

one key hi-dpi 是一个开源的命令行软件，用途是让一些不支持 hidpi的屏幕 可以支持。比如2k屏幕 。
```
bash -c "$(curl -fsSL https://raw.githubusercontent.com/xzhih/one-key-hidpi/master/hidpi.sh)"
```

## folderify icon

folderify 是一个macos文件夹美化命令行工具
1. 安装
```
brew install folderify
```
1. 去下载图标： https://tabler.io/icons ，或者用任何普通的图片
2. 准备png图标 可以使用 https://www.remove.bg/zh/upload 在线抠图工具
3. 执行命令，替换文件夹图标，可以用 opt + cmd + c 复制目录地址（或者 opt+右键点击）
```
folderify mask.png /path/to/folder
folderify link.png /Users/shrimppipi/TeamFile/私人文件库/url
```


