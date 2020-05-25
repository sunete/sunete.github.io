---
title: "如何创建一个 telegram 私聊机器人"
categories:
  - tutorial
tags:
  - 教程
  - Telegram
toc: true
toc_sticky: true
toc_label: "如何创建消息转发机器人"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
由于每天都会使用 telegram，并且在 telegram 频道上管理更新一些活动，所以避免不了和其他人私聊。但是为了保护隐私，有的时候是不想直接在网络上暴露自己的个人账号的，所以就需要一个 telegram 私聊机器人作为中间桥梁，间接把他人的消息传达给我。之前也已经按照网上的教程搭建过一个私聊机器人，但是已经完全忘记了搭建方法，所以在这里再次记录一下搭建流程，防止无法在网上找到相关教程。

## 私聊BotFather创建机器人
使用telegram查找并私聊 [BotFather][1] 以获得 api。

BotFather 是 Telegram 官方的机器人，用于创建新机器人账户和管理自己已存在的机器人。

 1. 点击开始，发送 `/newbot`，为你的机器人取一个名字，并将其发送给 [BotFather][2]。

 2. 为你的机器人创建用户名，用户名必须以 `bot` 结尾，例如 `telegeam_bot` 或者 `telegramBot`。其后 [BotFather][3] 会发送一条包含这个机器人 API 的消息，记下 API 下面会用到。（不要把 token 发送给其他人，因为其他人可以通过 token 控制你的机器人）。

ps：如果不小心退出，或者忘记了这个机器人的 API，你仍然可以发送 `/mybots` ,选择你刚刚创建的机器人，查看 API Token。

![BotFather][4]

## 私聊Livegram Bot
Livegram Bot 可以用于创建电报转发机器人，它可以将发送给机器人的消息转发给你。

 1. 查找 [Livegram Bot][5]，并点击开始

 2. 发送 `/addbot`

 3. 把从 [BotFather][6] 获取到的机器人 API 发送给 [Livegram Bot][7]
 
![Livegram Bot][8]

至此，Telegram 私聊机器人就已经搭建完毕可以使用了，任何发送给机器人的消息，都将通过这个机器人转发给你。

## 其他配置
如果你愿意，接下来也可以发送 `/mybots` 给 [BotFather][9]，选择相应机器人进行其他配置。

![mybots][10]

例如设置机器人、关联支付方式、删除机器人、等等···

![menu][11]

在 `Edit Bot` 中可以编辑机器人的描述、相关介绍和头像等其他信息

![edit][12]
 

参考文章：[Telegram：3分钟免费搭建可用于私聊的机器人](https://nobugin.com/telegram-3-minutes-free-to-build-a-robot-for-private-chat.html)

  [1]: https://t.me/BotFather
  [2]: https://t.me/BotFather
  [3]: https://t.me/BotFather
  [4]: https://s1.ax1x.com/2020/03/17/8t0jOg.png
  [5]: https://t.me/LivegramBot
  [6]: https://t.me/BotFather
  [7]: https://t.me/LivegramBot
  [8]: https://s1.ax1x.com/2020/03/17/8trRS0.png
  [9]: https://t.me/BotFather
  [10]: https://s1.ax1x.com/2020/03/17/8tsW4A.png
  [11]: https://s1.ax1x.com/2020/03/17/8tsLNj.png
  [12]: https://s1.ax1x.com/2020/03/17/8tywVg.png