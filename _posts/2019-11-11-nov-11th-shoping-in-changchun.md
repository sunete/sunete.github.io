---
title: "双十一出行——长春行"
categories:
  - diary
tags:
  - 旅游
  - 购物
  - 美食
  - 火车
toc: false
toc_label: "标题"
toc_icon: "heart"  # Font Awesome对应图标名称 (无fa前缀)	
---
今年双十一正好要去长春办事，所以决定放个短假，在长春玩一玩，正好看看双十一，实体店有没有什么活动，去红旗街万达买点东西。

## 吃早餐
早晨到了之后八点多吃了个早餐，烧卖+包子。吃过之后还没有饱，又去路边买了一份手抓饼。两份早餐吃过后，真的是很撑了。于是决定直接走着去万达，路程也不远。

<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta name="keywords" content="百度地图,百度地图API，百度地图自定义工具，百度地图所见即所得工具" />
    <meta name="description" content="百度地图API自定义地图，帮助用户在可视化操作下生成百度地图" />
    <title>百度地图API自定义地图</title>
    <!--引用百度地图API-->
    <script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=gNYMYXtagjUSVdAsfhsVS05dvZ7u5djs"></script>
  </head>
  
  <body>
    <!--百度地图容器-->
    <div style="width:600px;height:450px;border:#ccc solid 1px;font-size:12px" id="map"></div>
    <p style="color:red;font-weight:600">
      <a href="http://developer.baidu.com/map/index.php?title=jspopular/guide/introduction" style="color:#2f83c7" target="_blank"></a>
      <a href="http://lbsyun.baidu.com/apiconsole/key?application=key" style="color:#2f83c7" target="_blank"></a>
    </p>
  </body>
  <script type="text/javascript">
    //创建和初始化地图函数：
    function initMap(){
      createMap();//创建地图
      setMapEvent();//设置地图事件
      addMapControl();//向地图添加控件
      addMapOverlay();//向地图添加覆盖物
    }
    function createMap(){ 
      map = new BMap.Map("map"); 
      map.centerAndZoom(new BMap.Point(125.37551,43.852913),12);
    }
    function setMapEvent(){
      map.enableScrollWheelZoom();
      map.enableKeyboard();
      map.enableDragging();
      map.enableDoubleClickZoom()
    }
    function addClickHandler(target,window){
      target.addEventListener("click",function(){
        target.openInfoWindow(window);
      });
    }
    function addMapOverlay(){
      var markers = [
        {content:"我的备注",title:"红旗街万达",imageOffset: {width:0,height:3},position:{lat:43.873842,lng:125.303071}}
      ];
      for(var index = 0; index < markers.length; index++ ){
        var point = new BMap.Point(markers[index].position.lng,markers[index].position.lat);
        var marker = new BMap.Marker(point,{icon:new BMap.Icon("http://api.map.baidu.com/lbsapi/createmap/images/icon.png",new BMap.Size(20,25),{
          imageOffset: new BMap.Size(markers[index].imageOffset.width,markers[index].imageOffset.height)
        })});
        var label = new BMap.Label(markers[index].title,{offset: new BMap.Size(25,5)});
        var opts = {
          width: 200,
          title: markers[index].title,
          enableMessage: false
        };
        var infoWindow = new BMap.InfoWindow(markers[index].content,opts);
        marker.setLabel(label);
        addClickHandler(marker,infoWindow);
        map.addOverlay(marker);
      };
    }
    //向地图添加控件
    function addMapControl(){
      var scaleControl = new BMap.ScaleControl({anchor:BMAP_ANCHOR_BOTTOM_LEFT});
      scaleControl.setUnit(BMAP_UNIT_IMPERIAL);
      map.addControl(scaleControl);
      var navControl = new BMap.NavigationControl({anchor:BMAP_ANCHOR_TOP_LEFT,type:BMAP_NAVIGATION_CONTROL_LARGE});
      map.addControl(navControl);
      var overviewControl = new BMap.OverviewMapControl({anchor:BMAP_ANCHOR_BOTTOM_RIGHT,isOpen:true});
      map.addControl(overviewControl);
    }
    var map;
      initMap();
  </script>
</html>

## 坐电车
到了红旗街站点之后，刚好路过一个[有轨电车](https://baike.baidu.com/item/%E6%9C%89%E8%BD%A8%E7%94%B5%E8%BD%A6/2317603?fr=aladdin)车站。想着之前没坐过电车，这次刚好感受一下。     
电车大概坐了七八站，决定坐返程回万达，在回去的路上，在车厢尾部站着，透过车窗向外看，瞬间感觉到秋意很浓。

# 逛万达
回到万达之后就去了小米之家，准备看看小米电视。之前准备下手买小米电视4X-50寸的，但是店里没货。所以就没买，但是这次来没空手而归，买了两盒中性笔，一元一支很划算。    
出了小米之家继续闲逛，发现旁边有一家衣服店[NOME](http://www.nome.com/)。进去逛了一圈，发现衣服卖的真的很便宜，于是立刻就试了两件。最后自己选了一件黄色针织衫、给妹妹买了2件卫衣，一共花了200多。

# 吃午饭
买完衣服出来后就已经11：30分了。因为下午赶着办事，所以匆忙的去了饭店，还是上次去的火锅鸡，只不过这次提前预定了位置。饭店就在万达西南侧，出门大概200米就到了。上菜很快，这次点的是酱香火锅鸡。因为上次点的微辣，结果很辣，吃过之后胃不舒服，所以决定这次吃不辣的。    
![Snipaste_2019-11-18_21-06-22.png](https://i.loli.net/2019/11/18/hb5KaBZqToeMlf8.png)
但是吃过之后立刻就感觉，没有上次点的微辣火锅鸡香。两个人每次来吃火锅鸡，都是吃一半剩一半，太浪费了，下次换一家饭店尝尝。

# 回家
午饭过后，匆忙办完事就奔向火车站了。下午三点半的火车，上车之后发现车上人很少，找了一个车厢就休息了。手机只剩下35%电量，所以只能睡觉、发呆。坐火车，手机没电真的很无聊。本来准备好的电视剧也没办法看了。

# 到家
将近半夜，火车到家了，打个车到家，顺便把小米电视买了下来。睡觉 :sleeping: