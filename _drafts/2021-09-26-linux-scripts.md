---
title: "Linux 常用脚本命令"
categories:
  - tutorial
tags:
  - 教程
  - 分享
  - VPS
  - Linux
toc: true
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
## 服务器设置

### 修改服务器时区为东八区
```
cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

### 开放服务器所有端口
```
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -F
```

### 修改服务器 hosts
打开 hosts 的编辑文本模式
```
vi /etc/hosts
```

输入命令 `i` 编辑，按 `Esc` 键退出编辑，`:wq` 保存退出，`:q!` 不保存强制退出。

重启 hosts
```
/etc/init.d/network restart
```

国内服务器可以修改 hosts 实现加速 GitHub 访问效果，推荐使用 [Github520](https://github.com/521xueweihan/GitHub520) 的 hosts 。

### Cloudflare WARP 一键配置脚本
项目地址：<https://github.com/P3TERX/warp.sh>

```
bash <(curl -fsSL git.io/warp.sh) d
```

## Docker

### Docker 安装
国内主机安装 Docker
```
curl -sSL https://get.daocloud.io/docker | sh
```

国外主机安装 Docker
```
wget -qO- https://get.docker.com/ | bash
```

启动 Docker 服务
```
service docker start
```

设置 Docker 服务项开机自启( 重要 )
```
systemctl enable docker
```

### Docker Compose 安装
各平台 Docker Compose 安装可查看官方页面

<https://docs.docker.com/compose/install/>

下载 Docker Compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

国内下载 Docker Compose
```
sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

添加可执行权限
```
sudo chmod +x /usr/local/bin/docker-compose
```

查看版本测试安装结果
```
docker-compose --version
```


## 代理安装

### 233boy v2一键脚本
项目地址：<https://github.com/233boy/v2ray>

```
bash <(curl -s -L https://git.io/v2ray.sh)
```
### x-ui 
项目地址：<https://github.com/vaxilu/x-ui>

```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

## 服务器测试

### 秋水逸冰一键测试脚本 bench.sh
>bench.sh 特点：<br>
1、显示当前测试的各种系统信息；<br>
2、取自世界多处的知名数据中心的测试点，下载测试比较全面；<br>
3、IO 测试三次，并显示平均值。

详细介绍：<https://teddysun.com/444.html>

```shell
wget -qO- 86.re/bench.sh | bash
```

### 秋水逸冰 UnixBench 一键脚本
>一个开源的性能测试工具，用于测试 Linux 系统主机的性能。Unixbench 的主要测试项目有：系统调用、读写、进程、图形化测试、2D、3D、管道、运算、C库等系统基准性能提供测试数据。

详细介绍：<https://teddysun.com/245.html>

```
wget --no-check-certificate https://github.com/teddysun/across/raw/master/unixbench.sh
chmod +x unixbench.sh
./unixbench.sh
```

### Super Bench I/O 测试脚本
```
wget -qO- --no-check-certificate https://raw.githubusercontent.com/oooldking/script/master/superbench.sh | bash
```

或者

```
curl -Lso- -no-check-certificate https://raw.githubusercontent.com/oooldking/script/master/superbench.sh | bash
```

### Super Speed 一键测速脚本
```
wget https://raw.githubusercontent.com/oooldking/script/master/superspeed.sh && chmod +x superspeed.sh && ./superspeed.sh
```