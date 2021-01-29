---
title: "Github 加速下载方案"
categories:
  - tutorial
tags:
  - GitHub
  - 分享
toc: true
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
上网找的几个 GitHub 加速下载方法，推荐修改系统 hosts 的方法，一劳永逸。其他方法下载加速效果因人而异，收藏备用。

## 在线网页
在线下载网站的方便之处在于不受限于设备，随开随用，但加速效果还是受限于网络状况。

大多数网站的原理都是借助于 Cloudflare Workers 中转加速下载。这里不禁感叹一句：**CF！永远滴神！**

1. <http://toolwa.com/github/> 基于 [FastGit][1] 搭建
2. <https://d.serctl.com/>
3. <https://gh.api.99988866.xyz/> 基于 [gh-proxy][2] 搭建
4. <https://ghproxy.com/> 基于 [gh-proxy][2] 搭建

## 浏览器插件
仅适用于 Chrome 浏览器，其他浏览器适用性未知。

[GitHub 加速][3]{: .btn .btn--info}

## 油猴脚本
要使用该脚本，需要浏览器安装 **Tampermonkey 脚本管理器扩展**（[Chrome][4] | [Firefox][5] | [Edge][6]）。

[GitHub 增强-高速下载][7]{: .btn .btn--info}
[Github 镜像访问，加速下载][8]{: .btn .btn--info}

### 脚本中使用到的加速网站
#### Release、Code(ZIP) 文件加速：

https://gh.con.sh	美国

https://gh.api.99988866.xyz	美国

https://download.fastgit.org	日本东京

https://github.xiu2.xyz	日本东京

https://ghproxy.com	韩国首尔

https://pd.zwc365.com	中国香港

#### Git Clone 加速：

https://hub.fastgit.org	中国香港	

https://gitclone.com	中国浙江杭州	

https://github.com.cnpmjs.org	新加坡	

#### Raw 文件加速：

https://raw.sevencdn.com	中国国内	

https://cdn.jsdelivr.net	中国国内	

https://raw.fastgit.org	中国香港	

## 修改 hosts
通过修改系统的 hosts 文件也可实现加速效果，具体实现方法可参考文章 [《GitHub（国内）加速》][9]。

下面是我通过 [站长工具][10] 查询后在 hosts 中添加的内容

```
13.229.188.59 github.com

185.199.110.153 assets-cdn.github.com
185.199.108.153 assets-cdn.github.com
185.199.109.153 assets-cdn.github.com
185.199.111.153 assets-cdn.github.com

151.101.229.194 github.global.ssl.fastly.net
```

[1]: https://github.com/fastgitorg/document
[2]: https://github.com/hunshcn/gh-proxy
[3]: https://chrome.google.com/webstore/detail/github加速/mfnkflidjnladnkldfonnaicljppahpg/related?hl=zh-CN
[4]:https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo
[5]:https://addons.mozilla.org/firefox/addon/tampermonkey/
[6]: https://microsoftedge.microsoft.com/addons/detail/tampermonkey/iikmkjmpaadaobahmlepeloendndfphd?hl=zh-CN
[7]: https://greasyfork.org/zh-CN/scripts/412245-增强-高速下载
[8]: https://greasyfork.org/zh-CN/scripts/398278-github-镜像访问-加速下载
[9]: https://www.cnblogs.com/wylshkjj/p/13369627.html
[10]: http://tool.chinaz.com/dns
