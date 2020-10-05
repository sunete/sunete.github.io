---
title: "科学上网工具及教程合集"
categories:
  - tutorial
tags:
  - 教程
  - VPS
  - 科学上网
toc: true
toc_sticky: true
toc_label: "科学上网汇总"
toc_icon: "paper-plane"  # Font Awesome对应图标名称 (无fa前缀)	
---

博主自己收集的科学上网软件及教程，原本准备放在主页顶栏的，但是想着，我这这是一个小小的个博客而已，主要目的就是记录，不能太招摇（虽说 GFW 根本不可能理睬我这小博客）。所以，为了防止域名被墙，还是以文章的形式发布出来，以免得不偿失。博主对以下各项进行了主观打分（五星制），仅供参考。

## 科学上网软件
以下软件本身不具备科学上网功能，需要用国外服务器，结合[搭建教程](#科学上网搭建教程)自行搭建相应服务，并导入软件才能使用。如果没有自行搭建能力，建议购买机场[^1]服务。如果没有机场服务，且没有任何科学上网方式，可以[E-mail](mailto:xuhao0347@gmail.com) :envelope: 联系我，我可以提供一些帮助。

### Shadowsocks (SS)
- 易用性：:star::star::star::star::star:
- 安全性：:star::star::star::star::star:
- 官网：<https://shadowsocks.org/>
- 简介：Shadowsocks 又称小飞机，可以使用 ss 链接的科学上网软件，支持 Windows、Mac OS X、Android、iOS、路由器等多种平台，几乎覆盖所有种类用户端。原项目中国作者已经被请喝茶。

### ShadowsocksR (SSR)
- 易用性：:star::star::star::star::star:
- 安全性：:star::star::star::star::star:
- 官网：无 （GitHub 上有相关项目分支）
- 简介：SSR 是由 [breakwa11](https://mobile.twitter.com/breakwa11)（破娃）开发的一款科学上网软件，可使用 ss、ssr 链接，支持 Windows、Android 平台。由于作者被人肉，原作者已经停更，目前 GitHub 上有很多原版基础上继续维护的分支，也有很多魔改版，其中比较著名的有 [SSRR](#SSRR)。


### <span id="SSRR">ShadowsocksRR</span> (SSRR)
- 易用性：:star::star::star::star::star:
- 安全性：:star::star::star::star::star:
- 官网：<https://github.com/shadowsocksrr>
- 简介：ShadowsocksR (SSR) 原作者被请喝茶后，另外一位大神在原项目基础上维护、更改的客户端。易用性在 SSR 基础上提升了很多。可使用 ss、ssr 链接


### V2Ray
- 易用性：:star::star::star::star::star:
- 安全性：:star::star::star::star::star:
- 官网：<https://www.v2ray.com/>
- 简介：支持 vmess、ss 协议的科学上网客户端，安全性比前面的 ss 及 ssr 都好一些。操作简单，有多种客户端，详见官网。
  
### Qv2ray
- 易用性：:star::star::star::star:
- 安全性：:star::star::star::star::star:
- 官网：<https://github.com/Qv2ray/Qv2ray>
- 简介：一个通过插件就可以使用 V2ray / SSR / Trojan 等多种协议的科学上网软件。上手稍有难度，但是功能非常强大。一个客户端可以代替多个客户端，解决了多种协议需要多个客户端的痛点，适合使用多个机场或多种科学上网协议的人。


### Trojan
- 易用性：:star::star::star::star:
- 安全性：:star::star::star::star::star:
- 官网：<https://github.com/trojan-gfw/trojan>
- 简介：Trojan是一种新型的科学上网工具，近期受到很多用户的欢迎。伪装效果好，与 V2Ray 的 WS+TLS 模式非常相似。有 Windows、Android、iOS 客户端。


### ~~各类 VPN~~（不推荐）
- 易用性：:star::star::star:
- 安全性：:star:
- 简介：谷歌商店及其他各种途径获得的 VPN 均不推荐使用，免费 VPN 可能包含有很多广告、速度慢、稳定性差，同时也有可能泄露个人信息。所以不推荐使用各类 VPN。

## 科学上网搭建教程

### SS/SSR 一键脚本
1. 逗比 SS 一键脚本
```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ss-go.sh && chmod +x ss-go.sh && bash ss-go.sh
```
2. 秋水逸冰 SS 一键脚本
```
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```
3. 逗比 SSR 一键脚本
```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```
4. 秋水逸冰 SSR 一键脚本
```
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

### V2Ray 一键脚本
1. 233 V2Ray 一键脚本
```
bash <(curl -s -L https://git.io/v2ray.sh)
```

2. Atrandys V2Ray 一键脚本
```
curl -O https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/v2ray_ws_tls1.3.sh && chmod +x v2ray_ws_tls1.3.sh && ./v2ray_ws_tls1.3.sh
```

3. wulabing V2Ray 一键脚本
```
wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh" && chmod +x install.sh && bash install.sh
```
4. dylanbai8 V2Ray 一键脚本
```
wget -N --no-check-certificate git.io/v.sh && chmod +x v.sh && bash v.sh
```

### Trojan 一键脚本
```
curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh && chmod +x trojan_mult.sh && ./trojan_mult.sh
```

### MTproxy
一款简单方便的 Telegram 客户端代理，在 Telegram 中点击 MTP 链接，就能像使用 QQ 和微信一样简单地使用 Telegram。但是目前简单的 MTproxy 已经被识别，自行搭建后，很快就会失效，不过已经出现了在 MTproxy 基础上添加混淆的其他抗封版本。

### Socks 5
网络代理工具，已经被精准识别，很难长时间存活，不建议搭建使用。

[^1]: 机场：提供科学上网服务的网站。