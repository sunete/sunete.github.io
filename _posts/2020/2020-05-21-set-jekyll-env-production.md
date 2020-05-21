---
title: "Jekyll 开启生产模式方法"
categories:
  - blog
tags:
  - 博客
toc: false
toc_sticky: true
toc_label: "标题"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
通常在修改完 Jekyll 博客，推送之前，都需要先在本地运行以下命令预览，确认修改无误后再进行提交。
```
bundle exec jekyll serve
```

但是，默认开发模式下，运行上述命令不能在本地预览评论系统样式，这时就需要把环境变量设置为生产模式。

执行以下命令将环境变量设置为生产模式
```
set JEKYLL_ENV=production
```
接下来执行 `jekyll build` 或者 `jekyll server`

如果想切换回开发模式，执行以下命令
```
set JEKYLL_ENV=development
```
