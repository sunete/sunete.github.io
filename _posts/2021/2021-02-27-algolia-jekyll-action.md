---
title: "从 Travis CI 迁移到 GitHub Action"
categories:
  - website
tags:
  - 网站
  - GitHub
toc: false
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
因为没有数据库，所以静态博客本身无法进行站内搜索，需要借助于第三方的搜索引擎来实现。[Minimal Mistakes][2] 内置 lunr (default), algolia, google 三种搜索引擎。

如果你用过本博客的搜索功能，而且足够仔细，可能会发现，我的网站所用的搜索功能是由 [Algolia][1] 驱动。

[![20210227154458](https://cdn.jsdelivr.net/gh/sunete/imghost/img20210227154458.png)](https://cdn.jsdelivr.net/gh/sunete/imghost/img20210227154458.png)

Algolia 的配置，在搭建博客之初就已经配置好了。当时是利用 [Travis-CI][3] 自动化提交索引，只要我进行任何文件改动，Travis-CI 都会自动提交、部署，配合 Algolia 实现站内搜索。

但是去年 Travis-CI 改变了策略，免费部署额度大大降低，加上我还在上面部署了自动签到，所以很快超出了限额，导致我的博客站内搜索 5 个多月没能更新。

好在最近 [Minimal Mistakes][2] 项目中 [@dieghernan][4] 提出用 GitHub Action 来替代 Travis-CI 的 [方案][5]。于是我按照配置教程顺利为博客配置上了 GitHub Action + Algolia 的组合方案。

在此特别感谢 [@dieghernan][4] 提供解决方案。具体的配置方法作者写的很清楚，我也没必要复述，按照步骤来就行。

项目地址：<https://github.com/marketplace/actions/algolia-jekyll-action>


[1]: https://www.algolia.com/
[2]: https://github.com/mmistakes/minimal-mistakes
[3]: http://travis-ci.com/
[4]: https://github.com/dieghernan
[5]: https://github.com/mmistakes/minimal-mistakes/discussions/2807