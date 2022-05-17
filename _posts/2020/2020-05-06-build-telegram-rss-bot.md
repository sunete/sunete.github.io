---
title: "Telegram RSS 机器人搭建教程"
categories:
  - tutorial
tags:
  - 教程
  - Telegram
  - GitHub
  - VPS
toc: true
toc_sticky: true
toc_label: "搭建教程"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---

Telegram 是一款非常棒的即时通讯软件，在这款软件上有多种多样的机器人可供使用，其中非常实用的一个机器人就是 RSS 机器人。RSS 机器人可以通过 RSS 源订阅网站，并在聊天界面发送消息通知，可以及时收到并查看网站的最新文章。

Telegram 上有很多开放使用的 RSS 机器人，但是这些毕竟是别人的，所以我就尝试自己搭建一个。

## GitHub 开源地址
NodeRSSBot: <https://github.com/fengkx/NodeRSSBot>

## 准备工作
1. Centos 7 系统 VPS
2. 科学上网环境
3. SSH 管理软件 Xshell 或 Putty
4. Telegram

## 创建 Telegram 机器人
Telegram 查找 [BotFather](https://telegram.me/BotFather)，发送 `/newbot` 创建一个新的机器人。这里需要为机器人取一个名字，名字可随意设置。之后设置机器人的用户名，用户名必须以 bot 结尾，比如 `RSS_bot` 或者 `RSSbot`。创建完成后会获得该机器人的 Token。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200506143836.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200506143836.png"></a> </figure>

## 安装 Docker
Xshell 连接 VPS 后，使用 sudo 或 root 登录

确保 yum 包更新到最新
```shell
sudo yum update
```

执行 Docker 安装脚本
执行这个脚本会添加 docker.repo 源并安装 Docker。

```shell
curl -fsSL https://get.docker.com/ | sh
```

启动 Docker 进程
```shell
sudo service docker start
```

验证 docker 是否安装成功并在容器中执行一个测试的镜像
```shell
sudo docker run hello-world
```

## VPS 部署机器人
执行

```shell
docker pull fengkx/node_rssbot
```

成功后继续执行以下命令。

```shell
docker run --name rssbot -d -v <directory to store database file>:/app/data/ -e RSSBOT_TOKEN=<YOUR_TGBOT_TOKEN> fengkx/node_rssbot
```
其中 `<directory to store database file>` 替换为数据文件存储路径，可以设置为 `/var/data`；`<YOUR_TGBOT_TOKEN>` 替换为自己机器人的 Token。

执行完成后会返回一串数字和字母，到这里机器人就部署完成了。

如果想修改机器人其他配置，可在 Docker 命令中添加相应环境变量进行修改，示例如下：

`docker run --name rssbot -d -v /var/data:/app/data/ -e RSSBOT_TOKEN=<YOUR_TGBOT_TOKEN> -e RSSBOT_FETCH_GAP=10m -e RSSBOT_VIEW_ALL=true fengkx/node_rssbot`
## 使用 RSS 机器人
回到 Telegram 私聊 RSS 机器人以下消息，即可使用。

```
/rss       - 显示订阅列表，加 `raw`显示链接
/sub       - 订阅 RSS: /sub http://example.com/feed.xml 支持自动检测 RSS feed
/unsub     - 退订 RSS: /unsub http://example.com/feed.xml 或者通过键盘
/unsubthis - 回复一个 RSS 发来的消息退订该 RSS
/allunsub  - 退订所有源
/export    - 导出订阅到opml文件
/viewall   - 查看所有订阅和订阅人数 需要在设置中打开
/import    - 回复此消息 opml 文件导入订阅(群组)
/lang      - 更改语言
/heath      - 展示活跃订阅源的健康程度
```
其中通过 opml 文件导入订阅这个功能非常实用，直接将 opml 文件发送给机器人就能订阅里面所有的源。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200506183522.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200506183522.png"></a> </figure>

后续如果想在机器人聊天窗口添加可使用的快捷命令，在 [BotFather](https://telegram.me/BotFather) 设置就可以了。

## 其他设置
### Ubuntu 安装 Docker

```
curl  - o -  https://get.docker.com | sudo bash
sudo curl  - L "https://github.com/docker/compose/releases/download/1.26.2/docker - compose - $(uname  - s) - $(uname  - m)"  - o /usr/local/bin/docker - compose
sudo chmod +x /usr/local/bin/docker - compose
```

### Docker 删除容器和镜像
列出所有容器 ID
```
docker ps -aq
```

查看所有运行或者不运行容器
```
docker ps -a
```

停止所有的 container（容器），这样才能够删除其中的 images
```
docker stop $(docker ps -a -q) 或者 docker stop $(docker ps -aq) 
```

如果想要删除所有 container（容器）的话再加一个指令：
```
docker rm $(docker ps -a -q) 或者 docker rm $(docker ps -aq) 
```

查看当前有些什么 images
```
docker images
```

删除 images（镜像），通过 image 的 id 来指定删除谁
```
docker rmi <image id>
```

要删除全部image（镜像）
```
docker rmi $(docker images -q)
```

强制删除全部 image
```
docker rmi -f $(docker images -q)
```