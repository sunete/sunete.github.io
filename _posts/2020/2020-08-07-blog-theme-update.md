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
自己的小博客虽然一直保持 1 IP，但是访问速度也很重要，至少要让自己访问的时候速度快一点。

之前提到过博客加载速度慢的问题。有时 Font Awesome 图标不能加载出来，其主要原因还是 Font Awesome 在国内的速度不理想。

[![20200807182710](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200807182710.png)](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200807182710.png)

但是 [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 在 8 月 4 号的更新中解决了这一问题。最新版本 [4.20.0](https://github.com/mmistakes/minimal-mistakes/releases/tag/4.20.0) 将 Font Awesome 库用 jsDelivr CDN 加速，这样不论在哪里，博客图标都可以很快的加载出来。

虽然图标加载问题解决了，但是博客加载速度并没有显著的提升。F12 查看后发现是 Valine 评论系统和博客 js 文件拖慢了加载速度。

Valine 初次加载 5 秒！main.min.js 竟然耗时 7 秒多 :sweat: 

[![20200807184320](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200807184320.png)](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200807184320.png)

由于博客也没人留言，所以还是把评论关闭了。如果哪位朋友想要联系我，就用 [E-mail](mailto:xuhao0347@gmail.com) 吧。至于 main.min.js 这个坑暂时先留在这里，有时间再填。

