+++
title = "我写了一个python库：dumb_meun"
description = ""
date = 2023-02-18T16:19:07+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "python"
]
series = []
images = []
+++
> 我之前再我的程序里面 用了一个第三方库：`simple_term_menu`，提供菜单功能。但是当我再windows上尝试跑一下终于写好的程序时，竟然不能用。原因是它依赖于 `termios` 库， 不支持 win 。
> 因为我的功能需求比较简单，我决定自己下一个代替品，就是这个 `dumb_meun` 了。

主要要实现的功能：
- 传入一个 list ，显示菜单， 返回选中的 index
  - 上下键选择
  - enter建确认
  - *支持快捷键

因为python没有提供类似于c语言中的`getchar`函数，再 linux 上用 `termios` 库可以实现，但是在windows上使用的是 `msvcrt` 库。所以实际上在 python 中实现起来不是很容易。

```python
def get_key(): #get keypress using getch , msvcrt = windows or termios = linux
    try :
        import getch
        first_char = getch.getch()
        if first_char == '\x1b': #arrow keys
            a=getch.getch()
            b=getch.getch()
            return {'[A': 'up', '[B': 'down', '[C': 'right', '[D': 'left' }[a+b]
        if ord(first_char) == 10:
            return  'enter'
        if ord(first_char) == 32:
            return  'space'
        else:
            return first_char #normal keys like abcd 1234
    except :
        pass
    try:
        import msvcrt
        key = msvcrt.getch()  # get keypress
        if key == b'\x1b':  # Esc key to exit
            return 'esc'
        elif key == b'\r':  # Enter key to select
            return 'enter'
        elif key == b'\x48':  # Up or Down arrow
            return  'up'
        elif key == b'\x50':  # Up or Down arrow
            return 'down'
        else:
            return key.decode('utf-8')
    except:
        pass

while True:
    key = get_key()
    print("You pressed: ", key)
```

这个函数可以获取键盘输入，返回值是一个字符串，比如`up` `down` / `enter` / `a` `b` `c` / `1` `2` `3`，这样统一一下，可以兼容linux 和 win。

测试结果：
  ```
  Press a key to test out!
  You pressed:  down
  You pressed:  up
  You pressed:  a
  ...
  ```

## menu代码
> 我拷问了chatgpt老半天，他才给我编好

![后补充的流程图](https://raw.githubusercontent.com/cornradio/imgs/main/20230218215102.png)

- 提取快捷键是用 `re` 库的正则表达式

- 显示菜单通过 `os.system("cls" if os.name == "nt" else "clear")` 清屏，再打印出来，每次给菜单传入 list 和选中的 index ，这样用户可以看到自己正在选择哪个。

```python
import os
import re
def get_menu_choice(options):
    shortcuts = scan_short_cuts(options)  # scan for shortcuts
    selected_index = 0
    print(shortcuts)
    while True:
        show_menu(options, selected_index)
        key = get_key()
        if key == 'enter':  # Enter key to select
            return selected_index
        elif key in ('up','down'):  # Up or Down arrow
            selected_index = (selected_index + (1 if key == 'down' else -1) + len(options)) % len(options)
        elif key in shortcuts:  # Shortcut key
            show_menu(options, shortcuts[key]) #show selected option when using shortcut
            return shortcuts[key]

def scan_short_cuts(options):
    shortcuts = {}
    for i, option in enumerate(options):
        match = re.match(r"\[(.*)\](.*)", option)
        if match:
            shortcut, text = match.group(1, 2)
            shortcuts[shortcut] = i
    return shortcuts


def show_menu(options, selected_index):
    os.system("cls" if os.name == "nt" else "clear")
    print("Menu","current option:",selected_index)
    for i, option in enumerate(options):
        if i == selected_index:
            print(f"> {option}")
        else:
            print(f"  {option}")
    print("\nUse the arrow keys to move, Enter/Hotkey to select.")

```

使用方法非常直白：

```python
options = ["[1]Option 1", "[2]Option 2", "[3]Option 3","[q]quit"]
index = get_menu_choice(options)
print(f"You selected option {index + 1}: {options[index]}")
```

看看效果：

![](https://raw.githubusercontent.com/cornradio/imgs/main/20230214163952.png)

## 代码地址
> 其实我一开始想要参考一下 `simple_term_menu` 的源码，但是我发现我太菜了，根本看不懂他们的贼复杂的源代码（还用了信号啥的，我都不会），所以我就自己写了一个简单的。

使用的话就：
```
pip install dumb-menu
```
可以看看我在 pypi 写的[简明教程](https://pypi.org/project/dumb-menu/)