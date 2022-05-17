---
title: "离线下载工具 Cloud Torrent 搭建教程"
categories:
  - tutorial
tags:
  - 教程
  - VPS
  - 分享
  - 影视
toc: true
toc_sticky: true
toc_label: "Cloud Torrent 搭建教程"
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
网上看到有人介绍可以离线下载 BT 和磁力的项目 [Cloud Torrent](https://github.com/jpillora/cloud-torrent)，于是就去试着自己弄了一下，用 doubi 大佬的一键脚本，非常简单，傻瓜式操作，很快就搭建成功了。

下面就来写个教程水一篇文章，老司机赶快上车，嘀嘀嘀~~~

## 系统要求
CentOS / Debian / Ubuntu 都可以，本教程基于 Debian 10 X64

## 安装教程
服务器 root 账户登录后执行一键脚本
```html
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/cloudt.sh && chmod +x cloudt.sh && bash cloudt.sh
```
出现安装菜单

{% highlight shell linenos %}
 0. 升级脚本

 1. 安装 Cloud Torrent
 2. 升级 Cloud Torrent
 3. 卸载 Cloud Torrent
————————————
 4. 启动 Cloud Torrent
 5. 停止 Cloud Torrent
 6. 重启 Cloud Torrent
————————————
 7. 设置 Cloud Torrent 账号
 8. 查看 Cloud Torrent 账号
 9. 查看 Cloud Torrent 日志
————————————

 当前状态: 已安装 并 已启动

 请输入数字 [0-9]:
{% endhighlight %}

输入`1` 执行安装 Cloud Torrent。后面的端口以及用户名、密码等按需设置就行，也可以一路回车默认。

安装完成后就可以通过 `IP: 端口` 访问使用 Cloud Torrent 了。

## 使用方法

### 搜索磁力链接
在输入框输入想要搜索资源的名称，点击搜索，点击绿色按钮可以切换搜索源。找到想要的资源后点击其右侧下载按钮，就可以将其添加到任务列表中。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200528121045.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200528121045.png"></a> </figure>

### 离线下载
直接在输入框中输入磁力链接，点击下方 **Load Magnet** 按钮，下载任务就添加上了。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200528112400.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200528112400.png"></a> </figure>

BT 下载，点击输入框右侧上传按钮，选择种子文件，上传后会自动开始下载。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200528114534.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200528114534.png"></a> </figure>

## 测试效果
最近[《天气之子》][2]这部动漫电影很火，刚出了 BD 版本，就去 [bt之家][1] 下载了蓝光 4K 版本种子。测试离线速度很快，大约 20MB/s。当然，离线速度除了取决于服务器性能外，还与种子的热度有关，越热门的资源离线速度越快。

<figure> <a href="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200528091833.png"><img src="https://fastly.jsdelivr.net/gh/sunete/imghost/img20200528091833.png"></a> </figure>

## 常见问题

- **启动失败，日志提示：listen tcp IP:端口: bind: address already in use**

    这种情况是你绑定的网页访问端口被其他程序占用，你需要去关闭占用的程序，或者修改绑定的端口

    查看占用程序：

    ```
    netstat -lntp
    ```

    找到 0.0.0.0:你绑定的端口 这一行，看后面的程序名字，例如是 80 端口，然后被 nginx 占用了，那么这样关闭：

    ```
    /etc/init.d/nginx stop

    # 并且取消开机启动，避免与 Cloud Torrent 开机启动冲突。
    update-rc.d -f nginx remove
    ```

    如果你用上面的方式替换 nginx 发现无法停止，那么就直接终止进程，先看到进程的PID，也就是 xxx/nginx 这一列前面的 xxx 这个数字，然后输入命令：

    ```
    kill -9 PID进程数字
    ```

    然后再去尝试启动Cloud Torrent。

- **无法访问你的 http://IP:端口**

    可能是防火墙规则的问题，脚本已经默认设置了内部防火墙开放了端口规则，而部分VPS可能有外部防火墙，例如：阿里云、腾讯云、微软云、谷歌云、亚马逊云等，你需要去他们的后台找到 安全组/规则组 一类的选择去开放端口（分别是你的访问网页端口，例如 80，和BT下载端口 50007）

- **wget: unknown host "yun.doubibackup.com" 之类的错误**

    这是无法解析我的域名，多半是DNS的问题，请更换DNS为谷歌DNS。
    ```
    echo -e "nameserver 8.8.8.8\nnameserver 8.8.4.4" > /etc/resolv.conf
    ```

- **wget: command not found**

    这是你的系统精简的太干净了，wget 都没有安装，所以需要安装 wget。

    CentOS系统:
    ```
    yum install -y wget
    ```
    Debian/Ubuntu系统:
    ```
    apt-get install -y wget
    ```

## 参考文章
- [逗比根据地 Cloud Torrent 一键脚本](https://doubibackup.com/q7gcd25g-2.html)

- [Github--Cloud Torrent](https://github.com/jpillora/cloud-torrent)

[1]: https://www.btbtt.co
[2]: [https://www.imdb.com/title/tt9426210/]