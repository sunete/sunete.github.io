---
title: "青龙安装及对接傻妞教程"
categories:
  - tutorial
tags:
  - 教程
  - 服务器
  - Linux
toc: true
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---

Ubuntu 20.4 服务器安装青龙，并对接傻妞机器人。

## 安装青龙

执行以下命令，完成后就能通过 http://ip:5700 访问面板。

```shell
docker run -dit \
-v $PWD/ql/config:/ql/config \
-v $PWD/ql/scripts:/ql/scripts \
-v $PWD/ql/repo:/ql/repo \
-v $PWD/ql/log:/ql/log \
-v $PWD/ql/db:/ql/db \
-v $PWD/ql/jbot:/ql/jbot \
-v $PWD/ql/raw:/ql/raw \
-p 5700:5600 \
--name qinglong \
--hostname qinglong \
--restart always \
whyour/qinglong:latest
```

建议更改 `5700` 端口为其他端口，防止青龙端口被扫描爆破。

如不需要最新版青龙，可自行切换，只需将 `latest` 改成相应版本号，如 `2.10.13`。

## 安装脚本依赖

为防止出现错误 Error: Cannot find module ‘xx’，先安装脚本依赖。

```shell
docker exec -it qinglong bash
curl -fsSL https://ghproxy.com/https://raw.githubusercontent.com/shufflewzc/QLDependency/main/Shell/QLOneKeyDependency.sh | sh
```

等待安装完成后 `exit` 退出。

## 安装傻妞

使用一键安装脚本安装傻妞，非常简单。

```shell
# 国内服务器用户
s=sillyGirl;a=arm64;if [[ $(uname -a | grep "x86_64") != "" ]];then a=amd64;fi ;if [ ! -d $s ];then mkdir $s;fi ;cd $s;wget http://github.yanyuge.workers.dev/https://github.com/cdle/${s}/releases/download/main/${s}_linux_$a -O $s && chmod 777 $s;pkill -9 $s;$(pwd)/$s
# 国外服务器用户
s=sillyGirl;a=arm64;if [[ $(uname -a | grep "x86_64") != "" ]];then a=amd64;fi ;if [ ! -d $s ];then mkdir $s;fi ;cd $s;wget https://github.com/cdle/${s}/releases/download/main/${s}_linux_$a -O $s && chmod 777 $s;pkill -9 $s;$(pwd)/$s
```

安装完成后会出现『终端交互不可用，运行带-t参数即可启用』，按 **Ctrl+C** 退出。

## 配置傻妞并对接

cd 进入 sillyGirl 文件夹，输入命令 **./sillyGirl -t** 进行交互模式配置傻妞。

使用 set 命令设置傻妞机器人，这里建议先对接 QQ 机器人，或者电报机器人后在软件里操作更方便。

