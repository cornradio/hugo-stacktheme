---
title: nginx配置https(certbot) # 标题
date: 2024-03-26 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
slug: nginxhttpswithcertbot # url(注释掉 和标题相同)
# description: xxxx # 描述小字(注释掉 不显示描述)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)
image: certbot.jpg # 头图，注释掉，否则会有一个难看的呃加载不出来的图片

tags: # 只能在侧面看到的标签,会显示在文章的底部
    - nginx
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---



## 安装nginx
```
apt install nginx -y
```

nginx 默认html文件位置
```
/var/www/html/
```

## 用certbot自动配置

[certbot](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal)

用certbot安装会需要输入邮箱，但是其他的都是自动化的，很方便。

```
sudo snap install --classic certbot

#测试安装，不消耗额度,但是证书会提示有危险(私签)
sudo certbot --nginx  --test-cert
#真实安装
sudo certbot --nginx 
```

### 重启nginx
```
nginx -t
sudo systemctl restart nginx
```
## 开启防火墙允许

```
ufw allow 443
```