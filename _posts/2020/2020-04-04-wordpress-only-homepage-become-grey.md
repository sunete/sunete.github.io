---
title: "WordPress 仅使主页变为灰色模式"
categories:
  - tutorial
tags:
  - WordPress
  - 代码
  - 灰色模式
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
在上一篇文章[《清明节将 WordPress 转换为灰色模式》](https://sunete.github.io/tutorial/turn-wordpress-into-grey-mode/)，我已经讲述了如何将 WordPress 网站转换为灰色。但是经过一上午的感受，个人感觉网页体验非常不好。主要原因是，今天大多数网站都采用灰色模式，长时间浏览灰色网页，眼睛很不舒服。

那该怎么做才能既将网站变为灰色哀悼烈士，又不必长时间浏览灰色网页呢？我最终在 [吾爱破解论坛](https://www.52pojie.cn/) 中找到了解决办法。

吾爱破解论坛并没有将所有网页变为灰色，而是仅仅把论坛主页转为灰色。

![enter image description here](https://s1.ax1x.com/2020/04/04/Gwkjrd.png)

其他子页面比如原创破解区、精品软件区等都为正常色调。

![enter image description here](https://s1.ax1x.com/2020/04/04/GwAIyQ.png)

那么 WordPress 能否做到这一点呢？当然可以！

这里只需要将主页样式改变，而其他页面文件不去修改。做法就是把以下代码添加到首页模板 `index.php` 中。
```
<style> 
    html { 
        -webkit-filter: grayscale(100%); 
        -moz-filter: grayscale(100%); 
        -ms-filter: grayscale(100%); 
        -o-filter: grayscale(100%); 
        filter:progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);  
        _filter:none; 
    } 
</style>
```
以下是添加灰色代码后的 `index.php` 文件

![enter image description here](https://s1.ax1x.com/2020/04/04/GwVugU.png)

插入代码后，点击 `更新文件` 即可生效。再去看一下网站，就会发现，只有首页是灰色，而其它页面还是正常颜色的。
