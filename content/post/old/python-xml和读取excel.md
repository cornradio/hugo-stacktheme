+++
title = "Python Xml和读取excel"
description = ""
date = 2022-08-08T19:35:59+08:00
featured = false
draft = false
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

最近我接到了一个工作，就是把一份很长很长的漏洞扫描报告导入到单位的“测评能手”工具中，但是这个工具不支持导入这个excel表格，所以我要艰难的手动录入。

表格的长度有16000行，是对主机和数据库的漏扫内容，每一行有用的信息如下：	

| 主机        | 漏洞名称   | 危险等级 | 漏洞简述 | 详细描述 |
| ----------- | ---------- | -------- | -------- | -------- |
| xx.xx.xx.xx | xx版本过旧 | 低       | --       | --       |

主机有几百台，包括8个项目所有的主机，每个项目又有一些自己的服务器和DB，他们提供了服务器和DB的ip列表，我的任务就是先把不同的项目的漏洞条目分好，然后通过手工的方式一条一条的导入漏洞

# 把excel数据导入python

## 安装PANDAS

通过pandas可以读取表格的sheet页了：

首先安装pandas、以及读取需要表格依赖openpyxl库：

```sh
pip install pandas -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
pip install openpyxl -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```

# 读取sheet(s)

excel读取的时候需要选定sheet页，所以我们需要先获取sheet名称，

可以通过`for x in sheet_names`来loop整个excel文件。

```py
xpath = input("输入excel文件地址：")
# get all sheet names
sheep_name = pd.ExcelFile(xpath)
sheet_names = sheep_name.sheet_names
```

# 读取XLSX表格

导入pandas库、读取xlsx文件

```python
import pandas as pd
data = pd.read_excel('1.xlsx', sheet_name='Sheet1') #选取文件、要读取的sheet名
print(data)
```

