+++
title = "Json读写（Python）"
description = ""
date = 2023-01-31T15:34:37+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  ""
]
series = []
images = []
+++
使用 python 读写 json，或者使用 json5 处理一些格式“不太正确”的 json string，比如js代码的格式。
<!--more-->
把 python 对象编码成 json string


```python
import json

data = { 'a' : 1, 'b' : 2, 'c' : 3, 'd' : 4, 'e' : 5 } 
data_str = json.dumps(data, indent=4, separators=(',', ': '))
print(data_str)
```

解码 json string 到 python 对象

loads() 和 dumps() 函数 处理字符串

load() 和 dump() 函数 处理文件


```python
import json
# jsonstr = '{a:1,b:2,"c":3,"d":4,"e":5}'
jsonstr = '{"a":1,"b":2,"c":3,"d":4,"e":5}'
json_obj = json.loads(jsonstr)
json_obj['a']
```




    1



## 第三方库：Demjson


```
pip install demjson3
```


```python
import demjson3
data = { 'a' : 1, 'b' : 2, 'c' : 3, 'd' : 4, 'e' : 5 } 
demjson3.encode(data)
```




    '{"a":1,"b":2,"c":3,"d":4,"e":5}'



Demjson 可以处理一些格式“不太正确”的 json string


```python
jsonstr = '{a:1,b:2,"c":3,"d":4,"e":5}'
demjson3.decode(jsonstr)
```




    {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}



# json5

```
pip install json5
```

json5也可以处理一些格式“不太正确”的 json string ，并且语法要和 json 标准库一样


```python
import json5
jsonstr = '{a:1,b:2,"c":3,"d":4,"e":5}'
myobj = json5.loads(jsonstr)
```

json5 保存到文件


```python
json5.dump(myobj, open('test.json5', 'w'), indent=4)
```