```shell
# 基础配置
set sillyGirl name 傻妞 #设置傻妞机器人名
set sillyGirl port 8080 #设置傻妞http服务端口
set sillyGirl duration 5 #傻妞消息撤回等待时间，单位秒
set sillyGirl update_notify false #傻妞自动升级是否通知
set sillyGirl auto_update true #是否开启傻妞自动更新
set reply 打赏 [CQ:image,file=https://xxxxxxx] #傻妞内置赞赏码
set sillyGirl enable_http_server true #是否启动http服务，对接微信公众号等需要，建议开启
set sillyGirl ignore_notify true # 傻妞忽略通知命令，默认忽略。
set qq spy_on ? # 返利间谍模式
set sillyGirl pushplus [token] # 管理员推送绑定pushplus指令
set sillyGirl recall 关键词1&关键词2... # 关键词撤回功能#关键词支持正则表达式。
set reply ? ? ## 关键词回复功能 第一个问号是支持正则的关键词，第二个问号是回复的内容。
delete reply ? #删除用set设置的关键词回复
reply ? ? ## 关键词回复功能 第一个问号是支持正则的关键词，第二个问号是回复的内容。
reply ? nil ##删除reply设置的关键词回复，请区别于用set reply设置关键词的删除方法。
set sillyGirl recall [\s\S]*[^0-9a-zA-Z=][0-9a-zA-Z]{14}[^0-9a-zA-Z;][\s\S]* # 屏蔽京东口令小妙招
重启 #重启并静默运行
命令 #获取傻妞的命令列表
守护傻妞 #解决开机自启和崩溃重启
systemctl disable sillyGirl #linux命令，关闭守护模式，守护模式会导致没法自动升级
systemctl stop sillyGirl && systemctl disable sillyGirl #linux命令，遇见傻妞被被杀死，请执行命令
docker-compose up -d --build #linux命令，docker运行

# 对接qq
set qq tempMessageGroupCode ? #设置qq临时消息默认群号
set qq onGroups g1&g2&g3... #指定要监听的qq群
set qq auto_friend false #设置是否自动同意好友请求,似乎没用，不用在意。
set qq onself true #设置是否对监听自身消息
set qq default_bot 主机器人账号 #傻妞支持对接多个qq，设置主qq机器人
set qq masters q1&q2&q3... 设置qq管理员
set qq notifier q1&q2&q3... 设置接受通知的qq账号

# 对接telegtam
set tg token ? #设置telegram机器人token
set tg http_proxy ? #设置telegram机器人代理
set tg masters t1&t2&t3... #设置telegram机器人管理员
set tg notifier t1&t2&t3... 设置接受通知的telegram账号

# 对接微信公众号
set wxmp app_id ? #设置微信公众平台app_id
set wxmp app_secret ? #设置微信公众平台app_secret 
set wxmp token ? #设置微信公众平台token
set wxmp encoding_aes_key ? #设置微信公众平台encoding_aes_key
set wxmp masters w1&w2&w3 #设置微信公众平台管理员
set wxmp subscribe_reply ? #设置公众号关注事件回复
set wxmp default_reply 无法回复该消息 设置公众号默认回复

# 对接微信-可爱猫
set wx api_url ? #设置插件调用地址，确保傻妞可以访问可爱猫端口
set wx keaimao_dynamic_ip true #设置可爱猫是否动态网络地址，适用于可爱猫家庭宽带而傻妞在云服务器的情况下
set wx keaimao_port ? #设置可爱猫端口
set wx relay_mode true #设置图片转发模式，否则可能会出现此图片来自xx未经允许不得使用的提示
set wx relaier ? #设置指定转发地址，格式为 https://域名/relay?url=%s，不知道不用填
set wx sillyGirl_dynamic_ip true #设置傻妞是否动态网络地址，适用于傻妞家庭宽带而可爱猫在云服务器的情况下
set sillyGirl enable_http_server true #启动http服务，一定要打开

# 对接微信-vlw
set wx vlw_addr http://vlw插件ip:端口 #设置插件调用地址，对应之前插件配置的 序号3 HTTP 外网API调用地址
set wx vlw_token XXX #设置对接vlw插件的token，对应之前插件配置的 序号2 API调用Token，例如sillyGirl
set wx relay_mode true #设置图片转发模式，否则可能会出现此图片来自xx未经允许不得使用的提示。不懂就不要设置了。
set wx relaier ? #设置指定转发地址，格式为 https://域名/relay?url=%s，这个我也不知道干嘛的，不知道就别设置了。
set sillyGirl enable_http_server true #启动http服务，一定要打开

# 对接青龙
青龙管理 #多容器青龙配置
ql spy #自定义监听变量运行青龙指定脚本功能
# 使用命令
ql config #获取青龙config.sh设置的内容，但我没测试出来结果，等猫咪大佬解惑
ql envs #获取青龙config.sh内设置的所有环境变量内容，但我没测试出来结果，等猫咪大佬解惑
ql env get ? #获取青龙config.sh内指定环境变量的内容，仅精确匹配
ql env find ? #查找青龙config.sh内指定的环境变量内容，支持模糊匹配
ql env set ? ? #在青龙config.sh内设置环境变量
ql env remark ? ? #字面意思是给环境变量设置备注，但我没测试出来结果，等猫咪大佬解惑
ql env disable ? #禁用（注释）在青龙config.sh内设置的环境变量
ql env enable ? #启用（取消注释）在青龙config.sh内设置的环境变量
ql raw ? #下载raw链接的js
ql task ? #在青龙里面运行指定的js
ql repo ? #在青龙里面拉库，例：ql repo https://github.com/cdle/carry.git
ql cookie status #查询青龙里cookie状态
ql crons #获取青龙所有定时任务，但我没测试出来结果，等猫咪大佬解惑
ql cron status ? #查看青龙指定定时任务的状态
ql cron run ? #运行青龙定时任务，支持模糊匹配
ql cron stop ? #停止运行青龙定时任务，支持模糊匹配
ql cron enable ? #启用青龙定时任务，支持模糊匹配
ql cron disable ? #禁用青龙定时任务，支持模糊匹配
ql cron find ? #查找青龙定时任务，支持模糊匹配
ql cron logs ? #查找青龙定时任务运行日志，支持模糊匹配
ql cron hide duplicate #隐藏青龙重复定时任务
set qinglong autoCronHideDuplicate false #关闭自动隐藏任务命令

# 对接芝士
h #短信登录
q #退出短信登录
登录 #短信登录
登陆 #短信登录
查询 ? #查询指定账号的资产
资产推送 #向所有绑定了账号的用户推送资产
查询 #查询当前社交账号绑定的所有账号资产
关闭?通知 #关闭指定活动任务通知
任务通知 #推送账号失效、果园和萌宠成熟以及未继续种植通知。有私聊和群聊@两种方式，默认私聊。
账号管理 #自定义任务通知等
推送管理 #用户设置推送
jd asset ? #查询指定账号的资产
jd imOf ? #获取绑定的社交账号，仅精确匹配pt_pin值
jd find ? #查找对应账号的编号、pt_pin值、备注等信息，支持编号、pt_pin值、备注查询，支持连号查询
jd exchange ? ? #交换两个账号的序号位置
jd enable ? #启用指定账号
jd disable ? #禁用指定账号
jd remark ? ? #备注指定账号
jd remove ? #跨容器删除ck，?可以匹配整个ck和相应的备注。芝士只有这一种方式删除ck
jd send ? ? #给指定账号发送消息
jd unbind #解绑该社交账号下的某栋账号
jd check ? ? #不知道干嘛的，第一个问号是pin值，第二个问号是青龙clientid
jd myCookie #查询绑定ck
pt_key=([^;=\s]+); pt_pin=([^;=\s]+) #发送ck提交到青龙
pin=([^;=\s]+); wskey=([^;=\s]+) #发送wskey提交到青龙
packetId=?(&|&amp;)currentActId #极速推一推助力
set jd_cookie notify_mode group #任务通知设置群聊模式
set jd_cookie qqGroup ? #任务通知设置qq群聊ID
set jd_cookie wxGroup ? #任务通知设置微信群聊ID
set pinQQ pt_pin qq号码 #ck账号绑定qq号码，例 set pinQQ jd_xxxxxx 123456
delete pinQQ pt_pin，#取消ck账号绑定qq号码，例 delete pinQQ jd_xxxxxx
set pinTG pt_pin TGID #ck账号绑定TG账号，TGID找getmyid获取
delete pinTG pt_pin #取消ck账号绑定TG账号
set pinWX pt_pin 微信号 #微信给傻妞bot发送myuid获取，其实就是你的微信号，不是微信昵称。
delete pinWX pt_pin #取消ck账号绑定微信账号
set pinWXMP pt_pin #微信公众号用户id #给公众号发送myuid获取
delete pinWXMP pt_pin #取消ck账号绑定微信公众号用户号
set jdWSCK update 56 * * * * #设置wskey自动转cooke定时：
set jd_cookie query_wait_time [限制秒数] #限制查询频率 例:set jd_cookie query_wait_time 60
set jd_cookie adong_addr 阿东ip:端口 #设置阿东登录地址，不需要http，仅支持阿东1.7及以下版本
set jd_cookie selfQid 机器人qq账号 #设置阿东qq机器人账号，仅支持阿东1.7及以下版本
set jd_cookie nolan_addr http://诺兰ip:端口 #设置诺兰登陆地址，需要http
set jd_cookie login_num ? #设置登录坑位
delete jd_cookie adong_addr 例：delete jd_cookie adong_addr ip:5701 #删除阿东地址
delete jd_cookie nolan_addr 例：delete jd_cookie nolan_addr http://ip:5701 #删除nolan地址
set jd_cookie xdd_url ?  #短信登录接入xdd指令，格式http://IP地址:端口/api/login/smslogin
set jd_cookie xdd_token ? #对接xdd，额外设置参数
set jd_cookie asset_push ? #设置定时推送
set jd_cookie ad ? #自定义广告，成功登录后发送
set jd_cookie asset_query_alias xxxxxxx #自定义查询口令，变相实现屏蔽查询口令。
set jd_cookie disable_notify true #关闭推送指令，不想收到请jd unbind
set jd_cookie enable_auto_update true #自动检测ck有效性开关，关闭则设置为false。
set jd_cookie enable_yad false #跳过云上阿东。
set jd_cookie login_tip xxx #你也可以自定义登录提示
set jd_cookie sms_tip xxx #接收短信验证码提示
set silly http_addr http://192.168.31.233:8080 #失效ck无法禁用的，检查在青龙自动生成的傻妞地址GOTIFY_URL，特定网络环境手动设置

# 对接小爱同学
#小爱同学，可以指定API，对小爱说对话模式即可开启连续对话模式，闭嘴可关闭。
set sillyGirl 小爱同学 http://81.70.100.130/api/xiaoai.php?msg=%s&n=text #挂了就自己换
set sillyGirl 小爱同学 http://jiuli.xiaoapi.cn/i/xiaoai_tts.php?msg=%s #挂了就自己换
set sillyGirl 小爱同学gjson text # 处理json格式数据的小爱api，不填获取整个文本
silly delete 小爱同学gjson # 删除处理json格式数据的小爱api
# 使用方法：
1、唤起小爱：发送“小爱+想说的话”，例如：小爱今天天气。
2、对话模式：发送“小爱对话模式”开启，发送“闭嘴”结束。
3、成语接龙：发送“成语接龙”开始。这个可应该不是小爱同学的功能，但我懒得单独写它了。

# 对接短网址
set dwz address ? #设置短网址服务地址，填傻妞对外的可以访问的地址。
set dwz prefix d #设置短网址服务前缀
# 使用方法
发送“短网址+你想要转换的网址” #例：短网址 http://kejiwanjia.com/

# 对接返利
fanli_vip #vip用户对接
fanli_edit #进入返利傻瓜配置
返利设置 #进入返利傻瓜配置
返利配置 #进入返利傻瓜配置
```

配置完成后，执行 `./sillyGirl -d` 后台静默运行傻妞。

## 服务器管理傻妞

启动及停止相关命令

```shell
启动：systemctl start sillyGirl
停止：systemctl stop sillyGirl
重启：systemctl restart sillyGirl
禁用：systemctl disable sillyGirl
启用：systemctl enable sillyGirl
```

杀掉傻妞后台进程

```shell
ps -A|grep sillyGirl ##显示进程号
kill -9 xxxxxx ##杀掉进程
```



