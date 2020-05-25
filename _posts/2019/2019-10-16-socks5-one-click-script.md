---
title: "Scoks5 一键搭建脚本"
categories:
  - tutorial
tags:
  - 教程
  - VPS
toc: true
toc_label: "Scoks5一键搭建脚本"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
## GitHub 链接
<https://github.com/wyx176/Socks5>       
   
一键脚本
<pre><code>wget -q -N --no-check-certificate https://raw.githubusercontent.com/wyx176/Socks5/master/install.sh && bash install.sh</code></pre>

## 介绍 ##
一个 Shell 脚本，集成 Socks5 搭建，管理，启动，添加账号等基本操作。基于 Socks5 官方的辅助脚本，方便用户操作，并且支持快速构建 Socks5 服务环境。

## 系统支持 ##
* CentOS 6.x
* CentOS 7.x
* 谷歌云部分系统问题请看更新日志

## 功能 ##
 全自动无人值守安装，服务端部署只需一条命令）
- 一键开启、关闭 ss5 服务
- 添加账户，删除用户，开启账户验证，关闭账户验证，一键修改端口
- 支持傻瓜式用户添加，小白也可以用
- 自动修改防火墙规则
- 输入 s5 即可启动控制面板

## 一键安装脚本 ##

```yaml
wget -q -N --no-check-certificate https://raw.githubusercontent.com/wyx176/Socks5/master/install.sh && bash install.sh
```

## 其他问题
### 提示 wget: command not found 的错误
这是你的系统精简的太干净了，wget 都没有安装，所以需要安装 wget。

```yaml
yum -y install wget
```

### `s5` 命令执行后无反应
这是谷歌云自身问题，需要先执行以下代码,再执行 `s5`

```yaml
export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
```
