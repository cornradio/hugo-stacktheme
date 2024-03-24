+++

title = "corntab计划任务"
date = "2021-05-29"
author = "kasusa"
cover = ""
tags = ["ubuntu", "命令行"]
keywords = ["hugo2", ""]
description = "corntab的使用教程"
showFullContent = false

+++

# corntab

设置corntab任务，使用默认编辑器
```
corntab -e 
```

设置默认编辑器
```
select-editor 
```

设置任务，每天2：00执行
```
0 2 * * * /home/saber/DDREPORT/ddrp.sh
```