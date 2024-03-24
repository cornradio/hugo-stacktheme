+++
title = "用 simple_term_menu 创建更好的python菜单"
description = ""
date = 2023-02-09T16:25:24+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "python","menu"
]
series = []
images = []
+++

安装

```sh
pip install simple_term_menu
```
⚠️ 不支持windows
这个菜单库使用非常简单，只需要传入一个列表，就可以生成一个菜单，返回值就是选择的菜单项的索引。

- 支持`J` `K`/⬆️ ⬇️ 键移动
- 支持`/`斜杠搜索
- 支持快捷键（传入的 string 如 `[q] 退出` ,q 就变成快捷键了）
- 好看！
- 还有更多功能，我没有仔细研究，参考[>这里<](https://github.com/IngoMeyer441/simple-term-menu)

封装成函数，方便调用

```python
from simple_term_menu import TerminalMenu
def menu(choices:list):
    terminal_menu = TerminalMenu(choices,title="扫描结果转换XML工具 v1.0 (230208)\n---",show_search_hint=True)
    index = terminal_menu.show()

    print("执行", choices[index])
    if choices[index] == "[h] 文档":
        import webbrowser
        webbrowser.open('http://example.com')  
        return 0
    if choices[index] == "[q] 退出":
        exit()
    return index + 1 # 返回结果，从1开始
```


main 函数调用

```python
if __name__ == '__main__':
    while True:
        # 获取功能列表，显示菜单
        choices_str = open('menu.md', 'r', encoding='utf-8').read()
        choices =choices_str.splitlines()
        choice_index = menu(choices)
```


> 其实一开始选择用md是因为写序号的话可以自动排序，但是加了序号和快捷键之后，就不美观了，所以把序号删除了。

加载菜单 menu.md 

```md
长亭xray（主机+应用） html 1->1
长亭xray（主机+应用） html 多->1
绿盟（主机） <ip>.html 1->1
绿盟（主机） <ip>.html 多->1
安恒新版 (应用) html 1->1
Nessus csv(utf-8) 1->1
Nessus csv(gb18030) 1->1
[h] 文档
[q] 退出
```

效果图：
![](https://raw.githubusercontent.com/cornradio/imgs/main/20230209163535.png)

对了这个东西还有个坑的地方，在pycharm运行的时候需要设置一下才能正常使用（要开启模拟终端）：
![](https://raw.githubusercontent.com/cornradio/imgs/main/20230209163631.png)
