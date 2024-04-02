+++
title = "使用python多线程批量ping"
description = ""
date = 2022-06-18T19:53:02+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "python",  "Network"
]
series = []
images = []
+++



> 批量ping是我的工作中常常需要用到的功能了，但是手动好麻烦！我在网上找到了一个脚本，经过了一些改进现在非常好用了，为了方便自己以后复制和互联网精神，我把它放在这里！

# 特点
- 多个IP并行扫描，速度很快
- 扫描py代码所在目录下所有`.txt`文件，对每个txt文件内的所有IP进行扫描（会自动判断行内容是不是ip哦！目前只支持ipv4）
- 输出上色，更容易看清
- 输出使用tab分割，可以轻松复制到excel进行排序筛选之类的操作


# 代码

```py
import subprocess
import multiprocessing
import  time

def check_alive(ip):
    result = subprocess.call(f'ping -w 1000 -n 2 {ip}', stdout=subprocess.PIPE, shell=True)
    # 等待超时时间1000ms ， 测试次数 2次
    if result == 0:
        h = subprocess.getoutput('ping ' + ip)
        returnnum = h.split('平均 = ')[1]
        print(f'{ip}\t\033[32m[ok]\033[0m\t{returnnum}\t'.replace("\n","") )
    else:
        print(f'{ip}\t\033[31m[bad]\033[0m'.replace("\n",""))


if __name__ == '__main__':
    print('结果使用tab分隔，可以拷贝到excel中，通过数据透视进行ip排序等')
    # 获取所有当前目录下的txt文件并存入 txtfile_list
    import os
    path = "."
    file_name_list = os.listdir(path)
    txtfile_list = []
    for x in file_name_list:
        if x.__contains__('.'):
            if x.split('.')[1] == "txt":
                txtfile_list.append(x)
    print(txtfile_list)

    MUTIPROCESS = True

    for x in txtfile_list:
        print(f"scaning {x} :")
        # input("enter 开始ping")
        with open(x, 'r') as f:  # xxx.txt 内容应该包含ip地址，每行一个，可以写备注因为下面会
            print(f'ipaddress\t[ok]\tlatency\t'.replace("\n", ""))
            for line in f:
                # 识别ip地址
                if len(line.split('.')) == 4:
                    if MUTIPROCESS: # 多线程模式
                        p = multiprocessing.Process(target=check_alive, args=(line,))
                        p.start()
                    else: #单线程模式
                        check_alive(line)
                # 展示非ip行内容
                # else:   print(line)

        # 等待多线程数量为0（ping均结束）后开启下一个txt的扫描
        while True:
            if len(multiprocessing.active_children()) == 0:
                # print('thread count: '+ str(len(multiprocessing.active_children())) +' ,scan complete\n\n')
                print("------------")
                break
            time.sleep(3)

```

# 使用效果
为了避免信息泄露，我这里放的都是一些网络上的服务器，很少…… 
不过我正常使用这个工具的时候都是搞几十个ip来扫


![image](https://image.baidu.com/search/down?url=https://tvax2.sinaimg.cn/large/006rgJELgy1h3cncasc0qj319g0raano.jpg)
![image](https://image.baidu.com/search/down?url=https://tva2.sinaimg.cn/large/006rgJELgy1h3cnhgy70yj30fq0cjdi1.jpg)

# 尾巴
其实我是周末弄得啦，之前就是直接用的网上搜到的版本，但是总是感觉不好用，今天正好有空，就修改了一下。

无论是输出的排版、还是多个txt的支持之类的，我的版本都是比较好的啦！

如果说你有超级多个ip进行测试的话，你可能会发现有的时候一行输出了2个ip，然后下面还有个空行，那也是我很想解决（但是也不会弄）的东西，因为他们是并行开始ping的，没有办法知道他们测试结束的时间，如果他们的结束后print的时间正好卡在一起那就一行两个了。

不过目前也可以通过复制到excel里面然后把很明显串行的结果剪切过去来解决……但是 一点也不优雅！