![image](https://tva4.sinaimg.cn/large/006rgJELly1gx9t65s9y4j308703uq3j.jpg)

为了能操作到指定元素，我们需要先了解一下pandas的数据存储格式是什么：

```python
data = {
    	'列头1': ['Akey1', 'Akey2','Akey3'],
        '列头2': ['Bkey1','Bkey2','Bkey3'],
        '列头3': [np.nan, np.nan, np.nan]
       }
```

所以，pandas读取进来的我这个表就是这样的：

```
print(data)
---
   列头1    列头2  列头3
0  Akey1  Bkey1  NaN
1  Akey2  Bkey2  NaN
2  Akey3  Bkey3  NaN
```

获取第一列的值（通过列头名称选择）：

```
print(data['列头1'])
print(data.列头1)
---
0    Akey1
1    Akey2
2    Akey3
```

获取第一行的值（通过列序号选择）：
```
print(data.iloc[0])
---
列头1    Akey1
列头2    Bkey1
列头3      NaN
```

获取第一行的、第一列的值：

```
print(data.iloc[0].列头1)
print(data.iloc[0][0])
---
Akey1
```

获取指定列、第一行的值:

```
print(data['列头1'][0])
print(data.列头1[0])
---
Akey1
```

获取列头2为指定值的列头1内容：

这里比较绕，不过无脑复制就好啦！而且这个取数据方式还是比较有用的。

```
datarow = data.loc[data['列头2'] == 'Bkey1']
print(datarow.列头1)
---
Akey1
```

因为我的excel是数据源，我没有对修改excel和保存做深入研究，只有一句保存语句：

[参考](https://zhuanlan.zhihu.com/p/333560640)

```
data.to_excel(excel_writer='demo.xlsx', sheet_name='sheet_1')
```



## 了解pandas

其实仅仅为了处理excel还是没必要了解pandas了，不过网上写的教学不是很清楚都，所以我还是搜索并了解了pandas才弄明白怎么用。

[pandas c语言中文网](http://c.biancheng.net/pandas/loc-iloc.html)

```python
# 单维度的资料：
import pandas as pd

data = pd.Series([20, 10, 15])
print(data)
print('最大值', data.max())
print('中位数', data.median())

# 所有data*2
data = data * 2
print(data)

# 判定所有的data和20相等
data = data == 20
print(data)
```


```python
# 双维度的资料（表格读取后的效果）：
-------------------
   name  salary
0   amy    3000
1  jhon    5000
2   bob    4000

# 双维度的资料（自定义字典输入pandas）
data2 = pd.DataFrame(
    {
        "name": ['amy', 'jhon', 'bob'],
        "salary": [3000, 5000, 4000]
    }
)
print(data2)
# 取得name列内容
print(data2['name'])
print("=========")
# 取得特定的横向
print(data2.iloc[0])

# data = pd.read_excel('www2.xlsx', sheet_name='Sheet1')
data["name"] # 竖着来的
data.iloc[0] # 横着来的(ilocation - 0,1,2,3,4……)


```

## 过滤

但是有时候我们不知道自己想要的是第几行，比如想要知道amy的工资，要怎么办呢？

`data.loc`可以解决这个问题，比方说你可以提取`1,2`行让表格变成一个更小的表，所以我就可以组合语句，比方说这个地方有10个amy，你接可以拉一个amy表，看看谁的工资比较高。

```python
data2.loc[[1,2]] #返回第2,3行变成的小的表格
data2["name"]=="amy" #返回amy所在行
data_amy = data2.loc[ data2["name"]=="amy" ] #返回amy所在行变成的小的表格
```

## 遍历

```python
#dataInip是我通过想要的ip过滤的漏洞集合，
#获取了data之后我要导入到自己的数据结构中，vul是我的数据结构的一部分，我会作为log进行打印
vulcount = len(list(dataInip['级别']))

for i in range(vulcount):
    vul = [dataInip.iloc[i]['漏洞名称'], dataInip.iloc[i]['简述'], mydict[dataInip.iloc[i]['级别']], dataInip.iloc[i]['描述'], dataInip.iloc[i]['解决方案']]
    print(vul)
```

# 缓存数据

好久没有用python了我就忘记了怎么存储数据了，只会用最简单的变量了，上网简单的查了一下，可以通过这种方式来新建一个自己需要的数据结构:

```python
class ip_and_vuls:
    ip = "123.456.789.456"
    vuls = []

#访问
p1 = ip_and_vuls
p1.ip #123.456.789.456
#唯一的缺点就是用的时候得手动初始化， 用完了最好传出去copy
```

为什么我不用	__init__`初始化函数呢，因为我懒得学，而且这个操作更灵活（也更容易出现自己发现不了的bug）

其实如果写代码逻辑够好的话，这种也没问题，但是逻辑如果糟糕一点就是一坨屎了。

# XML

为什么又说到这里呢，因为我最终的目的就是要把表格的内容转换成有效的xml，就可以直接导入而不用手动粘贴了。

python的各种操作文件是我感觉异常简单的地方，c语言、java开个文件要好几行好复杂，python一行开了，一行输入完成了，一行又关好了。

xml这里我学的不精，能用为主嘛。

```python
import xml.etree.ElementTree as ET

# 获取xml（从外部文件读取）
tree = ET.parse("xmlLearn.xml")
# 获取xml根元素
root = tree.getroot()
# 打印xml（人不可读）
print(ET.tostring(root))
# 为根节点添加值
root.set("launched","2021-11-18 10:23:15")

# 为所有的investor节点添加一个属性 id
id = 1
for investor in tree.findall('investor'):
    investor.set('id',str(id))
    id += 1

# 删除所有investor节点下的id
for investor in tree.findall('investor'):
    del(investor.attrib['id'])
    id += 1

#添加一个节点investor（！重点！）
investor2 = ET.Element('investor')
investor2.text = 'Karl Amber'
root.append(investor2)

# 选择特定investor(xpath看不懂)
investor = root.find(".//investor[@id='4']")
print(investor.text)

# 输出到文件（没有缩进）
tree.write("xmlLearn.xml")

```

![](https://tvax3.sinaimg.cn/large/006rgJELly1gwjmtdp4urj30e307awhc.jpg)

这里我放一个图片希望大家看了可以懂，xml是一个嵌套树的结构，investor是root下面的，然而investor可以自己再有一个子节点（只要append就行了），xml是层级分明的文件结构

不过默认输出有很大的问题啊（我感觉）一是没有缩进，二是不支持中文，我很困扰所以我找到了下面的解决办法，虽然解决了但是要多加两个import了。这两个import都是python自带的，不用安装。

```python
import codecs
from xml.dom import minidom

# 美丽输出xml
f = open("money.xml")
xmlstr = minidom.parseString(ET.tostring(root)).toprettyxml(indent="   ")
with codecs.open("money.xml", "w", "utf-8") as f:
    f.write(xmlstr)
```

对于我来说，我就只要增加节点，给节点加内容、最后按照等保标准导入格式输出一个xml就好了

# 附件

我的成品（私人库主要是有点敏感信息所以就暂时不公开了）[kasusa/exceltodata: -- (github.com)](https://github.com/kasusa/exceltodata)

等级保护漏洞导入用xml格式：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<REPORT>
<SCANINFO TOOLNAME="XXXX" MAKERS="XXXX" POLICY="XXXX" SCANTASK="" SCANTIME="" FILE_ID="" />
<!-- TOOLNAME="扫描工具名称" MAKERS="工具厂商名称" POLICY="策略版本" SCANTASK="任务名称" SCANTIME="扫描时间" FILE_ID="文件ID(没啥大用处其实)" -->

<SCANDATA TYPE="OS">
	<HOST IP="192.168.0.100">    <!-- *IP地址： -->
		<OSTYPE>WINDOWS</OSTYPE> <!--  操作系统类型：Windows、Linux、.... -->
		<OSVERSION>Windows Server 2008</OSVERSION><!--  操作系统版本：Windows 2008、RedHat 9、.... -->
		<DATA>
			<VULNERABLITY>
				<NAME><![CDATA[Microsoft Windows Remote Desktop Protocol Server Man-in-the-Middle Weakness]]></NAME><!-- *漏洞名称： -->
				<NO CVE="CVE-2005-1794" CNVD="CNVD-2005-1794" MS="MS07-111" OTHER="xxxx" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号",没有编号可用NONE标识 -->
				<VULTYPE>缓存区溢出</VULTYPE><!-- 漏洞类型：如缓冲区溢出、设置不当、中间件漏洞、其他等等 -->
				<CVSS>6.4</CVSS><!-- 通用漏洞评分： -->
				<PORT>3389</PORT><!-- 端口： -->
				<RISK>中</RISK><!-- *风险情况：高、中、低、信息 -->
				<SYNOPSIS><![CDATA[It may be possible to get access to the remote host]]></SYNOPSIS><!-- 漏洞简述： -->
				<DESCRIPTION><![CDATA[The remote version of the Remote Desktop Protocol Server (TerminalService) is vulnerable to a man-in-the-middle (MiTM) attack. The RDP]]></DESCRIPTION><!-- *漏洞描述 -->
				<SOLUTION><![CDATA[- Force the use of SSL as a transport layer for this service if supported, or/and]]></SOLUTION><!-- *解决方案/整改意见 -->
				<VALIDATE><![CDATA[XXXXXX]]></VALIDATE><!-- 证据 -->
				<REFERENCE><![CDATA[http://www.oxid.it/downloads/rdp-gbu.pdf]]></REFERENCE>	<!-- 参考信息 -->
			</VULNERABLITY>
			<VULNERABLITY>
				<NAME><![CDATA[Terminal Services Encryption Level is Medium or Low]]></NAME><!-- *漏洞名称： -->
				<NO CVE="CVE-2005-1794" CNVD="CNVD-2005-1794" MS="MS07-111" OTHER="xxxx" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>设置不当</VULTYPE><!-- 漏洞类型：如缓冲区溢出、设置不当、中间件漏洞、其他等等 -->
				<CVSS>6.4</CVSS><!-- 通用漏洞评分： -->
				<PORT>3389</PORT>
				<RISK>中</RISK>>
				<SYNOPSIS><![CDATA[The remote host is using weak cryptography.]]></SYNOPSIS>
				<DESCRIPTION><![CDATA[The remote Terminal Services service is not configured to use strong cryptography.xxxxxxxxxxxxxxxxxxxxx]]></DESCRIPTION>
				<SOLUTION><![CDATA[- Change RDP encryption level to one of :xxxxxxxxxxxxxxxxxx]]></SOLUTION>
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE>
				<REFERENCE><![CDATA[The terminal services encryption level is set to :]]></REFERENCE>	
			</VULNERABLITY>
		</DATA>
	</HOST>
	
	<HOST IP="102.168.20.20">
		<OSTYPE>LINUX</OSTYPE>
		<OSVERSION>RED HAT 9</OSVERSION>
		<DATA>
			<VULNERABLITY>
				<NAME><![CDATA[Microsoft Windows Remote Desktop Protocol Server Man-in-the-Middle Weakness]]></NAME>
				<NO CVE="CVE-2005-1794" CNVD="CNVD-2005-1794" MS="MS07-111" OTHER="xxxx" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>缓存区溢出</VULTYPE><!-- 漏洞类型：如缓冲区溢出、设置不当、中间件漏洞、其他等等 -->
				<CVSS>6.4</CVSS><!-- 通用漏洞评分： -->
				<PORT>3389</PORT>
				<RISK>中</RISK>
				<SYNOPSIS><![CDATA[It may be possible to get access to the remote host]]></SYNOPSIS>
				<DESCRIPTION><![CDATA[The remote version of the Remote Desktop Protocol Server (TerminalService) is vulnerable to a man-in-the-middle (MiTM) attack. The RDP]]></DESCRIPTION>
				<SOLUTION><![CDATA[- Force the use of SSL as a transport layer for this service if supported, or/and]]></SOLUTION>
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE>
				<REFERENCE><![CDATA[http://www.oxid.it/downloads/rdp-gbu.pdf]]></REFERENCE>	
			</VULNERABLITY>
			<VULNERABLITY>
				<NAME><![CDATA[Terminal Services Encryption Level is Medium or Low]]></NAME>
				<NO CVE="CVE-2005-1794" CNVD="CNVD-2005-1794" MS="MS07-111" OTHER="xxxx" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>设置不当</VULTYPE><!-- 漏洞类型：如缓冲区溢出、设置不当、中间件漏洞、其他等等 -->
				<CVSS>6.4</CVSS><!-- 通用漏洞评分： -->
				<PORT>3389</PORT>
				<RISK>中</RISK>
				<SYNOPSIS><![CDATA[The remote host is using weak cryptography.]]></SYNOPSIS>
				<DESCRIPTION><![CDATA[The remote Terminal Services service is not configured to use strong cryptography.xxxxxxxxxxxxxxxxxxxxx]]></DESCRIPTION>
				<SOLUTION><![CDATA[- Change RDP encryption level to one of :xxxxxxxxxxxxxxxxxx]]></SOLUTION>
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE>
				<REFERENCE><![CDATA[The terminal services encryption level is set to :]]></REFERENCE>	
			</VULNERABLITY>
		</DATA>
	</HOST>
</SCANDATA>

<SCANDATA TYPE="DB">
	<HOST IP="102.168.20.20">
		<PORT>1433</PORT>
		<DBTYPE>Microsoft SQL Server</DBTYPE>
		<DBVERSION>Microsoft SQL Server 2008 R2</DBVERSION>
		<DATA>
			<VULNERABLITY> 
				<NAME><![CDATA[Easily-guessed password]]></NAME><!-- *漏洞名称： -->
				<NO CVE="NONE" CNVD="NONE" MS="NONE" OTHER="NONE" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>弱口令</VULTYPE><!-- 漏洞类型：如缓冲区溢出、设置不当、弱口令、其他等等 -->
				<RISK>高</RISK><!-- *风险情况：高、中、低、信息 -->
				<SYNOPSIS><![CDATA[It may be possible to get access to the remote host]]></SYNOPSIS><!-- 漏洞简述： -->
				<DESCRIPTION><![CDATA[The remote version of the Remote Desktop Protocol Server (TerminalService) is vulnerable to a man-in-the-middle (MiTM) attack. The RDP]]></DESCRIPTION><!-- *漏洞描述 -->
				<SOLUTION><![CDATA[- Force the use of SSL as a transport layer for this service if supported, or/and]]></SOLUTION><!-- *解决方案/整改意见 -->
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE><!-- 证据 -->
				<REFERENCE><![CDATA[http://www.oxid.it/downloads/rdp-gbu.pdf]]></REFERENCE>	 <!-- 参考信息 -->
			</VULNERABLITY>
			<VULNERABLITY>
				<NAME><![CDATA[Terminal Services Encryption Level is Medium or Low]]></NAME><!-- *漏洞名称： -->
				<NO CVE="NONE" CNVD="NONE" MS="MS13-112" OTHER="NONE" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>设置不当</VULTYPE><!-- 漏洞类型：如缓冲区溢出、设置不当、弱口令、其他等等 -->
				<RISK>中</RISK>
				<SYNOPSIS><![CDATA[The remote host is using weak cryptography.]]></SYNOPSIS>
				<DESCRIPTION><![CDATA[The remote Terminal Services service is not configured to use strong cryptography.xxxxxxxxxxxxxxxxxxxxx]]></DESCRIPTION>
				<SOLUTION><![CDATA[- Change RDP encryption level to one of :xxxxxxxxxxxxxxxxxx]]></SOLUTION>
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE><!-- 证据 -->
				<REFERENCE><![CDATA[The terminal services encryption level is set to :]]></REFERENCE>	
			</VULNERABLITY>
		</DATA>
	</HOST>
	
	<HOST IP="102.168.100.11">
		<PORT>1433</PORT>
		<DBTYPE>Microsoft SQL Server</DBTYPE>
		<DBVERSION>Microsoft SQL Server 2008 R2</DBVERSION>
		<DATA>
			<VULNERABLITY>
				<NAME><![CDATA[Easily-guessed password]]></NAME> <!-- *漏洞名称： -->
				<NO CVE="NONE" CNVD="NONE" MS="NONE" OTHER="NONE" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>弱口令</VULTYPE><!-- 漏洞类型：如缓冲区溢出、设置不当、弱口令、其他等等 -->
				<CVSS>6.4</CVSS><!-- 通用漏洞评分： -->
				<RISK>高</RISK><!-- *风险情况：高、中、低、信息 -->
				<SYNOPSIS><![CDATA[It may be possible to get access to the remote host]]></SYNOPSIS><!-- 漏洞简述： -->
				<DESCRIPTION><![CDATA[The remote version of the Remote Desktop Protocol Server (TerminalService) is vulnerable to a man-in-the-middle (MiTM) attack. The RDP]]></DESCRIPTION><!-- *漏洞描述 -->
				<SOLUTION><![CDATA[- Force the use of SSL as a transport layer for this service if supported, or/and]]></SOLUTION><!-- *解决方案/整改意见 -->
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE><!-- 证据 -->
				<REFERENCE><![CDATA[http://www.oxid.it/downloads/rdp-gbu.pdf]]></REFERENCE>	 <!-- 参考信息 -->
			</VULNERABLITY>
			<VULNERABLITY>
				<NAME><![CDATA[Terminal Services Encryption Level is Medium or Low]]></NAME> 
				<NO CVE="NONE" CNVD="NONE" MS="MS13-112" OTHER="NONE" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>弱口令</VULTYPE><!-- 漏洞类型：如缓冲区溢出、设置不当、弱口令、其他等等 -->
				<CVSS>6.4</CVSS><!-- 通用漏洞评分： -->
				<RISK>中</RISK>
				<SYNOPSIS><![CDATA[The remote host is using weak cryptography.]]></SYNOPSIS>
				<DESCRIPTION><![CDATA[The remote Terminal Services service is not configured to use strong cryptography.xxxxxxxxxxxxxxxxxxxxx]]></DESCRIPTION>
				<SOLUTION><![CDATA[- Change RDP encryption level to one of :xxxxxxxxxxxxxxxxxx]]></SOLUTION>
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE><!-- 证据 -->
				<REFERENCE><![CDATA[The terminal services encryption level is set to :]]></REFERENCE>	
			</VULNERABLITY>
		</DATA>
	</HOST>
</SCANDATA>

<SCANDATA TYPE="WEB">
	<HOST WEB="HTTP:\\WWW.TEST.COM">
		<WEBSERVERBANNER>Apache tomcat</WEBSERVERBANNER><!-- Web Server Banner信息， -->
		<SERVERVERSION>Microsoft Windows 2008 R2</SERVERVERSION><!-- 服务器信息 -->
		<TECHNOLOGIES>JSP</TECHNOLOGIES><!-- 使用语言 -->
		<DATA>		
			<VULNERABLITY>
				<NAME><![CDATA[SQL注入漏洞]]></NAME> <!-- *漏洞名称： -->
				<NO CVE="NONE" CNVD="NONE" MS="NONE" OTHER="NONE" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>注入类</VULTYPE><!-- 漏洞类型：如注入类、跨站脚本类、信息泄露类、弱口令/默认口令类、系统/服务漏洞类、权限/配置设置不当类、产品漏洞类、其他类 -->
				<RISK>高</RISK><!-- *风险情况：高、中、低、信息 -->
				<SYNOPSIS><![CDATA[It may be possible to get access to the remote host]]></SYNOPSIS><!-- 漏洞简述： -->
				<DESCRIPTION><![CDATA[The remote version of the Remote Desktop Protocol Server (TerminalService) is vulnerable to a man-in-the-middle (MiTM) attack. The RDP]]></DESCRIPTION><!-- *漏洞描述 -->
				<SOLUTION><![CDATA[- Force the use of SSL as a transport layer for this service if supported, or/and]]></SOLUTION><!-- *解决方案/整改意见 -->
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE><!-- 证据 -->
				<REFERENCE><![CDATA[http://www.oxid.it/downloads/rdp-gbu.pdf]]></REFERENCE>	 <!-- 参考信息 -->
				<DETAILS>
					<URL URL="HTTP:\\WWW.TEST.COM?DETAILS=100"><!-- *存在漏洞的url -->
						<TYPE>STRING</TYPE><!-- 类型（string类型、int类型、search类型、反射性、存储型等等） -->
						<PARAMETER><![CDATA[DETAILS=100' AND '1'='1]]></PARAMETER><!-- 存在漏洞的参数（可带测试脚本） -->
						<REQUEST><![CDATA[GET /preSysApp/global/js/validate/depends/prototype.js HTTP/1.1
								 Pragma: no-cache
								 Cache-Control: no-cache]]>
						</REQUEST><!-- 测试发送的request -->
						<RESPONSE><!-- 接收的request -->
						<![CDATA[
						xxxxxxxxxxxxxxxxxx
						]]>
						</RESPONSE>
					</URL>
					<URL URL="HTTP:\\WWW.TEST.COM?id=120"><!-- *存在漏洞的url -->
						<TYPE>INT</TYPE><!-- 类型（string类型、int类型、search类型、反射性、存储型等等） -->
						<PARAMETER><![CDATA[ID=100 AND 1=1]]></PARAMETER><!-- 存在漏洞的参数（可带测试脚本） -->
						<REQUEST><![CDATA[GET /preSysApp/global/js/validate/depends/prototype.js HTTP/1.1
								 Pragma: no-cache
								 Cache-Control: no-cache]]>
						</REQUEST><!-- 测试发送的request -->
						<RESPONSE>
						<![CDATA[xxxxxxxxxxxxxxxxxx]]>
						</RESPONSE><!-- 接收的request -->
					</URL>
				</DETAILS>
			</VULNERABLITY>	
			<VULNERABLITY>
				<NAME><![CDATA[跨站脚本]]></NAME> <!-- *漏洞名称： -->
				<NO CVE="NONE" CNVD="NONE" MS="NONE" OTHER="NONE" />
				<!-- CVE="CVE编号" CNVD="CNVD编号" MS="微软编号" OTHER="其他编号" -->
				<VULTYPE>跨站脚本类</VULTYPE><!-- 漏洞类型：如注入类、跨站脚本类、信息泄露类、弱口令/默认口令类、系统/服务漏洞类、权限/配置设置不当类、产品漏洞类、其他类 -->
				<RISK>高</RISK><!-- *风险情况：高、中、低、信息 -->
				<SYNOPSIS><![CDATA[It may be possible to get access to the remote host]]></SYNOPSIS><!-- 漏洞简述： -->
				<DESCRIPTION><![CDATA[The remote version of the Remote Desktop Protocol Server (TerminalService) is vulnerable to a man-in-the-middle (MiTM) attack. The RDP]]></DESCRIPTION><!-- *漏洞描述 -->
				<SOLUTION><![CDATA[- Force the use of SSL as a transport layer for this service if supported, or/and]]></SOLUTION><!-- *解决方案/整改意见 -->
				<VALIDATE><![CDATA[XXXXX]]></VALIDATE><!-- 证据 -->
				<REFERENCE><![CDATA[http://www.oxid.it/downloads/rdp-gbu.pdf]]></REFERENCE>	 <!-- 参考信息 -->
				<DETAILS>
					<URL URL="HTTP:\\WWW.TEST.COM?DETAILS=100"><!-- *存在漏洞的url -->
						<TYPE>反射性</TYPE><!-- 类型（string类型、int类型、search类型、反射性、存储型等等） -->
						<PARAMETER><![CDATA[DETAILS=100%20%3C%73%63%72%69%70%3E%61%6C%65%72%74%28%31%29%3C%2F%73%63%72%69%70%74%3E]]></PARAMETER><!-- 存在漏洞的参数（可带测试脚本） -->
						<REQUEST><![CDATA[GET /preSysApp/global/js/validate/depends/prototype.js HTTP/1.1
								 Pragma: no-cache
								 Cache-Control: no-cache]]>
						</REQUEST><!-- 测试发送的request -->
						<RESPONSE><!-- 接收的request -->
						<![CDATA[xxxxxxxxxxxxxxxxxx]]>
						</RESPONSE>
					</URL>
				</DETAILS>
			</VULNERABLITY>
		</DATA>
	</HOST>
</SCANDATA>
</REPORT>
```

---

python能提取excel还能处理，我就很开心了，还学到了xml相关的内容。

今天花了5小时把上面所有东东从0学完，到直接把工具做好我感觉也够神的了我）
