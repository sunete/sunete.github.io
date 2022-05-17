---
title: "使用 GitHub Action 持续构建 Algolia"
categories:
  - website
tags:
  - 网站
  - GitHub
  - 教程
toc: true
toc_sticky: true
toc_label: "教程"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
因为没有数据库，所以静态博客本身无法进行站内搜索，需要借助于第三方的搜索引擎来实现。[Minimal Mistakes][2] 内置 lunr (default), algolia, google 三种搜索引擎。

如果你用过本博客的搜索功能，而且足够仔细，可能会发现，我的网站所用的搜索功能是由 [Algolia][1] 驱动。

[![20210227154458](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210227154458.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210227154458.png)

Algolia 的配置，在搭建博客之初就已经配置好了。当时是利用 [Travis-CI][3] 自动化提交索引，只要我进行任何文件改动，Travis-CI 都会自动提交、部署，配合 Algolia 实现站内搜索。

但是去年 Travis-CI 改变了策略，免费部署额度大大降低，加上我还在上面部署了自动签到，所以很快超出了限额，导致我的博客站内搜索 5 个多月没能更新。

好在最近 [Minimal Mistakes][2] 项目中 [@dieghernan][4] 提出用 GitHub Action 来替代 Travis-CI 的 [方案][5]。于是我按照配置教程顺利为博客配置上了 GitHub Action + Algolia 的组合方案。

在此特别感谢 [@dieghernan][4] 提供解决方案。

具体的实现方法很简单：参考 [官方文档][6] 给 Jekyll 博客配置 Algolia 后，新建 GitHub Action 运行所需文件并添加 secret 即可。

## 一、安装 jekyll-algolia 插件
在博客 `Gemfile` 文件，插件部分添加 `gem 'jekyll-algolia'`。示例代码如下

```
source "https://rubygems.org" # 插件所需要的 Ruby 环境

gem 'jekyll', '~> 3.6' # Jekyll 版本需要 3.6.0 以上

group :jekyll_plugins do
  gem 'jekyll-archives'
  gem 'jemoji'
  gem 'jekyll-algolia' # 这行是新增的，用于添加 jekyll-algolia 插件
end
```
之后运行 `bundle install` 安装依赖。如果一切正常，运行 `bundle exec jekyll help` 就能看到 `algolia` 子命令。

## 二、编辑 config.yml
注册 Algolia 后，在 [控制面板][7] 获取 `application_id` 、 `index_name` 和 `search_only_api_key`。

在 `config.yml` 文件添加以下代码。注意替换相应值。
```
# _config.yml

algolia:
  application_id         : Algolia_APPLICATION_ID
  index_name             : Algolia_INDEX_NAME
  search_only_api_key    : Algolia_SEARCH_ONLY_API_KEY
```

## 三、使用 Algolia
按照上面的步骤配置完后，就能运行下面的命令来进行索引（以 Windows 为例）
```
set ALGOLIA_API_KEY=your_admin_api_key
bundle exec jekyll algolia
```
若出现 **Error: invalid byte sequence in GBK** 错误，可先执行 `chcp 65001`。

## 四、设置 GitHub Secret
到 GitHub Pages 博客项目下，在 Settings > Secrets 新增一个 Secret，名称为 `ALGOLIA_API_KEY` ，值为在  Algolia [控制面板][7] 获取的 Admin API Key 。

[![20210227183630](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210227183630.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210227183630.png)

## 五、新建 Workflow 文件
在博客项目 `/.github/workflows/` 文件夹下新建一个工作流程 yml 文件，例如 `algolia-search.yml`，并在文件中添加如下代码

[点击查看代码](https://github.com/dieghernan/algolia-jekyll-action#the-action){: .btn .btn--primary}

添加完成后，在博客的 main 或者 master 分支有任何的提交，都会运行 GitHub Action 进行自动构建。

[![20210227185532](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210227185532.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20210227185532.png)

参考项目：<https://github.com/marketplace/actions/algolia-jekyll-action>


[1]: https://www.algolia.com/
[2]: https://github.com/mmistakes/minimal-mistakes
[3]: http://travis-ci.com/
[4]: https://github.com/dieghernan
[5]: https://github.com/mmistakes/minimal-mistakes/discussions/2807
[6]: https://community.algolia.com/jekyll-algolia/getting-started.html
[7]: https://www.algolia.com/api-keys