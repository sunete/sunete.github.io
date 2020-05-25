---
title: "【转载】WordPress 更改固定链接 404 的解决办法"
categories:
  - tutorial
tags:
  - 网站
  - 教程
  - WordPress
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
本文转载自：[沈唁志博客][1]——[《WordPress更改固定链接404的解决办法》][2]

最近在阿里云 ECS 服务器上搭建了一个 Wordpress 网站，在修改主题固定链接后出现了页面 404 的问题，于是 Google 搜索解决方法，找到了此篇文章，顺利地用宝塔修改伪静态解决了这一问题，遂转载至博客。以下为原文内容。

----------

WordPress 网站建设中，固定链接设置是必不可少的，好的固定链接更美观、易用、利于用户分享和搜索引擎收录，需要注意的是，要使设置的固定链接生效的前提是你的网站环境支持伪静态。

## 常用参数有

 1. 日期和名称型 /% year%/% monthnum%/% day%/% postname%/
 2. 月份和名称型 /% year%/% monthnum%/% postname%/
 3. 数字型 /archives/% post_id%
 4. 文章名 /% postname%/
 5. ID+html 型 /% post_id%.html

很多站长在玩 WordPress 的时候，可能会碰到一个问题，就是想把 WordPress 伪静态，在后台设置好固定链接之后，就会出现文章页面或者所有的页面都出现 404 错误。下面就提供各种 web 环境下的 WordPress 伪静态规则设置教程。

## Apache 伪静态规则
Apache 是 Linux 主机下常见的环境，现在一般的 Linux 虚拟主机都采用这种环境。新建一个 htaccess.txt 文件，添加下面的代码：
```html
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>
```
然后上传到 WordPress 站点的根目录，重命名为 .htaccess ，修改完成后，要重启 Apache 才能生效。

## Nginx 伪静态规则
打开`nginx.conf`或者某个站点的配置环境，比如`sunete.github.io.conf`（不同的网站配置不一样），在`server {}`大括号里面添加下面的代码：
```html
location / {  
    index index.html index.php;   
    if (-f $request_filename/index.html){   
        rewrite (.*) $1/index.html break;   
    }   
    if (-f $request_filename/index.php){   
        rewrite (.*) $1/index.php;   
    }   
    if (!-f $request_filename){   
        rewrite (.*) /index.php;   
    }   
}   
  
rewrite /wp-admin$ $scheme://$host$uri/ permanent;  
```
保存以后，重启 Nginx 即可。

## IIS 伪静态
强烈不推荐在 windows 的 IIS 服务器下安装 WordPress，因为 IIS 环境运行 PHP 程序的效率，相对同等配置下 Linux 的 Apache 和 Nginx 环境，要低的多，更甚至于坑太多！
```html
[ISAPI_Rewrite]
# Defend your computer from some worm attacks
#RewriteRule .*(?:global.asa|default\.ida|root\.exe|\.\.).* . [F,I,O]
# 3600 = 1 hour
CacheClockRate 3600
RepeatLimit 32
# Protect httpd.ini and httpd.parse.errors files
# from accessing through HTTP
# Rules to ensure that normal content gets through
RewriteRule /tag/(.*) /index\.php\?tag=$1
RewriteRule /software-files/(.*) /software-files/$1 [L]
RewriteRule /images/(.*) /images/$1 [L]
RewriteRule /sitemap.xml /sitemap.xml [L]
RewriteRule /favicon.ico /favicon.ico [L]
# For file-based wordpress content (i.e. theme), admin, etc.
RewriteRule /wp-(.*) /wp-$1 [L]
# For normal wordpress content, via index.php
RewriteRule ^/$ /index.php [L]
RewriteRule /(.*) /index.php/$1 [L]
```
另存为 httpd.ini 文件，上传到 WordPress 站点的根目录即可。

## 宝塔面板设置伪静态
如果你的服务器上安装了宝塔面板，就方便多了

在 宝塔面板 > 网站 > 设置 > 伪静态 里选择对应的伪静态规则（WordPress）并保存即可。

## 后记
如果你按照上述方法设置了还是不起作用，那么有可能是你的服务器没有安装伪静态模块！Apache 服务器的话，就是 rewrite 模块没有开启，去除这一行前面的 #号就可以了
```html
LoadModule rewrite_module modules/mod_rewrite.so
```


  [1]: https://qq52o.me/
  [2]: https://qq52o.me/1876.html