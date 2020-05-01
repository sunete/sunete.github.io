---
title: "git clone 太慢怎么办"
categories:
  - tutorial
tags:
  - Github
  - 代理
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
在国内clone GitHub项目时有时会非常慢，下载速度可能只有10K/s。这时可以使用全局代理加快clone速度。

执行以下命令，使所有clone都通过ssr或ss代理。其中端口1080为ss本地代理端口，可在设置中查看。

```
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080
```

如需取消全局代理，执行以下命令。
```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

