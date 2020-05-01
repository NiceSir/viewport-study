# viewport(移动端适配)

## 相关概念

* 分辨率：屏幕的像素点数
* 屏幕尺寸： 屏幕对角线长度
* 设备像素（物理像素）：屏幕有多少个发光的点
* css像素：逻辑像素
* 设备像素密度(ppi/dpi) = 设备对角线的像素 / 屏幕尺寸
* 设备像素比（dpr） = 设备像素（分辨率）/ 逻辑像素（设备独立像素）

## 视口

* 视觉视口（visual viewport）：手机等设备的屏幕可视区域

        window.innerWidth/innerHeight

* 布局视口：文档实际的区域

        document.documentElement.clientWidth/clientHeight

* 理想视口：通常情况下为视觉视口

        screen.width/height 

## meta控制布局视口


        <meta name='viewport' content=''>
        //　　content中的属性
        width:设置布局视口的宽度为特定的值(device-width)
　　    initial-scale:设置页面的初始缩放程度和布局视口的宽度
　　    minimum-scale:设置了最小缩放程度(用户可缩小的程度)
　　    maximum-scale:设置了最大缩放程度(用户可放大的程度)
　　    user-scalable:是否阻止用户进行缩放,默认yes

## 常见适配方案

* 百分比+固定高度
    
    * 固定屏幕为理想视口宽度
    * 水平百分比布局
    * 可设置怪异盒模型(box-sizing:border-box;)

* rem适配

    * rem：根元素一个字体的大小（em：当前元素字体大小）




