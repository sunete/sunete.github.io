---
title: "把文章从Instapaper迁移到印象笔记"
categories:
  - diary
  - tutorial
tags:
  - Instapaper
  - 印象笔记
  - IFTTT
  - 稍后阅读
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
最近在使用Instapaper的时候发现，网站和软件加载速度极慢，貌似是加载不出来。上网搜索了一下才发现，原因是Instapaper的服务器部署在aws，而aws在中国境内几乎处于半墙状态，所以导致Instapaper无法使用。<br>

## Instapaper ##
Instapaper是一款稍后阅读软件，如果有一篇文章想要保存起来稍后阅读，只需要点击保存到Instapaper即可。<br> 
    
>Instapaper官网：https://www.instapaper.com/   
 
这个软件帮助我保存了不少文章。但是，对于一款稍后阅读软件来说，如果网络状况不允许，那几乎是致命的灾难。因为对于我来说，不可能每次看文章都去打开VPN，所以就想办法找一个可以替代Instapaper的软件。<br>
在多次寻找之后，最终选定了[印象笔记][1]。<br>

## 印象笔记 ##
印象笔记可以理解为一款笔记软件，但又功能又不仅仅是一款笔记软件。使用它可以在多种设备和平台间无缝同步每天的见闻、思考与灵感，一站式完成信息的收集备份、永久保存和高效整理。<br>

>官方网站：https://www.yinxiang.com/


除了这些实用的功能外，我选择它的很重要的一点是，印象笔记在国内也可以使用，全平台同步很便捷。手机上安装[印象笔记安卓版][2]，也有[PC客户端][3]以及浏览器扩展——[剪藏][4]<br>

## 迁移文章 ##
安装完成后最大的问题是如何将Instapaper中的文章简单快速迁移到印象笔记。<br>
使用IFTTT，只需要将所有Instapaper内部的文章进行归档，IFTTT就会自动把文章同步到印象笔记，非常的方便。最终将所用文章全部同步到了印象笔记，也把半墙状态的Instapaper卸载掉了。


  [1]: https://www.yinxiang.com/
  [2]: https://play.google.com/store/apps/details?id=com.evernote
  [3]: https://www.yinxiang.com/download/
  [4]: https://www.yinxiang.com/new/product/webclipper/install/