---
title: "修改主题之在标题下方添加文章发布时间"
categories:
  - tutorial
  - blog
tags:
  - 博客
  - 代码
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---

对于现在所使用的 Jekyll 主题 [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/)，作者非常的勤奋，不断地在更新主题。但是主题也有不符合我使用习惯的地方，一般为了方便于审阅博文便于查看发布时间，在标题的下方都会有发布时间，类似于下图。

![sample pic](https://i.loli.net/2019/12/28/jThQoDzX5vApki8.png)

但是 [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) 这款主题却只在文章标题下方显示阅读时间，`_config.yml` 文件中也并没有加入发布时间的调节代码，所以只能自己另辟跂径。于是我在与我使用相同主题的一位朋友的 [博客](https://ericluo.github.io/) 下参考到了一个方法——在阅读时间图标之后添加发布时间，这样只要调用阅读时间代码，就会一同显示出发布时间。

操作方法就是在 `_includes/read-time.html` 后添加以下代码

![code](https://i.loli.net/2020/01/01/ZTFpg3bWI8JU6LP.png)

更改后效果如下

![publish time pic](https://i.loli.net/2019/12/28/L5AfzRZJgY4yGIk.png)