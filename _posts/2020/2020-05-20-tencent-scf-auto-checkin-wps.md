---
title: "利用腾讯云函数实现 WPS 每日自动打卡"
categories:
  - tutorial
tags:
  - 教程
toc: true
toc_sticky: true
toc_label: "WPS 自动打卡教程"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
WPS 对于很多人来说是一款必不可少的办公软件，除了完善的 办公四件套[^1] 之外，注册用户还可获得 1G 的云存储空间，能多平台同步，用起来很方便。但是对于我这种云存储重度用户，免费的云存储空间根本不够用。

还好，WPS 够良心，有一个签到送会员的活动。只需要每天 `6:00~13:00` 在微信小程序 `WPS 会员` 中签到就能免费获得会员天数。WPS 会员用户云存储空间有 100G，足够日常使用了。但是每天去小程序打卡太麻烦，这里我就用腾讯云函数实现 WPS 每天自动打卡获得会员，完全解放双手。

## 获取 WPS sid 和邀请 id
### 获取 sid
电脑浏览器无痕窗口打开下方链接登录账号,点击签到。

[右键复制链接](https://zt.wps.cn/2018/clock_in?csource=pc_clock_oldactivity)

签到完成后，按 F12 进入检查模式，选择 Network 并勾选下面 Preserve log 选项，之后刷新网页。网页刷新完成后，在检查窗口依次点击各项，在详细页面查找账号 cookie，复制保存 `wps_sid=` 后面的内容，这就是我们要的 sid。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520160509.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520160509.png"></a> </figure>

### 获取邀请 id
点击签到页面左侧分享按钮，复制分享链接，链接中最后面一串数字就是你的邀请 id，类似于 `490164639`。

## 获取 sckey
sckey 是用于微信接收 [Server 酱][1] 发送到签到成功通知的，每次函数运行成功，你都会在微信收到 [Server 酱][1] 发来的消息。点击 [此处][1] 按照 [Server 酱][1] 页面提示申请 sckey。

## <span id="jump">上传 SCF 代码</span>
- [点击下载 SCF 代码](https://haha.lanzous.com/ictxhlc)
- 登录 [腾讯云函数控制台](https://console.cloud.tencent.com/scf)（第一次使用可能需要激活，按步骤激活就可以）。
- 选择 **函数服务** → **新建**，依次设置函数名称、运行环境和创建方式。运行环境选择 `Nodejs 10.15`，创建方式选择 `空白函数`。点击下一步。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520163156.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520163156.png"></a> </figure>

- 提交方法选择 `本地上传 zip 包`，在函数代码处点击上传，选择下载好的 [SCF 代码文件](#jump)，点击完成。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520171027.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520171027.png"></a> </figure>

## 修改 SCF 代码
点击函数代码，选择 `index.js`，依次把前面获取到的 sckey 、 sid 和邀请 id 填入到相应引号中间。修改完成后点击保存。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520165145.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520165145.png"></a> </figure>

## 设置函数运行事件
进入触发管理页面，创建触发器。触发方式选择定时触发，触发周期选择自定义触发周期，Cron 表达式填 `0 0 6 * * * *` 意思是每天早晨 6 点签到。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520165948.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200520165948.png"></a> </figure>

至此，腾讯云函数自动打卡就已经设置完成了。接下来就是等着程序第二天自动帮你打卡了:smile:


[^1]: 办公四件套：WPS 文字、WPS 表格、WPS 演示、金山 PDF
[1]: http://sc.ftqq.com/3.version