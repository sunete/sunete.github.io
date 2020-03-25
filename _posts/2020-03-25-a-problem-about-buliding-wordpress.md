---
title: "搭建Wordpress小记"
categories:
  - tutorial
tags:
  - 网站
  - 教程
  - wordpress
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
在网站备案完成后，下午有空，就开始搭建网站了。

起初试着按照以前的建站步骤来，解析域名之后在宝塔上传Wordpress网站源码。但是在上传后，无论如何也不能打开网站。

于是开始排查问题。数据库创建了，其他依赖也没有缺失，为什么呢？

去网上找了一圈，看了几篇文章后才发现，是服务器没有开启80和443端口导致的。

![参考][1]

去后台开启端口。

![开启端口][2]

网站能够正常访问啦

![成功][3]

参考文章：[案例八：允许公网通过HTTP、HTTPS等服务访问实例][4]

  [1]: https://s1.ax1x.com/2020/03/25/8jMFEV.png
  [2]: https://s1.ax1x.com/2020/03/25/8jMVCF.png
  [3]: https://s1.ax1x.com/2020/03/25/8jMkNT.png
  [4]: https://help.aliyun.com/document_detail/25475.html?spm=5176.2020520101.0.0.765e4df5SuLnDi