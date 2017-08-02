---
layout: post
title: xcode 断点小技巧
date: 2017-08-02
categories: blog
tags: xcode
description: 
---
在你新接手了一个项目的时候，你一定是是从项目的 AppDelegate 看起，
一行行，或者一个Control 一个 Control 的看起，直到整个项目都熟悉；
下面我教你一个查找 Control 的小技巧；

1.新建一个breakPoint 断点的需求

![](http://ooynqqqkg.bkt.clouddn.com/888EFC17-7642-4C8C-868D-34D47994200D.png)

2.在断点处写入 -[UIViewController viewDidLoad] 
代表什么意思呢，代表xcode 断点所有的 UIViewController 的 viewDidLoad  方法；
这样你只需也在启动项目的的时候，就能找到 ，现在程序到了那个控制器的 viewDidLoad方法；
![](http://ooynqqqkg.bkt.clouddn.com/QQ20170703-181807@2x.png)

3.如图所示，是不是就找到了现在启动到了哪个控制器，你只需点点点 ，就能找到显示的是哪个Control；
![](http://ooynqqqkg.bkt.clouddn.com/QQ20170703-182357@2x.png)


技能2
断点异常代码，定位bug，我猜很多同学刚学习OC 的时候，都是通过console，去找bug，要想充分利用你的xcode，你可以这样用；

1.比如我现在project 中有一个bug，我不用看console 也能定位到出问题的代码段；

2.新建 Exception breakpoint 如图所示；
![](http://ooynqqqkg.bkt.clouddn.com/QQ20170703-182503@2x.png)
新建成功
![](http://ooynqqqkg.bkt.clouddn.com/QQ20170703-182850@2x.png)

3.查看异常抛出点，如图所示，是不是很轻松，😄
![](http://ooynqqqkg.bkt.clouddn.com/481466D6-70C8-4AF3-95CD-0BC2EC8A5749.png)



同理，可以推测，

例如找到 
	[self.navigationController setNavigationBarHidden:YES animated:YES];

![](http://ooynqqqkg.bkt.clouddn.com/QQ20170703-184651@2x.png)
截图效果如下：
![](http://ooynqqqkg.bkt.clouddn.com/QQ20170703-184915@2x.png)
如图，确实如此；
![](http://ooynqqqkg.bkt.clouddn.com/QQ20170703-184943@2x.png)
那么是不可以断点到 的push 方法 或者pop 方法；找到跳转的地方；或者一些类方法，欢迎大家积极尝试；



欢迎查看我的[github](https://github.com/hunter858)和我的[个人博客](http://www.pengchao.tech)，正在一步步优化和完善，谢谢大家🙏 😄；
