---
title: "GitHub+jsDelivr+PicGo 搭建免费图床"
categories:
  - tutorial
tags:
  - 图床
  - GitHub
  - JsDelivr
toc: true
toc_label: "Github图床搭建教程"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
前几天在网上看到有人发了一篇利用 GitHub+jsDelivr 搭建图床的教程，当时大概地瞄了一眼，虽然教程不复杂，但是我以为需要注册 jsDelivr 的账号，所以就没去按教程做图床。恰逢今天是周末，没什么事忙，就着手开始搭建图床。

## 写在前面
在搭建图床之前，博客里所有图片几乎都是托管在图床网站，比如 [SM图床](https://sm.ms/)、[路过图床](https://imgchr.com/)、[聚合图床](https://www.superbed.cn/)、新浪图床等等。这些图床都能免费使用，并且其中几个带有付费套餐，可以获得更好的体验。但是对于我来说，这几款图床免费套餐完全够用，所以也没有忙于搭建自己的图床。

但是图床最重要的一点是稳定，不限制流量。以上几款图床虽说开办时间至少 3 年，但是不排除后期会停办或者被 gfw 屏蔽的可能，所以有一个属于自己的图床还是有必要的。至少这个图床可以和 GitHub 存在时间一样久、不会倒闭，虽然 GitHub 倒闭的可能性几乎为零。

## 搭建教程

### 创建 GitHub 仓库
登录 [GitHub][1] 账号-->点击右上加号-->【New repository】，在创建页面填写仓库名称并勾选所需选项
![](https://cdn.jsdelivr.net/gh/sunete/imghost/imgcreat-a-new-repository.png)

### 获取 access token
点击头像-->【setting】-->【Developer settings】-->【Personal access tokens】-->【Generate new token】

![](https://cdn.jsdelivr.net/gh/sunete/imghost/imgdeveloper-settings.png)

![](https://cdn.jsdelivr.net/gh/sunete/imghost/imggenerate-new-token.png)

在创建页面 `Note` 处填写 token 用途，勾选下方 `repo` 权限，点击生成按钮获取 token。之后**复制保存 token，在后面 PicGo 配置中会用到**。
![](https://cdn.jsdelivr.net/gh/sunete/imghost/imgnote-and-scopes.png)

### 下载并安装 PicGo
[PicGo](https://github.com/Molunerfinn/PicGo) 是一个用于快速上传图片并获取图片 URL 链接的工具。GitHub 图床需要利用 PicGo 上传。点击下方链接下载最新版本 PicGo 并安装

下载地址：<https://github.com/Molunerfinn/picgo/releases>

### 设置 PicGo
打开 PicGo 点击【图床设置】-->【GitHub 图床】按提示进行设置。自定义域名处非常终于，由于要使用 JsDelivr 加速访问，所以将自定义域名设置为【https://cdn.jsdelivr.net/gh/用户名/图床仓库名 】。

当然 PicGo 还有许多配置，不懂可以看看 [PicGo使用指南](https://picgo.github.io/PicGo-Doc/zh/guide/)。
![](https://cdn.jsdelivr.net/gh/sunete/imghost/imgPicGo-setting.png)

设置好后点击确定保存，就可以使用图床了。

## 使用图床
PicGo 的使用非常简单，可以拖拽上传、剪贴板上传或者选择文件上传。图片上传完成后会有提示，图片相关链接可以在相册中点击复制。
![](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200412194904.png)

## 示例图片
本文中所有图片均为 GitHub 图床外链图片，访问速度在国内非常棒。

-------------------

## 参考文章

[《GitHub+jsDelivr+PicGo 搭建免费图床》](https://segmentfault.com/a/1190000020240864)

[1]: https://github.com/