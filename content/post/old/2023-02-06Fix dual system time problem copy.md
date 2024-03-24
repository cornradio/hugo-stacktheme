+++
title = "Fix dual system time problem"
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
## Fix dual system time problem

fix a dual system bug : windows time not right everytime after using ubuntu.

run this in ubuntu
```
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```


## why having this problem

there a hardware called RTC in your computer:

if RTC time is 00:00 , and you are in UTC+8:00 time zone ,

`windows think `: ok ,RTC time is just right : now is 00:00

`ubuntu think `: RTC time is UTC+0:00 so i have to add 8 hours and now is 08:00

command make ubuntu think in windows way.