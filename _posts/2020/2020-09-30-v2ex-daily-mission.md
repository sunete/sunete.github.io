---
title: "V2EX 每天自动签到获取金币"
categories:
  - tutorial
tags:
  - 教程
  - VPS
  - Github
toc: true
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
利用 VPS 实现 v2ex 每天自动签到获取金币。本文教程主要依赖 GitHub 项目 v2ex_daily_mission。

项目地址：<https://github.com/lord63/v2ex_daily_mission>

## 获取账号 Cookie
登录 [v2ex](https://www.v2ex.com/) 账号，F12 调出控制台。复制保存 Cookie。

## 安装依赖
SSH 连接 Linux 服务器后，为避免执行命令时出现 `command not found` 的错误，在部署项目前需要先安装必要的依赖。

执行以下命令安装所需依赖，git 和 pip。

Debian 或 Ubuntu 可直接用包管理器安装

安装 Git
```
sudo apt-get install git
```

安装 Python

```
sudo apt-get install python-pip
```

Centos 系统使用以下命令安装

安装 Git
```
yum install git
```

CentOS yum 源 中默认没有 pip，需要安装 扩展源EPEL
```
sudo yum -y install epel-release
```

安装 pip
```
sudo yum -y install python-pip
```

## 部署项目
克隆 [v2ex_daily_mission](https://github.com/lord63/v2ex_daily_mission)。
```
git clone https://github.com/lord63/v2ex_daily_mission
```

基本安装

```
pip install v2ex_daily_mission
```

## 配置文件
使用自带的子命令初始化(可能需要 root 权限或者管理员权限)：

```
v2ex init
```
按提示依次输入 Cookie、日志路径和通知方式。

- Cookie 为第一步获取到的账号 Cookie
- 日志路径按需求设置，我设置为 `v2ex_daily_mission`
- 通知方式目前支持 bark 和 slack，因为我两个账号都没有，就默认没设置

下面是执行示例
```
# v2ex init
Input your cookie: 输入 v2ex 账号 Cookie
Input your log directory: v2ex_daily_mission
Input your notifier (bark, slack, none) [none]: 
Init the config file at: /usr/bin/v2ex_config.json
```
至此，配置已经完成，可以测试使用签到功能了。

## 开始使用
执行签到
```
v2ex sign
```
执行完成后会输出签到成功提示
```
# v2ex sign
Today: 20200930 的每日登录奖励 10 铜币
Total: 3412.0
```
其他使用命令及示例，参考原项目 [使用说明](https://github.com/lord63/v2ex_daily_mission#开始使用)。

## 定时执行签到
打开定时任务设置
```
crontab -e
```
按下 **I** 键进入编辑模式，然后加入下面一行代码。
```
0 9,21 * * *  /usr/local/bin/v2ex sign
```
这条命令的意思是每天的早、晚九点各执行一次签到（执行两次的目的是，防止意外失败导致连续签到中断）。

然后按 **Esc** 键退出编辑模式，然后输入 **:wq** 保存并退出！