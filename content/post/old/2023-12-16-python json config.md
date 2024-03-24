+++
title = "python json config"
description = ""
date = 2023-12-16T15:17:51+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "python","json"
]
image = "py-json.png"
+++

python 使用json存储自身配置的代码示例;
包含配置缺少报错提示、初始化配置文件等功能，方便取用

<!--more-->
## 使用方法

声明 `config_path` 作为json存放路径

声明 `config_data` 作为全局变量（字典类型）

代码中使用 `load_json_config()` 读取 config.json 的配置到内存

> `load_json_config` 会调用 `try_create_config` 、  `check_config` , 功能包括把json读取到内存，如果没有配置文件则创建;如果读取到的 config 配置文件比 `config_data` 字典内容少会进行提示报错。

使用 `config_data['xxx']` 访问即可

## todo 
未完善保存相关功能，目前都是从外部加载配置文件，暂时没有保存需求！

```python
config_path = "assests\\config.json"
config_data = {
    "folder_root_path": "",
    "open_floder_key": "enter",
    "notifiction": "on",
    "auto_hide": "on",
    "playsound": "off",
    "soundeffect": "effect2.wav",
    "reload_key": "ctrl+f12",
    "open_config_key": "ctrl+shift+f12",
}

def try_create_config():
    '''尝试创建配置文件,仅在第一次运行时创建'''
    try:
        with open(config_path, encoding='utf-8') as file:
            tmp = json.load(file)
    except FileNotFoundError:
        with open(config_path, "w", encoding='utf-8') as file:
            json.dump(config_data, file, indent=4)
            print("created config.json")

def check_config():
    '''检查配置文件'''
    global config_data
    
    with open(config_path, encoding='utf-8') as file:
        json_config = json.load(file)
        for k,v in config_data.items():
            if k not in json_config:
                print_red("Config Error",f"missing {k}")
                print_red("example",f'"{k}": "{v}"')
                print_red("try remove assests/config.json")
                exit()
        

def load_json_config():
    '''加载配置文件'''
    try_create_config()
    global config_data
    with open(config_path, encoding='utf-8') as file:
        json_config = json.load(file)
        check_config()
        config_data.update(json_config) # 更新配置文件

```
