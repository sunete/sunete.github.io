---
title: "Web 源码后门检测工具"
categories:
  - tutorial
tags:
  - 网站
  - 教程
toc: false
toc_sticky: true
toc_label: "标题"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
经常折腾网站，会在网上获得各种各样的网站模板，这些从网上下载来的源码上传到服务器上才能使用。很多时候，源码安全性都是未知的，如果源码存在后门，就有可能导致服务器被黑或者变成 肉鸡[^1]。这时就需要采取措施，防范一些存在后门的源码。这里列出 2 个比较出名的在线后门检测网站。

## 河马查杀
专业 webshell 查杀网站，有 Windows 和 Linux 客户端。同时还支持在线查杀。

官方网站：<https://www.shellpub.com/>

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200510092228.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200510092228.png"></a> </figure>

在线查杀方便在不需要下载软件即可使用。把源码 zip 压缩包上传即可查杀。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200510092642.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200510092642.png"></a> </figure>

## 百度 WebShell 检测
百度出品的在线查杀网站，不收费、不限制上传数量，算百度良心了一把

官方网站：<https://scanner.baidu.com/>

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200510093516.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200510093516.png"></a> </figure>

直接将源码上传，就可以在线查杀。支持的文件类型比河马查杀要多不少。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200510093952.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200510093952.png"></a> </figure>

[^1]: 肉鸡也称傀儡机，是指可以被黑客远程控制的机器。肉鸡通常被用作 DDOS 攻击。