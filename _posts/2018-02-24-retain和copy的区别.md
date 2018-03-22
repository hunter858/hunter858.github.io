
---
layout: post
title: retain 和copy的区别
date: 2018-02-24
categories: blog
tags:ios
description: 
---


retain 和copy的区别

在ios开发中我们一般都这么定义：

```
@property (nonatomic,copy) NSString *name，而不这么定义：

@property (nonatomic,retain) NSString *name，两者的差别就在一个使
```
用copy，一个使用retain。 
一直以来都不明白为什么，今天通过查阅资料总算弄明白了，所以记录一下。 
在说明白retain和copy的区别，首先需要明白深复制和浅复制的概念。 
1 深复制：内容拷贝,源对象和副本对象指的是两个不同的对象,源对象引用计数器不变,副本对象引用计数器为1 
2 浅复制：指针拷贝,源对象和副本对象指的都是同一个对象,对象引用计数器+1,相当于retain

只有不可变对象创建不可变副本(copy)才是浅复制，其它的都是深复制 
上面的结论至关重要，大家可以对NSString和NSMutableString分别测试，在此不再赘述。 
下面通过实验来说明copy和retain的区别。

```
@interface ViewController ()
@property (nonatomic,copy) NSString *name;
@property (nonatomic,retain) NSString *name2;
@end


-(void)test{
    NSString *str = @"fffff";
    self.name = str;
    self.name2 = str;
    NSLog(@"   str:  %p",str);
    NSLog(@"  copy:  %p",self.name);
    NSLog(@"retain:  %p",self.name2);

}
-(void)test2{
    NSMutableString *str = [NSMutableString stringWithString:@"ffffff"];
    self.name = str;
    self.name2 = str;
    NSLog(@"   strM:  %p",str);
    NSLog(@"   copy:  %p",self.name);
    NSLog(@"retaini:  %p",self.name2);
}
```
先执行test，再执行test2，两次执行的结果如下：



![20151209193606057.png](http://upload-images.jianshu.io/upload_images/1716313-8e61e0fab2005147.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![20151209193635805.png](http://upload-images.jianshu.io/upload_images/1716313-c14c024400679086.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


所以得出结论： 

（1）copy是创建一个新对象，两个对象内容相同，旧对象没有变化。新的对象retain为1，与旧有对象的引用计数不变。旧对象发生改变不影响新对象，copy减少对象对上下文的依赖。 

（2）retain属性表示两个对象地址相同（建立一个指针，指针拷贝），内容相同，这个对象的retain值+1。两个对象要改变就一起改变。 

（3）如果把一个对象赋值给另一个对象（如上面把str赋值给name或name2），如果该对象是不可变的，那么另一个对象是copy或者retain都可以，没区别；把一个对象赋值给另一个对象，如果该对象是可变的，并且希望另一个对象随着该对象变化而变化，则可以把另一个对象设置为retain（如上面把str赋值给name2）；如果希望另一个对象不随着该对象变化而变化，则可以把另一个对象设置为copy（如上面把str赋值给name）