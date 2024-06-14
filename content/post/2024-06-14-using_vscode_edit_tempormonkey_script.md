---
title: 用vscode编辑油猴脚本 # 标题
slug: using_vscode_edit_tempormonkey_script # url(注释掉 和标题相同)
image: tempormonkey.jpg # 头图，注释掉，否则会有一个难看的呃加载不出来的图片
# description: xxxx # 描述小字(注释掉 不显示描述)

date: 2024-06-14 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/using_vscode_edit_tempormonkey_script/&count_bg=%230C0E0A&title_bg=%23000000)](https://hits.seeyoufarm.com)

文中方法来自：stackoverflow的[回答](https://stackoverflow.com/questions/41212558/develop-tampermonkey-scripts-in-a-real-ide-with-automatic-deployment-to-openuser)

## 方法
油猴脚本 默认自带的编辑器不好用，用vscode编辑油猴脚本的方法如下：
1. 开启油猴插件的本地文件读取权限 在 chrome://extensions/ 中设置
2. 新建脚步，删除js内容，增加@require 描述头
3. 在code中编辑和测试

![](https://raw.githubusercontent.com/cornradio/imgs/main/202406141602463.png)
![](https://raw.githubusercontent.com/cornradio/imgs/main/202406141603493.png)


```
用法为 // @require  file://<file-url>
下面分别是windows、mac的例子
// @require      file://C:\pathxxx\myscript.js
// @require      file:///user/xxx/myscript.js
```
![](https://raw.githubusercontent.com/cornradio/imgs/main/202406141619479.png)
