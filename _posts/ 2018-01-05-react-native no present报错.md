
---
layout: post
title: react-native no present报错
date: 2018-01-05 react-native no present报错
categories: blog
tags: react-native,ios
description: 
---

![react-native](http://upload-images.jianshu.io/upload_images/1716313-806a3ba1d40d9d85.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

react-native 已经出来很久了，我确一直没有上手
当我最近开始吃鸡的时候，发现了一个让我很头疼的报错，简直丧心病狂；
对的，就是这报错；

```
No bundle URL present

Make sure you’re running a packager server or have included a .jsbundle file in your application bundle
```

>报错截图


![F3E62935E40B9C298C56EC82FC2A0E54.jpg](http://upload-images.jianshu.io/upload_images/1716313-c514ff3b6aa86b3b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



第一步：安装react-native 中文网的教程，把该装的插件都安装了
第二步：初始化项目 ，然后再终端执行命令 react-native run-ios
第三部：然后傻逼了




解决方法

[react-native 中文网 传送门](https://reactnative.cn/docs/0.51/native-modules-android.html#content)

[react-native 英文网 传送门](https://facebook.github.io/react-native/docs/tutorial.html)



###解决方法

尝试了N 多解决方法

* ***方法1:*** 把代理设置成全局模式 [这位小哥的参考链接](http://blog.csdn.net/suyie007/article/details/70768410)，然而并没有解决问题！！！

* ***方法2:*** 删除项目文件夹下的build 文件夹，再重新执行 react-native run-ios [另一位位小哥的参考链接](http://blog.csdn.net/yanzisu_congcong/article/details/78531601)，然后也没有用！！！

* ***方法3:*** 行吧，阿西吧；翻墙找 [stackoverflow.com](https://stackoverflow.com),终于让我尝试成功了
成功链接：[感谢歪果仁小伙伴-还是你们给力-成功链接](https://stackoverflow.com/questions/42610070/what-means-of-no-bundle-url-present-in-react-native/45267703#45267703)




>真正解决问题的方法
>其实还是很久之前我改了host 文件，然后127:0.0.1 被我换成别的域名了
>然后我把host 的本地环回地址改回去了，也就是127.0.0.1 换回去了，就好了；host 
>配置如下


![QQ20180105-133920.png](http://upload-images.jianshu.io/upload_images/1716313-09681b8ab4122e62.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



[https://stackoverflow.com/questions/42610070/what-means-of-no-bundle-url-present-in-react-native/45267703#45267703](https://stackoverflow.com/questions/42610070/what-means-of-no-bundle-url-present-in-react-native/45267703#45267703)

