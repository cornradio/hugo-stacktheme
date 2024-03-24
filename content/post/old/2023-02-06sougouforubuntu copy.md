+++
title = "install sougou for ubuntu"
description = ""
date = 2023-02-06T14:21:50+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "ubuntu"
]
series = []
images = []
+++

## install sougou for ubuntu
[you can follow this guide](https://shurufa.sogou.com/linux/guide)

## download and install
download sougou [here](https://shurufa.sogou.com/linux)

fix every thing sougou need 
```
sudo apt install fcitx
sudo cp /usr/share/applications/fcitx.desktop /etc/xdg/autostart/
sudo apt purge ibus
sudo apt install libqt5qml5 libqt5quick5 libqt5quickwidgets5 qml-module-qtquick2
sudo apt install libgsettings-qt1
```

install the package again
```
sudo dpkg -i sougou...deb
```
reboot


## settings and stuff
goto`ubuntu settings` - `Region & Language` - `Manage installed Languages` 

choose fcitx 

goto `fcitx configuration` , search for sougoupinyin and add it
