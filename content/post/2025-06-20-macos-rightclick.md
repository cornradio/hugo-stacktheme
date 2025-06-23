---
title: macos右键菜单编辑 # 标题
slug: macos-rightclick # url(注释掉 和标题相同)
image: https://i.imgur.com/4aOWR6L.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2025-06-23 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fmacos-rightclick&label=&icon=check-all&color=%23198754)

# macOS 右键菜单添加脚本
要点：在 自动操作软件中
1. 新建快捷操作
2. 工作流程输入： “文件和文件夹”
3. 位于 访达
4. 下面 传递输入 ， 作为自变量

![picture 1](https://i.imgur.com/4aOWR6L.png)  
![picture 2](https://i.imgur.com/6bJGQ6o.png)  

## 右键菜单展示
![picture 6](https://i.imgur.com/WKP6g27.png)  



## 1.增加一个转换gbk - utf8的功能

```
for f in "$@"
do
    iconv -f GBK -t UTF-8 "$f" > "${f%.txt}.utf8.txt"
done
```

![picture 4](https://i.imgur.com/S6YXESt.png)  


#### 🔸 `iconv -f GBK -t UTF-8 "$f" > "${f%.txt}.utf8.txt"`

- `iconv` 是命令本体，执行编码转换：
    - `-f GBK`：原编码是 GBK
    - `-t UTF-8`：目标编码是 UTF-8
- `"$f"` 是当前要处理的原始文件路径
- `> "${f%.txt}.utf8.txt"` 表示：
    - 输出文件为原文件名把 `.txt` 改为 `.utf8.txt`
    - `${f%.txt}` 是 Bash 的字符串替换语法，意思是“把结尾的 `.txt` 去掉”
    - 如果原文件叫 `hello.txt`，那输出文件就是 `hello.utf8.txt`
- `>` 表示输出写入新文件（不会覆盖原文件）

## 增加【用code 打开】菜单

https://code.visualstudio.com/ vscode， 程序员必备！

```
for f in "$@"
do
    open -a "Visual Studio Code" "$f"
done
```
![picture 3](https://i.imgur.com/KxO3Wsp.png)  


## 增加用 iterm 打开 菜单
https://iterm2.com/ 是一个很棒的终端软件。

```
for f in "$@"
do
    open -a "iTerm" "$f"
done
``` 
![picture 5](https://i.imgur.com/NNykhMO.png)  


## 增加用keka压缩菜单

这个需要使用 apple script 而不是命令行指令
keka 可以在 https://www.keka.io/en/ 下载，是一个开源好用的macos压缩软件。

```
on run {input, parameters}
    repeat with f in input
        set thePath to POSIX path of f
        do shell script "open -a Keka \"" & thePath & "\""
    end repeat
    return input
end run
```
![image](https://github.com/user-attachments/assets/e68f1cad-8a59-42bd-b8bd-03c693359d52)


