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
>2020年7月17日 更新：由于官方限制，目前需要手动在小程序打卡，邀请仍可用。
>
>2021年2月23日 更新：修改腾讯云函数

WPS 对于很多人来说是一款必不可少的办公软件，除了完善的 办公四件套[^1] 之外，注册用户还可获得 1G 的云存储空间，能多平台同步，用起来很方便。但是对于我这种云存储重度用户，免费的云存储空间根本不够用。

还好，WPS 够良心，有一个签到送会员的活动。只需要每天 **6:00~13:00** 在微信小程序 **WPS 会员** 中签到就能免费获得会员天数。WPS 会员用户云存储空间有 100G，足够日常使用了。但是每天去小程序打卡太麻烦，这里我就用腾讯云函数实现 WPS 每天自动打卡获得会员，完全解放双手。

## 获取 WPS sid 和邀请 id
### 获取 sid
电脑浏览器无痕窗口打开下方链接登录账号,点击签到。

[右键复制链接](https://zt.wps.cn/2018/clock_in)

签到完成后，按 F12 进入检查模式，选择 Network 并勾选下面 Preserve log 选项，之后刷新网页。网页刷新完成后，在检查窗口依次点击各项，在详细页面查找账号 cookie，复制保存 `wps_sid=` 后面的内容，这就是我们要的 sid。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200520160509.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200520160509.png"></a> </figure>

### 获取邀请 id
点击签到页面左侧分享按钮，复制分享链接，链接中最后面一串数字就是你的邀请 id，类似于 `490164639`。

## 获取 sckey
sckey 是用于微信接收 [Server 酱][1] 发送到签到成功通知的，每次函数运行成功，你都会在微信收到 [Server 酱][1] 发来的消息。点击 [此处][1] 按照 [Server 酱][1] 页面提示申请 sckey。

## 创建腾讯云函数
- 登录 [腾讯云函数控制台](https://console.cloud.tencent.com/scf)（第一次使用可能需要激活，按步骤激活就可以）。
- 选择 **函数服务** → **新建** → **自定义创建**，依次设置函数名称、运行环境和执行超时时间。运行环境选择 **Python3.6**，执行超时时间设置为 **150**，点击下一步。

[![20210223102036](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210223102036.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210223102036.png)

执行超时时间在 **新建函数** 页面下方 **高级配置** 里，必须设置为 **150**

[![20210223102538](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210223102538.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210223102538.png)

## 云函数代码
点击函数代码，选择 `index.py`，把下方代码 `# 初始化信息` 部分修改后填入框内。部署并测试。

```
# !/usr/bin/env python
# coding=utf-8
import requests
import pytz
import datetime
from io import StringIO
import time

# 初始化信息
SCKEY = 'xxxxxxxxxxxxxxxxxxxxxxxx'  # '*********复制SERVER酱的SCKEY进来*************(保留引号)'
data = {
    "wps_invite": [
        {
            "name": "WPS 签到",
            "invite_userid": 490164639,  # "*********填入邀请id*************(不保留双引号)",
            "sid": "xxxxxxxxxx"  # 填入sid(保留引号)
        }
    ]
}
# 初始化日志
sio = StringIO('WPS签到日志\n\n')
sio.seek(0, 2)  # 将读写位置移动到结尾
s = requests.session()
tz = pytz.timezone('Asia/Shanghai')
nowtime = datetime.datetime.now(tz).strftime("%Y-%m-%d %H:%M:%S")
sio.write("--------------------------" + nowtime + "----------------------------\n\n")


# 微信推送
def pushWechat(desp, nowtime):
    ssckey = SCKEY
    send_url = 'https://sc.ftqq.com/' + ssckey + '.send'
    if '失败' in desp:
        params = {
            'text': 'WPS小程序签到失败提醒' + nowtime,
            'desp': desp
        }
    else:
        params = {
            'text': 'WPS小程序签到提醒' + nowtime,
            'desp': desp
        }
    requests.post(send_url, params=params)


# 主函数
def main():
    wps_inv = data['wps_invite']
    # 这13个账号被邀请
    invite_sid = [
        "V02StVuaNcoKrZ3BuvJQ1FcFS_xnG2k00af250d4002664c02f",
        "V02SWIvKWYijG6Rggo4m0xvDKj1m7ew00a8e26d3002508b828",
        "V02Sr3nJ9IicoHWfeyQLiXgvrRpje6E00a240b890023270f97",
        "V02SBsNOf4sJZNFo4jOHdgHg7-2Tn1s00a338776000b669579",
        "V02ScVbtm2pQD49ArcgGLv360iqQFLs014c8062e000b6c37b6",
        "V02S2oI49T-Jp0_zJKZ5U38dIUSIl8Q00aa679530026780e96",
        "V02ShotJqqiWyubCX0VWTlcbgcHqtSQ00a45564e002678124c",
        "V02SFiqdXRGnH5oAV2FmDDulZyGDL3M00a61660c0026781be1",
        "V02S7tldy5ltYcikCzJ8PJQDSy_ElEs00a327c3c0026782526",
        "V02SPoOluAnWda0dTBYTXpdetS97tyI00a16135e002684bb5c",
        "V02Sb8gxW2inr6IDYrdHK_ywJnayd6s00ab7472b0026849b17",
        "V02SwV15KQ_8n6brU98_2kLnnFUDUOw00adf3fda0026934a7f",
        "V02SC1mOHS0RiUBxeoA8NTliH2h2NGc00a803c35002693584d"

    ]
    sio.write("\n\n==========wps邀请==========\n\n")
    for item in wps_inv:
        sio.write("为{}邀请---↓\n\n".format(item['name']))
        if type(item['invite_userid']) == int:
            wps_invite(invite_sid, item['invite_userid'])
        else:
            sio.write("邀请失败：用户ID错误，请重新复制手机WPS个人信息中的用户ID并修改'invite_userid'项,注意不保留双引号\n\n")
    desp = sio.getvalue()
    pushWechat(desp, nowtime)
    print(desp)
    return desp


# wps接受邀请
def wps_invite(sid: list, invite_userid: int) -> None:
    invite_url = 'http://zt.wps.cn/2018/clock_in/api/invite'
    for index, i in enumerate(sid):
        headers = {
            'sid': i
        }
        time.sleep(10)
        r = s.post(invite_url, headers=headers, data={
            'invite_userid': invite_userid})
        sio.write("ID={}, 状态码: {}, \n\n ".format(str(index + 1).zfill(2), r.status_code))


def main_handler(event, context):
    return main()


if __name__ == '__main__':
    main()

```
## 设置函数运行事件
进入触发管理页面，创建触发器。触发方式选择定时触发，触发周期选择自定义触发周期，Cron 表达式填 `0 0 8 * * * *` 意思是每天上午 8 点签到。

[![20210223104333](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210223104333.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210223104333.png)

至此，腾讯云函数自动打卡就已经设置完成了。接下来就是等着程序第二天自动帮你打卡了:smile:

## 项目地址
<https://github.com/lepecoder/checkin>

<https://github.com/writemanybug/WPS-invite>


[^1]: 办公四件套：WPS 文字、WPS 表格、WPS 演示、金山 PDF


[1]: http://sc.ftqq.com/3.version