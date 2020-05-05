---
title: "怎样获得YouTube频道RSS订阅链接"
categories:
  - tutorial
tags:
  - 教程
  - RSS
  - YouTube
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
有几个 YouTube 频道是我个人非常喜欢的，每当频道更新视频，我都希望能收到通知。但是我不可能每次都去用手机打开 YouTube，或者点击网页查看是否有视频更新，所以这时候就需要用RSS来订阅 YouTube 频道的更新。

但是有一个问题是，YouTube 官方并没有给出频道 RSS 订阅方式，所以就需要自己去想办法，为 YouTube 频道创建一个 RSS 订阅链接。

下面介绍几种为 YouTube 频道创建 RSS 订阅链接的方法。

## 查找 RSS 源方法
### 一、使用频道 ID 拼接 YouTube 频道 RSS 链接
这个方法适用于任何 YouTube 频道，也是我极力推荐的一种方法，非常简单。

比如我想用 RSS 订阅 YouTube 频道 [Kurzgesagt – In a Nutshell][1] 

搜索并点开频道，在地址栏复制频道链接
```html
https://www.youtube.com/channel/UCsXVk37bltHxD1rDPwtNM8Q
```
删除频道链接最后一个反斜杠以及前面的所有内容，只保留末尾的频道 ID **UCsXVk37bltHxD1rDPwtNM8Q**

将频道 ID 接在下面链接的末尾，即为频道 RSS 订阅链接
```html
https://www.youtube.com/feeds/videos.xml?channel_id=
```
[Kurzgesagt – In a Nutshell][2] 频道 RSS 订阅链接：
```html
https://www.youtube.com/feeds/videos.xml?channel_id=UCsXVk37bltHxD1rDPwtNM8Q
```

### 二、利用 feeder.co 查找 RSS 订阅源
[feeder.co][3] 是一款 RSS 订阅软件，其包含移动端 app 和 chrome 插件，这里我们利用 feeder.co 的 chrome 插件——[RSS Feed Reader][4] 来寻找 RSS 订阅链接。此方法适用于大多数包含却没有给出 RSS 订阅链接的网站，并不能为网站生成 RSS 源。

从 chrome 扩展商店中搜索并安装 [RSS Feed Reader][5]
 
扩展程序地址：<https://chrome.google.com/webstore/detail/rss-feed-reader/pnjaodmkngahhkoihejjehlcdlnohgmp>

![8BfA8x.png](https://s1.ax1x.com/2020/03/18/8BfA8x.png)

点击 feeder.co 插件图标，并点击所显示的弹窗右上角的加号，进入添加或查找 feed 页面
 
![8BfvFA.png](https://s1.ax1x.com/2020/03/18/8BfvFA.png)

在添加 feed 页面输入所需订阅的网站，点击搜索，搜索到后点击添加即可
 
![search][6]

### 三、Feedly 查找订阅源
[Feedly][7] 是一个多平台 RSS 阅读软件，功能丰富，界面设计精致。现在我的手机和 PC 端都在使用 [Feedly][8]，多平台同步，非常方便。这里简单介绍利用 Feedly 插件 [Feedly Notifier][9] 查找 RSS 源的方法。

在 chrome 应用商店搜索并安装 [Feedly Notifier][10]

扩展程序地址：<https://chrome.google.com/webstore/detail/feedly-notifier/egikgfbhipinieabdmcpigejkaomgjgb>

![Feedly Notifier][11]

安装完成后，点击菜单栏图标，并点击弹出栏左上角 Feedly 网站图标进入网站
 
![进入 feedly][12]

点击左侧栏加号搜索并添加网站 RSS，可直接输入网址查找已存在 RSS 链接并订阅

![feedly search][13]

## 总结
当然添加或者查找 RSS 源的方法不只有以上几种方法，或者软件，这里并没有全部列举出来。比如非常优秀的开源项目 [RSSHUB][14]，或者可以为没有Feed 的网页生成 RSS 订阅源的 [Feed43][15]，都是非常棒的 RSS 插件或网页。但是不论是用什么方法找到 RSS 源，只要能达到便于获取所需信息、节约时间，这些要求，就是最棒的 RSS 辅助工具。

参考文章：

[How to Get an RSS Feed for a YouTube Channel][16]

[用 RSS 訂閱 YouTube：YouTube 頻道網址轉 RSS 連結][17]


  [1]: https://www.youtube.com/channel/UCsXVk37bltHxD1rDPwtNM8Q
  [2]: https://www.youtube.com/channel/UCsXVk37bltHxD1rDPwtNM8Q
  [3]: https://feeder.co/
  [4]: https://chrome.google.com/webstore/detail/rss-feed-reader/pnjaodmkngahhkoihejjehlcdlnohgmp
  [5]: https://chrome.google.com/webstore/detail/rss-feed-reader/pnjaodmkngahhkoihejjehlcdlnohgmp
  [6]: https://s1.ax1x.com/2020/03/18/8B4SAJ.png
  [7]: https://feedly.com/
  [8]: https://feedly.com/
  [9]: https://chrome.google.com/webstore/detail/feedly-notifier/egikgfbhipinieabdmcpigejkaomgjgb
  [10]: https://chrome.google.com/webstore/detail/feedly-notifier/egikgfbhipinieabdmcpigejkaomgjgb
  [11]: https://s1.ax1x.com/2020/03/18/8DP64s.png
  [12]: https://s1.ax1x.com/2020/03/18/8DFX7D.png
  [13]: https://s1.ax1x.com/2020/03/18/8DCH6f.png
  [14]: https://docs.rsshub.app
  [15]: https://feed43.com/
  [16]: https://danielmiessler.com/blog/rss-feed-youtube-channel/
  [17]: http://blog.pulipuli.info/2017/04/rssyoutubeyoutuberss-get-rss-feed-for.html