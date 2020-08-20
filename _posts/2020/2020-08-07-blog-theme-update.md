---
title: "博客主题更新"
categories:
  - diary
tags:
  - 网站
  - 日记
toc: false
toc_sticky: true
toc_label: "标题"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
自己的小博客虽然一直保持 1 IP，但是访问速度也很重要，至少要让自己访问的时候速度快一点。于是一直在想方设法加速博客静态文件以提升博客加载速度。在今天的主题更新中，终于一次性解决了访问速度慢的问题。

之前提到过博客加载速度慢的问题。有时 Font Awesome 图标不能加载出来，其主要原因还是 Font Awesome 在国内的速度不理想。

[![20200807182710](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200807182710.png)](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200807182710.png)

但是 [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 在 8 月 4 号的更新中解决了这一问题。最新版本 [4.20.0](https://github.com/mmistakes/minimal-mistakes/releases/tag/4.20.0) 将 Font Awesome 库用 jsDelivr CDN 加速，这样不论在哪里，博客图标都可以很快的加载出来。

虽然图标加载问题解决了，但是博客加载速度并没有显著的提升。F12 查看后发现是 Valine 评论系统和博客 js 文件拖慢了加载速度。

Valine 初次加载 5 秒！main.min.js 竟然耗时 7 秒多！

[![20200807184320](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200807184320.png)](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200807184320.png)

于是我开始着手使用 jsDelivr 加速静态文件。评论系统调用的 js 文件直接使用 jsDelivr 加速。至于 main.min.js 我也同样用 jsDelivr 加速，修改 `scripts.html` 中调用 main.min.js 文件代码为

```
<script src="https://cdn.jsdelivr.net/gh/sunete/sunete.github.io/assets/js/main.min.js"></script>
```
即可实现 js 文件加速，可大大提升网站加载速度。

