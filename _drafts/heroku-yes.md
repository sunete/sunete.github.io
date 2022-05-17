---
title: "Heroku 免费搭建 V2Ray 教程"
categories:
  - tutorial
tags:
  - 教程
  - 分享
toc: true
toc_sticky: true
toc_label: "搭建教程"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
之前按照 GitHub 项目 [IBMYes](https://github.com/CCChieh/IBMYes) 的教程，利用 IBM 免费搭建了一个 V2Ray，通过 CloudFlare 中转后，速度的确很快，稳定运行了将近一个月。但是随着用的人越来越多，IBM 也逐渐不稳定了，晚高峰速度变慢，偶尔断流。所以就利用Heroku 再搭建一个 V2Ray。下面详细说明搭建流程。

## 一、注册 Heroku
首先到 Heroku 官网 <https://heroku.com> 注册账号，注册邮箱不要用 QQ 邮箱，尽量用 Gmail 邮箱。

[![20200718083614](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718083614.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718083614.png)

## 二、一键部署 V2Ray 项目
点击下方按钮一键部署 V2Ray 项目到 Heroku。

[一键部署](https://dashboard.heroku.com/new?template=https%3A%2F%2Fgithub.com%2Fbclswl0827%2Fv2ray-heroku){: .btn .btn--info}

进入部署页面后，填写项目名称并选择地区。地区有美国和欧洲，这里我选择了美国。填写完成后点击 **Deploy app**。

[![20200718084328](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718084328.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718084328.png)

## 三、获取 UUID
部署完成后点击 **Manage APP** 进入项目页面。点击 **Setting** 再点击 **Reveal Config Vars** 查看并保存 UUID。

[![20200718085732](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718085732.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718085732.png)

## 配置 CloudFlare 反向代理
登录 [CloudFlare](https://www.cloudflare.com/) 官网，点击右侧 **Workers** 后点击**创建 Worker**。

[![20200718091105](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718091105.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718091105.png)

在 **脚本** 框内填入以下代码，把代码中的 `应用名称` 替换为第二步填写的应用名称。

```
addEventListener(
  "fetch",event => {
     let url=new URL(event.request.url);
     url.hostname="应用名称.herokuapp.com";
     let request=new Request(url,event.request);
     event. respondWith(
       fetch(request)
     )
  }
)
```

修改完成后点击 **保存并部署**，复制保存右侧 Worker 反向代理域名

[![20200718092044](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718092044.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718092044.png)

## 配置 V2Ray 客户端
打开 V2Ray 客户端，按照下图配置 VMess 服务器。

[![20200718093046](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718093046.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718093046.png)

## 测试效果
配置完成后，vmess 地址填写 `cloudflare.com` 速度大概在 1 万左右，如果觉得速度不够理想，可以下载软件自选 IP 填入替换。

[CloudFlare 自选 IP](https://haha.lanzous.com/im77Pep9iij){: .btn .btn--info}

[![20200718094635](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718094635.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20200718094635.png)

