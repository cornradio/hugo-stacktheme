---
title: 把 frpc 变成 systemd 服务，开机自启 + 崩溃自动重启 # 标题
slug: frp-service # url(注释掉 和标题相同)
image: https://wcp.cornradio.org/images/ubuntu-rdp/image-2.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2026-06-29 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Ffrp-service&label=&icon=check-all&color=%23198754)


之前一直用 screen 跑 frpc，手滑关掉就断了。改成 systemd 服务后：

* 开机自动启动
* 进程挂了 5 秒后自动重启
* 用 `systemctl` 统一管理，不用再记 screen 会话名

## 一键部署脚本

把 `FRP_DIR` 改成你实际的 frp 安装目录，然后跑一遍就行：

    # 你的 frp 安装目录，改成实际路径
    FRP_DIR=/home/kasusa/frp_0.60.0_linux_amd64
    
    sudo tee /etc/systemd/system/frpc.service << EOF
    [Unit]
    Description=FRP Client
    After=network.target
    
    [Service]
    Type=simple
    User=$(whoami)
    WorkingDirectory=${FRP_DIR}
    ExecStart=${FRP_DIR}/frpc -c ${FRP_DIR}/frpc.toml
    Restart=always
    RestartSec=5s
    
    [Install]
    WantedBy=multi-user.target
    EOF
    
    sudo systemctl daemon-reload
    sudo systemctl enable --now frpc

## 如果后续手动修改路径

直接编辑 service 文件：

    sudo nano /etc/systemd/system/frpc.service

需要改的地方就两行：

    WorkingDirectory=/你的frp目录
    ExecStart=/你的frp目录/frpc -c /你的frp目录/frpc.toml

改完后重新加载：

    sudo systemctl daemon-reload
    sudo systemctl restart frpc

## 日常管理

    sudo systemctl status frpc     # 查看状态
    sudo systemctl stop frpc       # 停止
    sudo systemctl start frpc      # 启动
    sudo systemctl restart frpc    # 重启
    journalctl -u frpc -f          # 实时日志

## 是的，它会自启动

`systemctl enable` 已经把 frpc 加入了开机自启。服务器重启后会自动拉起，不用手动进 screen 了。