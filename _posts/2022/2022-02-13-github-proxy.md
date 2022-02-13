---
title: "终于设置好了 GitHub 网络"
categories:
  - tutorial
tags:
  - 教程
  - 日记
  - 网站
toc: false
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
又过了好久没有更新博客，主要是 GitHub 网络太差，总是出现 `failed to connect to github 443` 错误，这就很烦。所以最近写的东西都放在一个临时的 Typecho 博客里。

不过从今往后不会有这个问题了，因为我已经顺利解决了网络问题。

电脑的 Clash 是开机自启的，所以只需要设置好 git 代理，就能借助 Clash 顺利把博客项目推送到 GitHub。

设置代理也很简单，只需要在 CMD 执行以下命令即可设置代理。

```
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

因为我的 Clash 代理端口是 7890 ,所以设置代理端口为 7890，如果是其他的代理工具，需要修改为相应端口。

取消 git 全局代理

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

接下来就可以开启搬砖模式，把文章搬回来啦！嘿嘿 ~