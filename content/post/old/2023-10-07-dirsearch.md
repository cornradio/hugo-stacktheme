+++
title = "dirsearch"
description = ""
date = 2023-10-07T09:32:55+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "dirsearch"
]
series = []
images = []
+++
[maurosoria/dirsearch: Web path scanner (github.com)](https://github.com/maurosoria/dirsearch)


扫描例句(win)
```
python dirsearch.py -u baidu.com -x400-500 -F --full-url 
python dirsearch.py -l urls.txt --headers-file headers.txt -x400-500 -F --full-url
```

扫描例句(kali)
```
dirsearch -u baidu.com -x400-500 -F --full-url 
dirsearch -l urls.txt --headers-file headers.txt -x400-500 -F --full-url
```
urls.txt 从burp中提取主要的url，headers.txt 从burp中拿登陆后的header

urls.txt 和 headers.txt 要新建在原版 py 文件目录下，否则，dirsearch找不到。

---

--full-url：显示完整URL路径，包括协议和域名。

-e 扫描后缀 如 `-e php,asp ` 

-u 域名可以带不带 http:// 前缀都可

---

查找到dirsearch的位置
```
locate dirsearch.py
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py 
```

你需要自行创建两个文件用来放置 url 和 headers
```
touch /usr/lib/python3/dist-packages/dirsearch/urls.txt
touch /usr/lib/python3/dist-packages/dirsearch/headers.txt
```

字典文件（可以自己修改、添加）：

```
/usr/lib/python3/dist-packages/dirsearch/db/dicc.txt 
```
