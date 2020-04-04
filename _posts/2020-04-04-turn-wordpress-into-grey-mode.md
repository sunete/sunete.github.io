---
title: "清明节将WordPress转换为灰色模式"
categories:
  - tutorial
  - blog
tags:
  - WordPress
  - 清明节
  - 灰色模式
  - 代码
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
今天是4月4日清明节，举国都在为逝世的烈士哀悼。想着我也应该做一点什么。作为一名“半吊子站长”，我也要模仿其他站长，在今天把自己的网站变为灰色色。于是就着手在网上搜教程，把之前搭建好的WordPress网站用代码改为灰色色调，以哀悼逝世的英雄们。

但是再找好教程和代码之后，进入后台编辑主题css文件时却出现了bug——每次想要添加代码备注时，回车后，网页就会卡死。

虽然失败了一次，但是我还没放弃，继续在网上找其他人的解决办法，最终，在比较多篇文章之后，终于成功将网站变成了灰色色调！

![enter image description here](https://s1.ax1x.com/2020/04/04/GdgFjP.png)

问题出在我修改`style.css`样式表文件上，每次修改这一文件，都会导致卡死。但之后参考其他文章，在`header.php`的`<head>之间任意位置<head>`添加以下代码，成功解决了之前的问题。
```
<style type="text/css">
    html {
        filter: grayscale(100%); 
        -webkit-filter: grayscale(100%); 
        -moz-filter: grayscale(100%); 
        -ms-filter: grayscale(100%); 
        -o-filter: grayscale(100%); 
        -webkit-filter: grayscale(1);
    }
</style>
```

修改后的代码
![enter image description here](https://s1.ax1x.com/2020/04/04/Gdgphd.png)

后面又发现了更加简单的更改方法，可直接在WordPress主题设置中修改。
 1. 进入WordPress后台-外观-自定义-额外CSS：
 2. 然后粘贴下方代码，点击发布即可
```
html {
filter: progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);
-webkit-filter: grayscale(100%);
}
```
其他主题直接将代码添加到css文件中即可。

虽说已经成功将网站更改为灰色色调，但是能否用代码实现，在每年清明节网站自动转换为灰色模式呢？这应该需要定时代码来实现。我不会代码，Google搜索也没有相关文章，所以只能这样手动操作了。

参考文章：

- [将WordPress变成黑白双色风格以示哀悼的方法](https://www.arefly.com/wordpress-black-white/)
- [一行 CSS 代码实现整个网站网页变黑白灰的效果](https://oldtang.com/2793.html)
- [WordPress 全站变灰CSS代码分享及使用方法](https://wangdalao.com/3179.html)