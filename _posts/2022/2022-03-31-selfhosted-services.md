---
title: "我在服务器上搭建了哪些服务"
categories:
  - diary
tags:
  - VPS
toc: false
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
玩服务器已经有三四年的时间了，从最开始热心网友指导我搭建网站，到现在能够熟练的驾驭服务器，服务器带给我的便利越来越多。最近又新开出来了一台 4 核 24 G 的 Oracle Cloud 服务器，就准备把我常用的一些服务迁移到这台新的服务器上。本文就来罗列一下我常用的自建服务。

## 1. Bitwarden

以前密码都是自动保存在 Chrome 里，各个平台账号太多，几乎所有账号的密码都设置为同一个，这样如果遇上某个网站被撞库，密码泄露，后果不堪设想，于是萌生了使用密码管理服务的想法。在经过多方面对比后，选择了 Biwarden，对于一般用户来说，官方的免费服务完全够用，我自建主要是用到了自动填充二次验证的功能。

服务器搭建的是 [Vaultwarden](https://github.com/dani-garcia/vaultwarden) —— Bitwarden 第三方 Docker 服务。

## 2. Telegram RSS Bot

我是一个重度 RSS 用户，加上平时经常用 [Telegram](https://telegram.org/)，就搭建了一个 RSS 机器人，搭配 RSSHub，订阅、接收 RSS 信息非常方便。

有关 Telegram RSS 机器人的项目在 GitHub 很多，我选择的是下面几个。

- [FreshRSS](https://github.com/FreshRSS/FreshRSS)
- [rssbot](https://github.com/iovxw/rssbot)
- [NodeRSSBot](https://github.com/fengkx/NodeRSSBot)

## 3. 青龙面板

神一般的存在，因为能定时运行 Python、JavaScript 代码，可以做很多事儿。我主要是用来挂京东签到脚本和论坛自动签到脚本，解放双手，不用每天去手动签到了。

GitHub：https://github.com/whyour/qinglong

## 4. Cloudreve

自建网盘程序，可以挂载 OneDrive、Google Drive、SharePoint 等网盘，搭配 Aira2 离线下载一些电影电视剧，很方便。

GitHub：https://github.com/cloudreve/Cloudreve

## 5. 哪吒监控

目前手上服务器有 6 台，为了实时监控服务器状态，就搭建了一个哪吒监控。在监控网站可以实时显示服务器 CPU、内存和硬盘的使用情况。再说哪个站长没个探针呢，是吧？

GitHub：https://github.com/naiba/nezha

## 6. ArchiSteamFarm

ASF，用来 Steam 挂卡，挂出来的卡牌可以出售或合成。

GitHub：https://github.com/JustArchiNET/ArchiSteamFarm

