---
title: "怎样在 GitHub 上 Pull Request"
categories:
  - tutorial
tags:
  - GitHub
  - Pull Request
  - 博客主题
toc: true
toc_sticky: true
toc_label: "怎样Pull Request"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
在之前发布的一篇文章 [《bilibili适应页面宽度》][1] 中，我就提到了，[minimal-mistakes][2] 这个主题插入 YouTube、Vimeo、Google Drive 等国外网站视频时可以自适应页面宽度，但是国内的哔哩哔哩视频却不可以，所以我就自己尝试解决这个问题。最终，通过修改 `_includes/video` 代码，这个问题得到了解决。于是我向 [minimal-mistakes][2] 的开发者提交了 issue，请求在主题中添加哔哩哔哩视频相关代码。两天后，开发者回复我说，希望我为主题 Pull Request。

![20200430205358](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200430205358.png)

虽然 [minimal-mistakes][2] 作者希望我 Pull Request，但是从我开始使用 Github，根本没有提交过 Pull Request，所以只能求助于 Google，来为 [minimal-mistakes][2] 做出一些贡献了。下面简单介绍如何向一个 GitHub 项目 Pull Request。

## 1. Fork respository
到 GitHub 项目仓库主页，点击右上角 Fork。

![20200430210201](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200430210201.png)

## 2. clone 项目到本地并修改
在电脑上按 `Win+R` 调出运行窗口，输入 cmd，回车。

![20200430211409](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200430211409.png)

在 cmd 窗口输入 `git clone 仓库网址`，将项目克隆到本地。

![20200501093725](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200501093725.png)

在 VSCode 中修改代码保存，并上传到 GitHub 仓库。

![20200501093925](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200501093925.png)

## 3. GitHub 网页端 Pull Request
访问你自己刚 clone 并修改的的项目主页，点击 `New pull request`。

![20200501094541](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200501094541.png)

跳转到原作者项目主页后 `Creat pull request`。

![20200501094746](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200501094746.png)

新建一个 master 以外的分支，选择作者分支与该分支进行对比。之后添加相关描述提交 pull request 即可。

![20200501100058](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200501100058.png)

提交成功，等待作者 merge。

![20200501093557](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200501093557.png)



---
## 参考文章

[思否--熊丸子解答](https://segmentfault.com/q/1010000006216219)


[1]: https://sunete.github.io/tutorial/bilibili-video-adapts-to-the-width/
[2]: https://github.com/mmistakes/minimal-mistakes