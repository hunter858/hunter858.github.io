
---
layout: post
title: React-Native 之调试指南 （七）
date: 2018-01-30
categories: blog
tags:ios, react-native
description: 
---


React-Native 之调试指南 （七）


在模拟器上开启Developer Menu
Android模拟器：
可以通过 `Command⌘ + M` 快捷键来快速打开 Developer Menu。也可以通过模拟器上的菜单键来打开。

心得：高版本的模拟器通常没有菜单键的，不过Nexus S上是有菜单键的，如果想使用菜单键，可以创建一个Nexus S的模拟器。

iOS模拟器：
可以通过`Command⌘ + D `快捷键来快速打开 Developer Menu。





###Chrome开发者工具

![QQ20180126-120512.png](http://upload-images.jianshu.io/upload_images/1716313-ee62c2f8fefdf82e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


在Chrome上调试js代码，需要在开发菜单中选择 `Debug JS Remotely`，这会打开一个新的`http://localhost:8081/debugger-uitab`页。

在Chrome中，按下⌘ + option + i或者选择视图(View) -> 开发者(Developer) -> 开发工具(Developer Tools)来打开开发工具控制台。打开有异常时暂停（Pause On Caught Exceptions）选项，能够获得更好的开发体验。

译注：Chrome 中并不能直接看到App的用户界面，而只能提供`console `的输出，以及在`sources `项中断点调试js脚本。

![image](http://upload-images.jianshu.io/upload_images/1716313-6de0e4fab6eed1b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


###在真机上调试：

在iOS上 —— 打开 RCTWebSocketExecutor.m文件，将其中的 `localhost ` 替换为你电脑的ip地址。然后晃动设备打开开发菜单，即可开始调试。
对于Android设备 —— 如果你通过usb连接了一个Android 5.0或更高版本的设备，则可以通过adb命令建立一个从设备向电脑转发的端口：`adb reverse tcp:8081 tcp:8081` (点击这里查看adb命令的帮助)。或者，你可以通过摇晃打开开发者菜单，选择`Dev Settings`，然后在 `Debug server host for device` 中设置你电脑的ip地址:端口号。




