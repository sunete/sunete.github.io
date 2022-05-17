---
title: "微信、支付宝刷步 蚂蚁森林每天296g能量"
categories:
  - tutorial
tags:
  - 教程
toc: true
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
之前一直用抓包版本的云函数刷步数，但是此版本有一个缺点是退出小米运动账号就会停止刷步，很不方便。

后面发现吾爱 [@feifei](https://www.52pojie.cn/thread-1222713-1-1.html) 更好用的无需抓包版本刷步函数，利用腾讯云函数，自动登录小米运动账号，调用官方接口，修改小米运动步数并同步至支付宝、微信。可以足不出户就能霸占微信运动榜首，每天收取蚂蚁森林296g能量。

此版本无需抓包，按照步骤配置函数代码，即可实现每天自动刷步，推荐此方法。

## 云函数配置
登录 [腾讯云函数控制台](https://console.cloud.tencent.com/scf/list)，新建函数，运行环境选择 `Python 3.6`，模板函数选择 `helloworld` 模板。

[![20201216174117](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201216174117.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201216174117.png)

## 函数代码
### 新建 data_json.txt
新建名为 `data_json.txt` 的文件，文件内容 [点击此处下载](https://www.lanzoui.com/iz6HHjeu23i)，复制进去保存。

[![20201216175343](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201216175343.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201216175343.png)

### 修改 index.py
复制下方代码，替换原文件内容，配置相关参数后保存。

<details>
<summary>点击查看代码</summary>

<pre><code>
import requests,time,re
from random import randint
  
headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.121 Safari/537.36'
    }
  
#以下参数自己填写
user = ""
password = ""
step = str(randint(17760,20000))
 
#机器人key
key = ""
qq = ""
 
def get_code(location):
    code_pattern = re.compile("(?<=access=).*?(?=&)")
    code = code_pattern.findall(location)[0]
    #print(code)
    return code
 
#get_code("https://s3-us-west-2.amazonaws.com/hm-registration/successsignin.html?region=cn-northwest-1&access=N2CPd5eddwaEs0vWwqUlC&country_code=CN&expiration=1602140234")
 
def login(user,password):
    url1 = "https://api-user.huami.com/registrations/+86" + user + "/tokens"
    headers = {
        "Content-Type":"application/x-www-form-urlencoded;charset=UTF-8",
        "User-Agent":"MiFit/4.6.0 (iPhone; iOS 14.0.1; Scale/2.00)"
        }
    data1 = {
        "client_id":"HuaMi",
        "password":f"{password}",
        "redirect_uri":"https://s3-us-west-2.amazonaws.com/hm-registration/successsignin.html",
        "token":"access"
        }
    r1 = requests.post(url1,data=data1,headers=headers,allow_redirects=False)
    print(r1.text)
    location = r1.headers["Location"]
    #print(location)
    try:
        code = get_code(location)
    except:
        print("登录失败！")
        return 0,0
    print("access_code获取成功！")
    print(code)
     
    url2 = "https://account.huami.com/v2/client/login"
    data2 = {
        "app_name":"com.xiaomi.hm.health",
        "app_version":"4.6.0",
        "code":f"{code}",
        "country_code":"CN",
        "device_id":"2C8B4939-0CCD-4E94-8CBA-CB8EA6E613A1",
        "device_model":"phone",
        "grant_type":"access_token",
        "third_name":"huami_phone",
        } 
    r2 = requests.post(url2,data=data2,headers=headers).json()
    login_token = r2["token_info"]["login_token"]
    print("login_token获取成功！")
    print(login_token)
    userid = r2["token_info"]["user_id"]
    print("userid获取成功！")
    print(userid)
 
    return login_token,userid
     
#login("","")
 
def main_handler(event, context):
    login_token,userid = login(user,password)
    if login_token == 0:
        return
    t = get_time()
    app_token = get_app_token(login_token)
    with open('data_json.txt','rt') as f:
        data_json = f.read()
    date = time.strftime("%Y-%m-%d",time.localtime())
    data_json += date + "\"}]"
    step_pattern = re.compile("12345")
    de_id_pattern = re.compile("321123")
    data_json = de_id_pattern.sub("DA932FFFFE8816E7",data_json)
    data_json = step_pattern.sub(f"{step}",data_json)
    url = f'https://api-mifit-cn.huami.com/v1/data/band_data.json?&t={t}'
    head = {
        'User-Agent': 'Mozilla/5.0 (iPhone; CPU iPhone OS 13_4_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 MicroMessenger/7.0.12(0x17000c2d) NetType/WIFI Language/zh_CN',
        'apptoken': f'{app_token}'
        }
    data = {
        'data_json': f'{data_json}',
        'userid': f'{userid}',
        'device_type': '0',
        'last_sync_data_time': '1589917081',
        'last_deviceid': 'DA932FFFFE8816E7',
        }
    response = requests.post(url, data=data, headers=head).json()
    print(response)
    result = f"每日修改步数{step}："+ response['message']
    print(result)
    robot(result)
    return result
  
#获取时间戳
def get_time():
    url = 'http://api.m.taobao.com/rest/api3.do?api=mtop.common.getTimestamp'
    response = requests.get(url,headers=headers).json()
    t = response['data']['t']
    return t
  
#获取app_token
def get_app_token(login_token):
    url = f"https://account-cn.huami.com/v1/client/app_tokens?app_name=com.xiaomi.hm.health&dn=api-user.huami.com%2Capi-mifit.huami.com%2Capp-analytics.huami.com&login_token={login_token}&os_version=4.1.0"
    response = requests.get(url,headers=headers).json()
    app_token = response['token_info']['app_token']
    print("app_token获取成功！")
    print(app_token)
    return app_token
  
#机器人
def robot(text):
    try:
        url = "https://qmsg.zendee.cn:443/send/" + key
        data = {
            'msg': f'{text}',
            'qq': f'{qq}'
            }
        r = requests.post(url,data =data)
        print(r.text)
    except:
        print("发送失败！")
    else:
        print("发送成功！")
</code></pre>
</details>

<br>注意填写参数：

- user = "小米运动账号"
- password = "小米运动密码"
- key = "[Qmsg酱key](https://qmsg.zendee.cn/)"
- qq = "自己的QQ号"

key 和 qq 需要到 [Qmsg官网](https://qmsg.zendee.cn/) 设置获取。网站：[https://qmsg.zendee.cn/](https://qmsg.zendee.cn/)

## 设置定时触发
云函数触发管理，创建触发器，按照下图设置。corn 表达式填入 `0 0 13 * * * *` 代表每天 13:00 触发函数，也可按照自己的喜好修改，详细配置策略可参考 [Cron相关文档](https://cloud.tencent.com/document/product/583/9708#cron-.E8.A1.A8.E8.BE.BE.E5.BC.8F)。

[![20201216175420](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201216175420.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201216175420.png)

关于抓包刷步云函数可查看 [语雀文档](https://www.yuque.com/docs/share/336d83f9-10b5-43f3-8101-54b084596396?# 《微信、支付宝刷步 蚂蚁森林每天296g能量》)

参考文章：

- [利用云函数+Python实现每日自动修改微信支付宝步数并用qq提醒](https://www.52pojie.cn/thread-1222713-1-1.html)
- [云函数 小米运动刷步数](https://www.52pojie.cn/thread-1247687-1-1.html)