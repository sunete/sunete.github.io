---
title: "Bilibili 视频适应页面宽度"
categories:
  - tutorial
tags:
  - 网站
  - Jekyll
  - 教程
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
## 哔哩哔哩视频嵌入问题
之前在一篇文章中想要插入哔哩哔哩视频，从B站视频下方点击分享按钮获取 iframe 嵌入代码，形式如下

```
<iframe src="//player.bilibili.com/player.html?aid=24220173&bvid=BV1KW411N7vE&cid=40606466&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

如果直接将代码插入到文章内部，会有 2 个很明显的问题。

一、视频并不能自动适应网页宽度，嵌入后视频窗口太小，不适合观看

![](https://cdn.jsdelivr.net/gh/sunete/imghost/img2020-04-13_09-47-04.png)

二、直接嵌入的视频会自动播放弹幕，如果弹幕较多，会遮挡视频，影响观感

![](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200413182227.png)

所以，想在文章中嵌入哔哩哔哩视频，并达到适宜观看的目的，就必须解决上面两个问题。

## 哔哩哔哩视频嵌入问题解决办法

### 哔哩哔哩视频适应网页宽度
视频太小的原因是宽高不够，之前我的解决办法是直接在嵌入代码中设置视频的宽高。但是这么做的缺点也很明显，固定了视频的宽高后，只有网页适宜观看，移动端的观感就非常不好，大小不合适。

但是回头想一想，为什么这个主题嵌入 YouTube 视频可以自动适应电脑端和移动端呢？肯定是有相应的调节代码。于是就在主题的 css 代码中寻找相应的样式代码。最终发现视频大小调节代码在 `_sass\minimal-mistakes\_utilities.scss` 中。[点击查看代码](https://github.com/sunete/sunete.github.io/blob/999d4aeba6e5772303668b1f26a0d74e71d99c69/_sass/minimal-mistakes/_utilities.scss#L538)

以下为代码内容。

```
/*
   Responsive Video Embed
   ========================================================================== */

.responsive-video-container {
  position: relative;
  margin-bottom: 1em;
  padding-bottom: 56.25%;
  height: 0;
  overflow: hidden;
  max-width: 100%;

  iframe,
  object,
  embed {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
}
```

既然主题 css 内包含等比缩放 css 类，那么不论是用 iframe 嵌入什么视频，都可以自动适应宽度。只需要像下面一样，用 `responsive-video-container` 类的块内容把 iframe 包起来即可。

```
<div class="responsive-video-container">
  <iframe src="//player.bilibili.com/player.html?bvid={{ video_id }}&page=1&as_wide=1&high_quality=1&danmaku=0" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
</div>
```

### 关闭哔哩哔哩视频弹幕
如果你仔细观察，就会发现，上面我所列出的视频 iframe 嵌入代码和直接获取的代码稍有区别。

直接获取的代码是这样的：
```
<iframe src="//player.bilibili.com/player.html?aid=497646355&bvid=BV1tK411L7W5&cid=176555911&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

我所列出的代码时这样的
```
<iframe src="//player.bilibili.com/player.html?bvid={{ video_id }}&page=1&as_wide=1&high_quality=1&danmaku=0" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```
其中最重要的，用来关闭弹幕的代码就是 `danmaku`。其取值为 `1` 代表开启弹幕，取值为 `0` 代表关闭弹幕。

### 其他 iframe 链接参数
除上面提到的 `danmaku` 之外，iframe 嵌入代码还有视频清晰度、开始播放时间等其他的参数可以配置。

![](https://cdn.jsdelivr.net/gh/sunete/imghost/img20200413172503.png)

### 视频测试
[Bilibili 视频](https://www.bilibili.com/video/BV1Vb41177ud)

{% include video id="BV1Vb41177ud" provider="bilibili" %}

## 参考文章
- [【前端笔记】使用 iframe 嵌入等比缩放的哔哩哔哩视频](https://blog.potatofield.cn/%e3%80%90%e5%89%8d%e7%ab%af%e7%ac%94%e8%ae%b0%e3%80%91%e4%bd%bf%e7%94%a8iframe%e5%b5%8c%e5%85%a5%e7%ad%89%e6%af%94%e7%bc%a9%e6%94%be%e7%9a%84%e5%93%94%e5%93%a9%e5%93%94%e5%93%a9%e8%a7%86%e9%a2%91/)
- [接入B 站 iframe 视频(bilibili 引用视频)](https://blog.csdn.net/xinshou_caizhu/article/details/94028606)