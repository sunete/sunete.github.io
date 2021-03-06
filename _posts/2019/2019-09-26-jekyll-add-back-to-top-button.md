---
title: "Jekyll 博客添加回到顶部按钮"
categories:
  - website
tags:
  - 网站
  - 教程
  - Jekyll
toc: true
toc_sticky: true
---

## 博客搭建进度
这几天只要有空闲时间，就在完善博客的设置。大致完成了以下几项
- [x] 设置网站关于页面
- [x] 设置网站归档页面 
- [x] 学会在博文添加侧边栏目录
- [ ] ~~为网站添加valine评论系统~~
- [x] 博客添加回到顶部按钮

## 详细工作内容

### 设置网站关于界面
关于界面最开始一直显示 404，找不到原因。之后不断地和同主题的其他人的博客文件进行对比才发现是没有在 `_pages` 文件夹中添加 `about.md` 的页面文件。最后添加上 `about.md` 之后，网站关于页面正常跳转到已编辑的关于页面。不仅如此，顺带学习了一下 markdown 语法中的居中代码。
```yaml
    <center>居中文字</center>
```
效果如下
<center>居中文字</center>

### 设置网站归档页面
最初网站归档页面也没有，主要原因是从 GitHub 上 clone 下来的主题文件中没有 `_pages` 文件夹，于是我单独创建了一个文件夹用于存放网页文件，问题解决。原本是想把归档的三个链接：按时间归档、按分类归档、按标签归档，放在左侧边栏，但是没有找到怎样设置左侧边栏，待填坑。

### 给文章添加侧边栏目录
在阅读文章时想直接跳转到自己想看的部分时，侧边栏的作用就体现出来了。点击侧边栏上的小标题，即可跳转，非常方便，于是就研究了一下侧边栏实现方法。侧边栏目录在原主题中已有代码，只是之前不知道且不会设置。

在一番 Google 之后，发现侧边栏目录是借助于 toc(Table of Content) 来实现的。大多数 Jekyll 网站添加侧边栏是通过官方推荐的 [jekyll-toc-generator](https://github.com/dafi/jekyll-toc-generator "jekyll-toc-generator") 来实现的。在博客主题文件中已经存在了 toc 文件，所以并不用再次去安装，只需要在相应的文章内部调用即可。调用代码在主题作者的博客 [《Layout: Post with Table of Contents 》](https://mmistakes.github.io/minimal-mistakes/layout-table-of-contents-post/) 中也提到了。

调用方法：在文章开头添加代码

```yaml
---
toc: true # 是否开启 toc
toc_sticky: true # 固定侧边栏
toc_label: "Unique Title" # 侧边栏标题
toc_icon: "heart"  # 侧边栏图标，留空默认为书本图标
---
```

### Jekyll 添加 valine 评论系统
学会开启评论后就没有打开评论，毕竟只是一个小站，不需要什么评论。前面试着使用了 [utterances comments](https://github.com/utterance/utterances) ——一款基于 GitHub issues 的评论工具。utterances 配置方法很简单，我主要参考了文章 [《博客使用 utterances 作为评论系统》](https://www.cnblogs.com/stevexu/p/10808134.html) 。utterances 颜值很高，无需翻墙即可使用，但是需要 GitHub 账号登录，考虑到访问博客的用户不一定有 GitHub 账号，所以没有使用。

之后发现了 [valine comments](https://github.com/xCss/Valine) 。valine comments 不仅界面简洁，无广告，而且还不用评论者登录留言，非常棒的一款评论系统。但是按照 Duter2016 的教程 [Jekyll添加Valine评论「邮件通知和评论列表头像」](https://duter2016.github.io/2019/09/18/Jekyll%E6%B7%BB%E5%8A%A0Valine%E8%AF%84%E8%AE%BA-%E9%82%AE%E4%BB%B6%E9%80%9A%E7%9F%A5%E5%92%8C%E8%AF%84%E8%AE%BA%E5%88%97%E8%A1%A8%E5%A4%B4%E5%83%8F/) 配置后却不能正常显示。头大！

### 博客添加回到顶部按钮
博客还缺少的一个就是 Top 按钮，回到顶部还是必要的。虽然说主题内封装有回到顶部的 js 文件，奈何我这个程序小白完全不会调用，只好上 Google 搜索解决办法。最终在网页内加上了回到顶部按钮。这是我最有成就感的一点成功之处（可能很简单的一件事）。

将以下代码添加到博文采用的布局 html 文件的最后

```yaml
<div id="backtop">
   <a href="#">TOP</a>
</div> 
```

添加按钮的 css 样式

```yaml
#backtop a { /* back to top button */
    text-align: center;
    line-height: 50px;
    font-size: 16px;
    width:50px;
    height: 50px;
    position: fixed;
    bottom: 10px; /* 小按钮到浏览器底边的距离 */
    right: 60px; /* 小按钮到浏览器右边框的距离 */
    color: rgb(64,120,192); /* 小按钮中文字的颜色 */
    z-index: 1000;
    background: #fff; /* 小按钮底色 */
    padding: auto; /* 小按钮中文字到按钮边缘的距离 */
    border-radius: 50px; /* 小按钮圆角的弯曲程度（半径）*/
    -moz-border-radius: 50px;
    -webkit-border-radius: 50px;
    font-weight: bold; /* 小按钮中文字的粗细 */
    text-decoration: none !important;
    box-shadow:0 1px 2px rgba(0,0,0,.15), 0 1px 0 #ffffff inset;
}

#backtop a:hover { /* 小按钮上有鼠标悬停时 */
    background: rgba(64,120,192,0.8); /* 小按钮的底色 */
    color: #fff; /* 文字颜色 */
}
```



## 参考文章
- [Jekyll博文内链和返回顶部按钮](https://www.smslit.top/2015/10/28/backToTop-Jekyll/)  
- [爲 Jekyll 博客添加目錄與 ScrollSpy 效果](https://www.twblogs.net/a/5b8cb2332b71771883349fde)    
- [为 Jekyll 博客添加目录与 ScrollSpy 效果](http://t.hengwei.me/post/为jekyll博客添加目录与scrollspy效果.html)