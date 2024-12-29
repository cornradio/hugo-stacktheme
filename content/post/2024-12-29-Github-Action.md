---
title: Github_Action-入门
date: 2024-12-29 00:00:00+0000
slug: Github_Action
image: https://i.imgur.com/kWCcd38.png
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/Github_Action/&count_bg=%23F26E00&title_bg=%23000000)](https://hits.seeyoufarm.com)

简单来说,如果你经常需要手动build. 或者给多个平台一起build. 或者任何自动化的操作,都可以用 github action功能 !   
他能快速给你一个临时虚拟机, 可以是linux、windows、macos .  然后你还能执行任何命令 .  
需要学习他的yml语法、了解常用功能才能正常使用他的基础功能.  
比如,我通过做一个python


## 学习资料
[github action官网](https://github.com/features/actions)
皮皮虾的[github action 例子](https://github.com/tech-shrimp/GithubActionSample)
可以在github的 [marketplace](https://github.com/marketplace?type=actions) 搜索到别人编写好的 action ,但是我觉得还不如自己写..用起来号麻烦啊. 
[官方文档](https://docs.github.com/en/actions/writing-workflows/quickstart)
[语法参数](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions#about-yaml-syntax-for-workflows) 这里可以看到支持的虚拟机型号 runs-on:`ubuntu-latest` \ 各种参数选项 on: `[push]`之类的

# act 简介和安装

> 提示 ： act 不适合模拟其他系统，大概率报错，我想在 m1 上面跑一个 x64 的 windows ，失败了

act 是本地环境,可以用来测试你写的action对不对.  
但是 很难用. 因为. 他需要docker 还有github的网络环境.  
in ZhCn is very hard!!! to use !!!!

https://www.direcore.xyz/archives/39/

使用之前需要先安装好 `docker` 环境。

[act](https://github.com/nektos/act/releases/tag/v0.2.35)  [docker](https://www.docker.com)

mac 用户可以通过 brew 安装 act

```
brew install act
```

# act

在运行 `act` 之前，需要先启动 `docker` 保证他在后台运行 ， 保证网络通畅，在运行的时候需要下载环境之类的，如果网络不行很慢很慢，还不如让等一个 `runner` 来跑了。我们安装本地调试的意义就没了。

首先进入你配置过脚本的 `act` 目录，查看所有的 job 

```
act -l
```

 如果你有不止一个 job，那么可以使用下面的命令执行指定的 job
 
```
act -j <job id>
```


```
act -P windows-latest=-self-hosted
```



## 创建文件

```
.github/workflows/xxx.yml
```


```yml
# 语法 https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions#about-yaml-syntax-for-workflows
name: GitHub Actions Demo # 工作流名称 显示在 action 的左侧栏
run-name: ${{ github.actor }} is testing out GitHub Actions 🚀 # 显示在右边的展开面板
on: [push] # 触发条件 push 事件,这个方框是一个数组 可以有多个如 [push, fork]
jobs: # 你的任务列表
  Explore-GitHub-Actions: # 任务名称
    runs-on: ubuntu-latest # 运行环境 还有 windows-latest 还有 macOS-latest 
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event." #这种是单行命令
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code # 下载你的库代码
        uses: actions/checkout@v4
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository #这种是多行命令
        run: | #这种竖杠yaml标准多行语法 他会保留换行符
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."

```


这是一个我写的制作 Python打包的一个action
这里有几个关键的操作
1. 选择虚拟机
2. 创建python环境
3. pull action
4. 运行命令
5. 生成 artifacts (编译后导出的下载文件)
```yml
name: Python package

on: [push]

jobs:
  build-ubuntu-executable:
    runs-on: ubuntu-22.04
    strategy:
      matrix:
        python-version: ["3.10"]
    steps:
    -   uses: actions/checkout@v4
    -   name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v5
        with:
            python-version: ${{ matrix.python-version }}
    # You can test your matrix by printing the current Python version
    -   name: install pip requirements
        run: |
            pip install -r requirements.txt
    -   name: build by cmd
        run: |
            pyinstaller --name=LAN_clipboard_app --add-data "templates:templates" --add-data "static:static" app.py -y
            chmod +x dist/LAN_clipboard_app
    -   name: Copy artifacts
        uses: actions/upload-artifact@v3
        with:
            name: lanclip-linux-x64
            path: dist/
```

