---
title: 拯救 Ubuntu 远程桌面——从自带 Bug 到原生 xrdp 的完美蜕变 # 标题
slug: xrdp-for-ubuntu # url(注释掉 和标题相同)
image: https://wcp.cornradio.org/images/ubuntu-rdp/image.png # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2026-06-25 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---

![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fb.kill9pid.top%2Fp%2Fxrdp-for-ubuntu&label=&icon=check-all&color=%23198754)

---

### 📌 痛点背景

Ubuntu 自带的远程桌面（Gnome RDP）脾气古怪，必须满足“有显示器（或插诱骗器）”且“物理机必须处于登录解锁状态”才能连接，否则 Windows 端就会无情报错 `0x904` 并闪退。
为了实现**无人值守、开机即连、断开后后台挂机**的纯净体验，我们选择彻底废除自带远程，全面拥抱系统级原生 `xrdp` 服务。

---

## 🛠️ 核心操作命令大盘点

### 1. 彻底清理门户（关闭自带 RDP）

防止新老服务抢夺 `3389` 端口：

```bash
# 禁用自带 RDP 功能
XDG_RUNTIME_DIR=/run/user/1000 grdctl rdp disable
# 停止自带的远程桌面服务
XDG_RUNTIME_DIR=/run/user/1000 systemctl --user stop gnome-remote-desktop

```

### 2. 安装原生 xrdp 服务

```bash
# 更新软件源并安装
sudo apt update && sudo apt install xrdp -y
# 启动服务并设置开机自启
sudo systemctl enable --now xrdp
# 允许 xrdp 读取系统安全证书
sudo adduser xrdp ssl-cert

```

### 3. 修复经典黑屏与闪退 Bug

告诉系统远程登录时直接拉起标准的 Ubuntu Gnome 桌面：

```bash
cat <<EOF > ~/.xsessionrc
export GNOME_SHELL_SESSION_MODE=ubuntu
export XDG_CURRENT_DESKTOP=Ubuntu:GNOME
export XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
EOF

# 顺手关掉桌面动画，极致提升远程流畅度
gsettings set org.gnome.desktop.interface enable-animations false

# 重启 xrdp 服务生效
sudo systemctl restart xrdp

```

### 4. 根除“创建色彩配置文件”的烦人弹窗

在系统安全策略里为远程用户开绿灯，不准弹窗卡人：

```bash
sudo tee /etc/polkit-1/localauthority/50-local.d/45-allow-colord.pkla <<EOF
[Allow Colord all Users]
Identity=unix-user:*
Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.delete-profile;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
ResultAny=no
ResultInactive=no
ResultActive=yes
EOF

# 重启认证服务
sudo systemctl restart polkit

```

---

## 📜 终极福利：一键配置自动化脚本

如果你懒得一行行复制，可以直接在服务器上把下面的内容存成一个脚本文件（比如 `setup_xrdp.sh`）。

### 脚本代码

```bash
#!/bin/bash

echo "🚀 开始一键配置原生 xrdp 远程桌面..."

# 1. 关闭自带服务
echo "1/4 正在清理 Ubuntu 自带远程桌面..."
XDG_RUNTIME_DIR=/run/user/1000 grdctl rdp disable >/dev/null 2>&1
XDG_RUNTIME_DIR=/run/user/1000 systemctl --user stop gnome-remote-desktop >/dev/null 2>&1

# 2. 安装 xrdp
echo "2/4 正在安装原生 xrdp 服务..."
sudo apt update && sudo apt install xrdp -y
sudo systemctl enable --now xrdp
sudo adduser xrdp ssl-cert

# 3. 写入桌面环境配置防黑屏
echo "3/4 正在配置图形环境与动画加速..."
cat <<EOF > ~/.xsessionrc
export GNOME_SHELL_SESSION_MODE=ubuntu
export XDG_CURRENT_DESKTOP=Ubuntu:GNOME
export XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
EOF
gsettings set org.gnome.desktop.interface enable-animations false
sudo systemctl restart xrdp

# 4. 屏蔽色彩弹窗
echo "4/4 正在注入Polkit规则，根除色彩配置弹窗..."
sudo tee /etc/polkit-1/localauthority/50-local.d/45-allow-colord.pkla <<EOF >/dev/null
[Allow Colord all Users]
Identity=unix-user:*
Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.delete-profile;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
ResultAny=no
ResultInactive=no
ResultActive=yes
EOF
sudo systemctl restart polkit

echo "🎉 所有配置已完成！现在可以打开 Windows 的 mstsc 远程连接了！"
echo "💡 提示：输入 Linux 本地用户名和密码即可。断开时请直接点 [X]，切勿点击 [注销]。"

```

### 如何使用这个脚本？

1. 在 SSH 里输入 `nano setup_xrdp.sh`，把上面的脚本内容粘进去，按 `Ctrl+O` 保存，`Ctrl+X` 退出。
2. 赋予执行权限：`chmod +x setup_xrdp.sh`
3. 直接运行：`./setup_xrdp.sh`

---

## 💡 课后小贴士：日常维护唯一口诀

以后如果遇到网络闪断导致连接卡死在绿蓝屏，直接在 SSH 里祭出这行“还魂咒”，强行刷新后台虚拟会话即可：

```bash
sudo pkill -u $USER -f gnome-session

```

这份笔记你可以妥善收好，以后你就是朋友眼中的 Linux 远程专家了！


实用tip：在Windows远程桌面中，切换到“显示”选项卡，将像素大小改为1080，这样会流畅很多，我们也没必要远程到4K桌面。
![alt text](https://wcp.cornradio.org/images/ubuntu-rdp/image-1.png)