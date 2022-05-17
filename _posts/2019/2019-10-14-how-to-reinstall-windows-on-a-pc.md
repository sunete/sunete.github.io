---
title: "重装 Windows 系统"
categories:
  - tutorial
tags:
  - Windows
  - 教程
toc: true
toc_sticky: true
toc_label: "如何重装系统"
toc_icon: " "  # Font Awesome对应图标名称 (无fa前缀)	
---
电脑从买来，到使用一段时间，总会经历重装系统。有的人可能是送去电脑维修店重装系统，有些人可能是请朋友帮忙，但不论如何，自己会重装是最方便的，而且这也是一项小技能。所以在此写一篇关于重装系统的教程。

## 准备器材
1. 一台联网电脑    
2. 至少 8G 的 U 盘    
3. 启动盘制作工具 [Rufus](https://rufus.ie/)    
4. Windows ISO 镜像
5. 电脑对应版本驱动（非必须）

## 下载Windows镜像
官方 Windows 镜像可以到 [MSDN我告诉你](https://msdn.itellyou.cn/) 下载.

官方网站：<https://msdn.itellyou.cn/>    

这里以 Windows7 专业版镜像为例 

1. 点击链接进入官网    
2. 点击操作系统    
3. 选择所需系统镜像，这里选择 `Windows 7 Professional (x64) - DVD (Chinese-Simplified)`    
4. 点击 `详细信息` 可以找到镜像下载链接	

```yaml
ed2k://|file|cn_windows_7_professional_x64_dvd_x15-65791.iso|3341268992|3474800521D169FBF3F5E527CD835156|/
```

5. 复制链接到迅雷，点击下载。
[![20201211174951](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211174951.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211174951.png)
 
## 下载启动盘制作工具 Rufus
[Rufus](https://rufus.ie/) 是一个开源免费的快速制作 U 盘系统启动盘和格式化 USB 的实用小工具，它可以快速把 ISO 格式的系统镜像文件快速制作成可引导的 USB 启动安装盘，支持 Windows 或 Linux 启动。Rufus 小巧玲珑，软件体积仅 1.1MB，然而麻雀虽小，它却五脏俱全，而且速度极快。

官方网站：<https://rufus.ie/> 

进入官网，选择下载 `Rufus 3.8 Portable (1.1 MB)`。便携版即可，也可以选择安装版。

[![20201211175040](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211175040.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211175040.png)

## 制作 U 盘启动盘
将U盘插入电脑，打开 Rufus。    
1. 设备选择要制作为启动盘的 U 盘    
2. 选择已经下载好的 ISO 镜像文件           
3. 分区类型选择 GPT        
4. 目标系统类型选择 UEFI
5. 点击开始即可刻录 
     
[![20201211175247](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211175247.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211175247.png)

由于目前大部分电脑都支持 UEFI+GPT 的设置，只要是新装的主流配置电脑，在默认的环境下都支持 UEFI+GPT 的配置，所以在分区类型和目标系统类型里面，选择 UEFI 和 GPT 即可。开始刻录后，等下方绿条走完并显示完成后即可安全弹出 U 盘，把 U 盘插到需要安装系统的电脑里，开始装系统吧！

## 安装系统

### 进入 BIOS
把制作好的启动盘插入电脑，在**开机前之**连续点击键盘上的 BIOS 按钮即可进入菜单（不同机器快捷键有所不同，主要集中在 F6-F12 等按键）。    
具体按什么键，参照下表（某些机型可能有所不同）

| 组装机主板  | 组装机按键  | 笔记本电脑  | 笔记本按键  | 台式机品牌  | 台式机按键  |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  华硕主板 | F8  |  联想笔记本 | F12  |  联想台式机 | F12  |
|  技嘉主板 | F12  |  宏基笔记本 |  F12 | 惠普台式机  | F12  |
| 微星主板  | F11  |  华硕笔记本 | ESC  | 宏基台式机  | F12  |
| 映泰主板  |  F9 |  惠普笔记本 | F9  |  戴尔台式机 | ESC  |
|  梅捷主板 | ESC或F12  | 联想Thinkpad  | F12  |  神州台式机 |  F12 |
| 七彩虹主板  |  ESC或F11 |  戴尔笔记本 |  F12 | 华硕台式机  | F8  |
|  华擎主板 |  F11 | 神舟笔记本  |  F12 |  方正台式机 | F12  |
| 斯巴达卡主板  | ESC  | 东芝笔记本  | F12  | 清华同方台式机 |  F12 |
|  昂达主板 | F11  | IBM笔记本  |  F12 |  海尔台式机 | F12  |
| 双敏主板  |  ESC | 富士通笔记本  | F12  |  明基台式机 | F8  |
|  翔升主板 |  F10 | 海尔笔记本  | F12  |   |   |
| 精英主板  |  ESC或F11 | 方正笔记本 |  F12 |   |   |
|  冠盟主板 |  F11或F12 | 清华同方笔记本  | F12  |   |   |
|  富士康主板 | ESC或F12  |  微星笔记本 |  F11 |   |   |
| 顶星主板  |  F11或F12 |  明基笔记本 | F9  |   |   |
|  铭瑄主板 |  ESC | 技嘉笔记本  |  F12 |   |   |
|  盈通主板 |  F8 |  Gateway笔记本 |  F12 |   |   |
| 捷波主板  |  ESC |  eMachines笔记本 |  F12 |   |   |
| Intel主板  |  F12 |  索尼笔记本 | ESC  |   |   |
|  杰微主板 |  ESC或F8 | 苹果笔记本  | 长按**option**键  |   |   |
|  致铭主板 |  F12 |   |   |   |   |
| 磐英主板  |  ESC |   |   |   |   |
|  磐正主板 | ESC  |   |   |   |   |
|  冠铭主板 |  F9 |   |   |   |   |

如果成功进入 BIOS 界面，一般会如下图

[![20201211180552](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211180552.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211180552.png)

此时，你需要知道你的 U 盘的名字，一般如果是大牌的 U 盘都会有自己的品牌名字，而如果是偏杂牌的 U 盘则可能带“UDISK”字样。这里刻录的 U 盘是东芝的 U 盘，所以带有系统的 U 盘为第四个与第七个。

为了安装 UEFI，我们选择带有 UEFI 字样的 U 盘选项，也就是第七个。

### 系统安装
选择后，就会进入对应品牌的 UEFI 界面，稍等片刻，便进入了装系统界面。当然由于不同系统有不同的安装界面，以下界面仅供参考。

[![20201211180818](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211180818.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211180818.png)

点击开始安装，接下来就是傻瓜式安装了。

### 自定义，仅安装 Windows

[![20201211181004](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211181004.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211181004.png)

### 选择系统盘，配置容量
重装系统可以把除了存有你重要数据以外的所有盘符删掉，点击新建，设置容量，然后它会提示你新建一些用于系统功能的分区，点击确认，然后选择下一步即可。

[![20201211181035](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211181035.png)](https://fastly.jsdelivr.net/gh/sunete/imghost/img20201211181035.png)

之后便是漫长的等待啦。等电脑重启后，系统会继续安装，根据步骤执行操作即可。

