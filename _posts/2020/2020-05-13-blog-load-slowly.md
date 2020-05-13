---
title: "博客加载速度过慢问题"
categories:
  - blog
tags:
  - 博客优化
toc: false
toc_sticky: true
toc_label: "标题"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
由于 GitHub 在国内访问速度的问题，博客加载速度很慢，国内用户首次加载需要耗时 10s 左右，访问体验很差。

<figure> <a href="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200513102350.png"><img src="https://cdn.jsdelivr.net/gh/sunete/imghost/img20200513102350.png"></a> </figure>

从加载信息中可以看到，最耗时的是博客的 `main.css` 和 `main.min.js` 两个文件，所以想加快博客的加载速度，就必须从这两个文件入手。国内加快 js 文件加载速度最好的方法就是配置 CDN。在众多 CDN 中，jsDelivr 是最出众的，加载速度快、稳定。所以接下来就可以着手优化博客了。

网上为 Jekyll 博客配置 jsDelivr 的方法很多，但是并没有适合我这款博客的相似教程，所以这算是一个坑，后面慢慢填吧~