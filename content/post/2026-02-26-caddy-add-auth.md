---
title: 用caddy给任何服务加一层密码防护 # 标题
slug: caddy-add-auth # url(注释掉 和标题相同)
image: https://wcp.cornradio.org/images/caddy/image.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2026-02-26 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fcaddy-add-auth&label=&icon=check-all&color=%23198754)


> 最近 coding 的频率比较高，写了很多的web程序,但是他们都没有任何的密码保护.  
> 网上搜到用 [authlia](https://www.authelia.com/) 帖子比较多 , 但是我研究了一下，发现他非常复杂, 还需要借助npm（nginx proxy manager）等工具来实现代理转发。  
> 我请教了一下 ai, 他说 caddy 支持反向代理和基本认证功能，可以很方便地给任何服务加一层密码防护,我用了一下感觉确实很方便。  


> 下面的教程是关于如何使用 [caddy](https://caddyserver.com/download) 给一个本地的服务(http://localhost:3000) 加一层密码保护。


## 原理说明与本地测试
使用 [caddy](https://caddyserver.com/download) 制作一个密码哈希字符串，命令行输入：
```
.\caddy.exe hash-password --plaintext <YOURPASSWORD>

$2a$14$O27TM4SE4Z3CNYfzZE2FI.7Tk2hRuR1XM3R0hO4YAquBOYopQQiBK
```

在 Caddy 程序所在的目录下，新建一个文本文档，名字改叫 `Caddyfile`（不要有 .txt 后缀），内容如下：

```
#要的访问端口（http）
:9080 {
    basic_auth {
        # 账号是 admin，后面粘贴你刚才生成的加密字符串
        admin $2a$14$O27TM4SE4Z3CNYfzZE2FI.7Tk2hRuR1XM3R0hO4YAquBOYopQQiBK
    }
    reverse_proxy localhost:3000
}
```

启动caddy

```
.\caddy run --config Caddyfile
```

<http://127.0.0.1:9080/> 可以发现转发成功，且需要输入密码进入。  


## Caddy 完整版安装与配置手册

> centos 版本
### 1. 下载并替换二进制文件

由于 `yum` 版功能不全，直接从官方拉取最新全功能版：

```bash
# 下载 64 位 Linux 官方包
curl -L "https://caddyserver.com/api/download?os=linux&arch=amd64" -o /usr/bin/caddy

# 授权
chmod +x /usr/bin/caddy

# 检查 basic_auth 模块是否完整 
caddy list-modules | grep http.handlers.authentication

```

### 2. 创建极简配置文件

如果 `/etc/caddy` 目录不存在则先创建：`mkdir -p /etc/caddy`。

```bash
cat <<'EOF' > /etc/caddy/Caddyfile
:3001 {
	# 账号 admin，密码用 caddy hash-password <your-password>生成
    basic_auth * {
        admin $2a$14$O27TM4SE4Z3CNYfzZE2FI.7Tk2hRuR1XM3R0hO4YAquBOYopQQiBK
    }
    # 反向代理到你的后端
    reverse_proxy localhost:3000
}
EOF

```
可以添加多个，直接复制粘贴多搞几个就行了。

### 3. 配置 Systemd 系统服务

让 Caddy 支持后台运行、自启动和 `systemctl` 管理：

```bash
cat <<EOF > /etc/systemd/system/caddy.service
[Unit]
Description=Caddy Service
After=network.target

[Service]
Type=notify
ExecStart=/usr/bin/caddy run --environ --config /etc/caddy/Caddyfile
ExecReload=/usr/bin/caddy reload --config /etc/caddy/Caddyfile --force
Restart=on-failure

[Install]
WantedBy=multi-user.target
EOF

```

### 4. 启动并验证

```bash
# 加载并启动
systemctl daemon-reload
systemctl enable --now caddy

# 检查状态
systemctl status caddy
```

---

### 常用运维指令速查表

| 操作          | 命令                                             |
| ----------- | ---------------------------------------------- |
| **修改配置后生效** | `caddy reload --config /etc/caddy/Caddyfile`   |
| **查看实时日志**  | `journalctl -u caddy -f`                       |
| **生成新密码哈希** | `caddy hash-password --plaintext "你的新密码"`      |
| **检查配置语法**  | `caddy validate --config /etc/caddy/Caddyfile` |


### 效果展示
![tupina](https://wcp.cornradio.org/images/caddy/image-1.png)


## 其他caddy用法

### fileserver

```
caddy file-server --browse --listen :8080
```
界面比python的 http.server 好看很多，支持目录浏览和文件下载。

![图片](https://wcp.cornradio.org/images/caddy/image-2.png)

### md阅读站

此方法可以极简启动一个支持markdown渲染的文件服务器，适合在本地快速浏览文档或者笔记。甚至可以当一个简单的博客。

其中包含两部分核心功能：
1. `templates` 模块：它允许我们在响应中使用模板语法，动态生成 HTML 内容。我们利用这个功能来把 Markdown 文件渲染成 HTML。
2. `markdown` 函数：这是 Caddy 内置的一个函数，可以把 Markdown 文本转换成 HTML。我们在模板中调用它来渲染 Markdown 文件的内容。
3. `fileserver` 模块：提供静态文件服务和目录浏览功能。

```bash
#caddy run --config ./Caddyfile 
:8080 {
    root * .
    encode zstd gzip

    templates {
        mime .md text/html
    }

    route {
        @markdown {
            path *.md
            file
        }
        
        handle @markdown {
            header Content-Type "text/html; charset=utf-8"
            
            respond `
            <!DOCTYPE html>
            <html>
            <head>
                <meta charset="UTF-8">
                <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/github-markdown-css/github-markdown.min.css">
                <style>
                    body { background-color: #151515; margin: 1em; }
                </style>
            </head>
            <body>
                <div class="nav"><div class="nav-content"><a href="/">⬅</a></div></div>
                <article class="markdown-body">
                    {{ include .Req.URL.Path | markdown }}
                </article>
            </body>
            </html>
            `
        }

        file_server browse
    }
}
```

![blog](https://wcp.cornradio.org/images/caddy/image-3.png)