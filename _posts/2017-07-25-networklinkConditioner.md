---
layout: post
title: ios开发模拟网路较差的环境
date: 2017-08-02
categories: blog
tags: ios
description: 
---





在日常的开发中，有时候我们需要模拟网络不太好的情况
xcode 给我们提供了这样一个工具，废话不多说，就是它，如图

下载链接 [https://download.developer.apple.com/Developer_Tools/Hardware_IO_Tools_for_Xcode_7.3](https://download.developer.apple.com/Developer_Tools/Hardware_IO_Tools_for_Xcode_7.3/Hardware_IO_Tools_for_Xcode_7.3.dmg)

1. 打开Xcode ,Open Developer Tool ->More Developer Tool 打开官方下载链接 
![](http://ooynqqqkg.bkt.clouddn.com/WX20170726-212539@2x.png)

2. 进入下载链接，搜索关键字 [Hardware IO Tools for Xcode]() 下载第一个就行了；
![](http://ooynqqqkg.bkt.clouddn.com/WX20170726-212340@2x.png)

3. 安装下载好的 [dmg]() 文件， 安装里面的这个，在系统偏好设置里面找到；
![](http://ooynqqqkg.bkt.clouddn.com/WX20170726-212138@2x.png)


4. 安装成功 对啦，就是这个啦；
![](http://ooynqqqkg.bkt.clouddn.com/WX20170726-212607@2x.png)

6. 新建一个 [custome]() 自定义网络样式，调整里面的参数，即可设置一个较差的网络环境
![](http://ooynqqqkg.bkt.clouddn.com/WX20170726-212910@2x.png)
![](http://ooynqqqkg.bkt.clouddn.com/WX20170726-213135@2x.png)


7. 打开 `on `开关 效果图如下
![](http://ooynqqqkg.bkt.clouddn.com/2017-07-26%2022_00_14.gif)

8. 温馨提示，用完记得把它关掉，不然你mac上网也会超慢😊
插播个广告，访淘宝首页 []()


