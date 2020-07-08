---
title: "Discuz 论坛自动签到云函数代码"
categories:
  - tutorial
tags:
  - 教程
toc: false
toc_sticky: true
toc_label: "标题"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
最近在网上搜集了很多利用腾讯无服务器云函数（SCF）自动签到的代码，细数一下，已经成功部署了 8 项签到任务。腾讯 scf 的免费额度用来签到完全够用，每个月的费用都是零。不仅解放双手，还完全免费。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200708184413.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200708184413.png"></a> </figure>

其中很多都是 Discuz 论坛签到任务，比如[吾爱破解][1]、[MT 论坛][2]和[爱好论坛][3]。既然都是 Discuz 论坛，那么将代码进行简单的修改，理论上应该能实现所有 Discuz 论坛自动签到。于是我在 [MT 论坛][2]自动签到函数的基础上进行了简单的修改，并测试，结果成功了！

下面是通用签到函数代码，需要修改的有 2 处： `url2`中的 formhash 和 `cookie2` 中的 cookie。[点击查看如何获取 url 和 cookie](#1)。

修改完成后，在 scf 中新建运行环境为 Python3.6 的空白函数，并将以下代码部署进去，设置定时运行即可实现自动签到。

```
# -*- coding: utf8 -*-
import requests
import datetime

url2= 'https://bbs.binmt.cc/k_misign-sign.html?operation=qiandao&format=button&formhash=你的formhash值&inajax=1&ajaxtarget=midaben_sign'
cookie2 = '填入你的cookie'
def it():
    headers = {
        'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36','cookie':cookie2
         }
    res = requests.post(url=url2, headers=headers).text
    print(res)
def main_handler(event, context):
    return it()
if __name__ == '__main__':
    it()
```

<span id="1">获取 url 和 cookie 方法：<span>

登录账号后在签到按钮处右键复制链接，替换函数代码中的 url。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200708190726.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200708190726.png"></a> </figure>

登录账号后在个人中心页面按 **F12** 或右键调出审查元素界面。刷新页面后在 Network 各项中找到账号 cookie 复制填入到函数代码相应位置。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200708193216.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200708193216.png"></a> </figure>

[1]: https://www.52pojie.cn/
[2]: https://bbs.binmt.cc/
[3]: https://www.aihao.cc/forum.php