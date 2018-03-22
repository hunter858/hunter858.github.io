---
layout: post
title: 使用objective-c和javaScript做简单的网络爬虫
date: 2017-1-02
categories: blog
tags: 
description: 
---


 前几天，一位做健康类SEO优化的朋友叫我把网页上的文字和链接搞下来，所以就抱着试试的心态去搞搞，反正试了又不会怀孕。首先做这各你首先得要知道什么是DOM和懂一些javascript，关于这方面的教程就不在这里介绍了。可以看这里[廖雪峰javascript]()教程 和[W3CSchool]()。

   好了，我要爬得链接为：百度搜素的关键字:“健康减肥”。我要拿到的是搜索的结果的文字和点击的超链接地址（需求为前5000条数据），如图所示:

![](http://opevtrwe5.bkt.clouddn.com/042120459072499.png.jpeg)

 接下来，使用Firefox的插件firebug调试工具来查看网页的源代码，经仔细观察(次步骤一定要耐心自信^_^,否则没法往下做)，发现搜索的结果均在这个节点里里面<div id="content_left">，如图所示：
        
![](http://opevtrwe5.bkt.clouddn.com/042127221816004-1.png.jpeg)
	
![](http://opevtrwe5.bkt.clouddn.com/Unknown.png)
	
好了，知道了自己需要查找的内容在哪，接下来就用用js代码来筛选我们需要的内容了。首先我们把刚刚的那个网页下载下来，保存到本地，然后在body(一定要保证在</body>添加)的最后添加如下代码。`<script src="script.js"></script>`
如图：

![](http://opevtrwe5.bkt.clouddn.com/dd)


下一步，新建一个一个与这个html同一目录下的js文件script.js,添加如下代码

  
复制代码
	var leftContent = document.getElementById('content_left');//获取id为content_left标签
		
	var results = leftContent.getElementsByTagName('h3');//经观察，所有的链接都放在h3标签中
		
	var string = "";
		
	for (var i = 0; i < results.length; i++) {
	    
	var node = results[i];
	var nodeA = node.getElementsByTagName('a')[0];//没啥的，观察出来的规律
	    
	string += nodeA.innerHTML + "这是一个字符串分割标识" +nodeA.href + "<br>" + "<br>" + "<br>" ;
	//"这是一个字符串分割标识"和"<br><br><br>"是分割标识字符串,稍后在oc代码中阐述
	};


	document.body.innerHTML = "";//清空原来的内容
	
	document.body.innerHTML = string;//添加新内容

  
复制代码
 

很好，接下来，打开刚刚保存的html文件，是不是网页内容变了，变了就对了。下一步的任务，就是把这些内容写到xml文件或者新德html文件里面。

重头戏准备来了，接下新建一个Xcode的singleViewApplication程序，在Main.storyboard拖一个UIWebView，并让控制器引用它，并把刚刚写好的script.js文件添加到工程中，如图所示:
   
  
	<script src="script.js"></script>
  
 

在ViewController.m添加如下代码，

复制代码
  

	#import "ViewController.h"
	#import "BaiduModel.h"
	
	@interface ViewController ()<UIWebViewDelegate> {
	    int _page;
	    NSString *_path;
	    NSMutableArray *_totalArray;
	    NSTimer *_timer;
	    
	}
	@property (weak, nonatomic) IBOutlet UIWebView *webView;
	@end
	
	@implementation ViewController
	
	- (void)viewDidLoad {
	    [super viewDidLoad];
	    
	    _page = 0;
	    
	    _totalArray = [NSMutableArray array];
	    
	   NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:5.0 target:self selector:@selector(runTimeAction) userInfo:nil repeats:YES];
	    _timer = timer;//至于这里为什么使用定时器加载，因为我发现不用定时器，加载过快会被百度服务器屏蔽
	}
	
	//加载链接
	- (void)loadRequest {
	    [self.webView loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:_path]]];
	}
	
	#pragma mark - 网页加载完毕回调方法，这个时候执行js脚本和保存数据
	- (void)webViewDidFinishLoad:(UIWebView *)webView {
	    
	    NSString *scriptPath = [[NSBundle mainBundle] pathForResource:@"script" ofType:@"js"];
	    NSString *script = [NSString stringWithContentsOfFile:scriptPath encoding:NSUTF8StringEncoding error:nil];
	    
	   NSString *letfContent = [webView stringByEvaluatingJavaScriptFromString:script];
	    //返回为id=runTimeAction元素的字符串
	    
	    if (letfContent.length) {
	       [self convertToModels:letfContent];//转成模型并且保存到_totalArray中
	    }
	}
	
	#pragma mark转成模型并且保存到_totalArray中
	- (void )convertToModels:(NSString *)str {
	    //<br><br><br>和“这是一个字符串分割标识”可以script脚本里面找到,作为分隔字符串的标识
	    NSArray *modelStrArr = [str componentsSeparatedByString:@"<br><br><br>"];
	    
	    for (NSString *modelStr in modelStrArr) {
	        
	       NSArray *theModelStr = [modelStr componentsSeparatedByString:@"这是一个字符串分割标识"];
	        
	        BaiduModel *baidu = [[BaiduModel alloc] init];
	        baidu.title = theModelStr.firstObject;
	        baidu.url = theModelStr.lastObject;
	        
	        [_totalArray addObject:baidu];//添加到大数组中
	    }
	}
	
	- (void)runTimeAction {
	    
	    NSString *keyWord = @"%E5%81%A5%E5%BA%B7%E5%87%8F%E8%82%A5";//"健康减肥"关键字为加了百分号编码后的字符串
	    NSString *oq = @"%E5%81%A5%E5%BA%B7%E5%87%8F%E8%82%A5";
	    NSString *rsv_t = @"4c24%2BJ96BhSoWjwj4WADhDN6Po%2FOIC5AqnhkmmjfltO5TbZ8YmjxqZjZxrsw7ILy9sBo";
	    
	    NSString *path = [NSString stringWithFormat:@"https://www.baidu.com/s?wd=%@&pn=%d&oq=%@&tn=baiduhome_pg&ie=utf-8&usm=3&rsv_idx=2&rsv_pq=d0bafbb000053f45&rsv_t=%@",keyWord,_page,oq,rsv_t];
	    /*
	     *其中参数wd为搜索关键字,pn为分页参数，其他有几个参数不知道什么鬼意思,反正不管它就是了,别动它就是，否则他会适应手机屏幕而得不到合适的结果
	     */
	    _path = path;
	    _page += 10;
	
	    [self loadRequest];
	  
	    if (_totalArray.count>5000) {//只爬5000条左右数据
	        [_timer invalidate];
	        //归档
	        [self writeToFile];
	        
	        NSLog(@"归档完成！！！！！！！！！！！！！！！！！！！");
	    }
	}
	
	- (void)writeToFile {
	    
	    NSMutableArray *arrM = [NSMutableArray array];
	    
	    for (BaiduModel *baidu in _totalArray) {
	    
	        NSMutableDictionary *dict = [NSMutableDictionary dictionary];
	        [dict setObject:baidu.title forKey:@"title"];
	        [dict setObject:baidu.url forKey:@"url"];
	        [arrM addObject:dict];
	    }
	    [arrM writeToFile:@"/Users/liwenshen/Desktop/today/reptile.plist" atomically:YES];
	}
	
	@end

  
复制代码

当然你也可以生成html字符串，拷贝到html文件中，代码如下:

复制代码

	- (void)generateHtml {
    
    NSString *htmlHeader = @"<!DOCTYPE html><html><head><meta charset=\"utf-8\"></meta></head><body>";
    NSString *htmlFooter = @"</body></html>";
    
    NSMutableString *strM = [NSMutableString stringWithString:htmlHeader];
    
    for (BaiduModel *b in _totalArray) {
        
       NSString *a = [NSString stringWithFormat:@"<a href=\"%@\">%@</a><br>",b.url,b.title];
        
        [strM appendString:a];
        
    }
    [strM appendString:htmlFooter];
    
    NSLog(@"%@",strM);
	}
复制代码
 

好了，终于写完了，有不懂的可以给我留言，当然做爬虫最好的是选用java，Python等语言，有很多对应的库,同时，你也可以保存到数据库中。学会这个，你可以去交友网站，把所有的妹子都爬下来，嘻嘻。接下来，欣赏一下爬虫出来的结果:

![](http://opevtrwe5.bkt.clouddn.com/Unknown-1.png)

![](http://opevtrwe5.bkt.clouddn.com/Unknown-2.png)



