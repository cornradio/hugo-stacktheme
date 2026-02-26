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
        # 账号是 k123，后面粘贴你刚才生成的加密字符串
        k123 $2a$14$O27TM4SE4Z3CNYfzZE2FI.7Tk2hRuR1XM3R0hO4YAquBOYopQQiBK
    }
    reverse_proxy localhost:3000
}
```

启动caddy

```
.\caddy run --config Caddyfile
```

http://127.0.0.1:9080/ 可以验证访问。  
他就会弹出密码验证框。