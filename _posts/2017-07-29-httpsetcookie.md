---
layout: post
title: NSUrlrequest 请求加cookie
date: 2017-07-29
categories: blog
tags: cookie
description: 
---

最近项目中碰到的需求是，在hybird 开发中，给H5 的请求加点cookie
怎么调试，怎么塞，怎么验证呢；


这次我们拿 [https://www.baidu.com]() 来做实验，插入我自己的名字 拼音 [pengchao]()  和  [this is my cookie]() ;

实验结果如图：
![](http://opevtrwe5.bkt.clouddn.com/WX20170801-215657@2xstep6.png)

第一步，允许你的iphone 或者 ios simluator 允许开发者调试，怎么做呢；
iphone -> 设置 -> Safari -> 高级 - >javaScript 和 web检查器 勾选；
![](http://opevtrwe5.bkt.clouddn.com/WX20170801-213325@2xstep1.png)
![](http://opevtrwe5.bkt.clouddn.com/WX20170801-213354@2xstep2.png)
![](http://opevtrwe5.bkt.clouddn.com/WX20170801-213439@2xstep3.png)

第二步，找到mac 的Safari 浏览器，打开偏好设置，找到最下方的，在菜单栏中显示"开发"菜单;

![](http://opevtrwe5.bkt.clouddn.com/WX20170801-215130@2xstep4.png)
![](http://opevtrwe5.bkt.clouddn.com/WX20170801-215425@2xstep5.png)

第三步，运行代码，在safari 的开发中，找到 正在调试的 iphone  或者 simluator
,找到对应的那个 请求的域名，或者详细链接，

![](http://opevtrwe5.bkt.clouddn.com/WX20170801-213508@2xstep5-1.png)
![](http://opevtrwe5.bkt.clouddn.com/WX20170801-215425@2xstep5.png)

放代码 

	- (void)viewDidLoad {
	    [super viewDidLoad];
	    // Do any additional setup after loading the view, typically from a nib.
	    
	    NSString *urlStr = @"https://www.baidu.com";
	    NSURL *url =[NSURL URLWithString:urlStr];
	    NSURLRequest *request = [NSURLRequest requestWithURL:url];
	    
	    NSHTTPCookie *cookie = [self setName:@"pengchao" value:@"this is my  cookie"];
	    [[NSHTTPCookieStorage sharedHTTPCookieStorage] setCookie:cookie];
	    [self.webView loadRequest:request];
	}


### 另一个方法

	-(NSHTTPCookie *)setName:(NSString *)CookieName value:(NSString *)CookieValue{
	    
	    NSMutableDictionary *cookieProperties = [NSMutableDictionary dictionary];
	    [cookieProperties setObject:CookieName forKey:NSHTTPCookieName];
	    //设置cookie 的name
	    [cookieProperties setObject:CookieValue forKey:NSHTTPCookieValue];
	    //设置cookie 的name 对应的value 值
	    [cookieProperties setObject:@".baidu.com" forKey:NSHTTPCookieDomain];
	    //设置cookie 的域
	    [cookieProperties setObject:@".baidu.com" forKey:NSHTTPCookieOriginURL];
	    //
	    [cookieProperties setObject:@"/" forKey:NSHTTPCookiePath];
	    //设置cookie在哪个路径下
	    [cookieProperties setObject:@"0" forKey:NSHTTPCookieVersion];
	    //设置cookie的版本
	    [cookieProperties setObject:[NSDate dateWithTimeIntervalSinceNow:60*60*24] forKey:NSHTTPCookieExpires];
	    //设置失效时间
	    [cookieProperties setObject:@"0" forKey:NSHTTPCookieDiscard];
	    //设置sessionOnly
	    
	    NSHTTPCookie *cookie = [NSHTTPCookie cookieWithProperties:cookieProperties];
	    return cookie;
	}
 
 代码，我就不解释啦，所有代码都在这，如果用户需要缓冲到本地，可以用 `NSUserDefaults`
 
 成功塞入: 妈妈再也不用担心我给H5 塞cookie 出问题了
 ![](http://opevtrwe5.bkt.clouddn.com/WX20170801-215657@2xstep6.png)
