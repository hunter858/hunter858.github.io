---
layout: post
title: QQBugly
date: 2017-08-02
categories: blog
tags: QQBugly
description: 
---

### 真的如厂商所说，好用的线上bug集成工具；

![](http://ooynqqqkg.bkt.clouddn.com/WX20170801-222144@2xstep2.png)

在我们线上app 中，我们的电商项目集成了[QQBugly]() ，但是我们没有勾选自动上传 [DYSM]() 符号表，所以我们要手动上传 ；

算是给腾讯Bugly 打个广告吧,[腾讯Bugly官网地址](https://bugly.qq.com/v2/)，需要的开发们，自行研究一下，或者听我给你讲一讲；

[官方集成文档地址(ios) ](https://bugly.qq.com/docs/user-guide/instruction-manual-ios/?v=20170627170213)

集成教程我就不说了，文档很详细，为啥要写这篇博客呢，为了记录帮助自己理解和消化；


#### 什么是符号表？
符号表是内存地址与函数名、文件名、行号的映射表。符号表元素如下所示：

<起始地址> <结束地址> <函数> [<文件名:行号>]
![](http://ooynqqqkg.bkt.clouddn.com/4001.png)

说直白点，就是利用符号表，帮你找到出错的代码；
哇：这么神奇，对，就是这么神奇；
我们用的是第二种方式 `提取dSYM文件的符号表文件并上传`

[官方给的工具链接](https://bugly.qq.com/v2/sdk?id=37f16cf0-2020-4e30-9e8d-0f7de59cfe94) 集成文档内有，我教你如何用就好；

#### 1. 下载官方工具，放到了一个文件夹;
#### 2. 找到线上 ipa 的 [dSYM]()；
>打开 xcode 的 `Window ` 的选项中的 `Organizer` 找到上次打包生成的 文件；如图

![](http://ooynqqqkg.bkt.clouddn.com/WX20170801-223755@2xstep3.png)
![](http://ooynqqqkg.bkt.clouddn.com/WX20170801-223959@2xstep5.png)
![](http://ooynqqqkg.bkt.clouddn.com/WX20170801-223859@2xstep4.png)

>如果你告诉我，你删了，或者找不到 dSYM 文件，小编只能告诉我，我也很无奈，下次记得备份每个版本的 dSYM ，不然就用 第一种方式上传 [dSYM]() 吧，省去很多麻烦；
##### 3. 打开 终端工具 键入命令：
    java -jar /Users/pengchao/Desktop/buglySymboliOS2/buglySymboliOS.jar -i /Users/pengchao/Desktop/test/SpringTour.app.dSYM -o 0801.zip

> 实用命令  第一个 [[ ]]() 表示 buglySymboliOS.jar 的路径，第二个 [[ ]]() 表示dSYM的路径，第三个 [[ ]]() 表示生成的zip 的名称；
    java -jar [buglySymboliOS.jar路径] -i [xxx.app.dSYM的路径] -o [xxx.zip] 
	
>例如：
    java -jar /Users/pengchao/Desktop/buglySymboliOS2/buglySymboliOS.jar -i /Users/pengchao/Desktop/test/SpringTour.app.dSYM -o 0801.zip
	
![](http://ooynqqqkg.bkt.clouddn.com/WX20170801-225609@2xstep6.png)


>生成zip 成功，在finder 搜索 [0801.zip]() ，然后到腾讯Bugly 的官网，找到那个发生闪退的bug ；


#### 4. 上传 zip 符号表
![](http://ooynqqqkg.bkt.clouddn.com/WX20170801-230312@2xstep8.png)

>在没有上传符号表之前，我们是看不懂的；截图如下；

![](http://ooynqqqkg.bkt.clouddn.com/WX20170801-230332@2xstep7.png)
>上传成功；我们看到了，截图告诉我们，哪个控制器的，哪个 ViewMode 出错，在哪 一行，都清晰可见，现在我们就去看代码，找代码，复现bug。(最好是找到出错设备的那个软件版本，最好的机型相同);

![](http://ooynqqqkg.bkt.clouddn.com/WX20170801-225934@2xstep9.png)



##### 5. 通过 提示信息 找错误代码；

>根据提示一步步的找到了 `STHome2017ViewController viewDidLoad` 方法
`[STHome2017ViewModel startNetWork]` 里面的 `[STHome2017ViewModel topBannerDataBatch:failure:]` 方法发生了闪退；

>但是由于我找了台iphone 7 软件版本也是出bug的那个，不幸没能复现bug ，这就很尴尬了；

>后来我仔细看了代码，发现可能是，我这个 `NSDictionary` 可能有了一个 `null ` 的值，才导致的闪退了，我写了一段模拟代码，果不其然发生了闪退现象，所以我加了个安全保护；
下面展示一下我的 错误代码；

##### 6. 修改前的代码

    self.topBannerOperation=[manager GETAndShowExceptionIfErr:JavaCMSHomeQueryContent parameters:@{@"cityId":([STConfig GetInstance].localCity.CityId),@"positionId":NullNumber([OnlineConfigurationManager sharedManager].localConfigurationmodel.landingPage.home.topCarousel.positionId)} success:^(AFHTTPRequestOperation *operation, id responseObject, id Response) {
        
        if (responseObject[@"data"]!=nil&&[responseObject[@"data"] isKindOfClass:[NSDictionary class]]) {
            weakself.topBannerModel=[[Home2017CMSModel alloc]initWithDictionary:responseObject[@"data"] error:nil];
        }
        
        dispatch_group_leave(weakself.group);
        
    } failure:^(AFHTTPRequestOperation *operation, NSError *error) {
        
        dispatch_group_leave(weakself.group);
        

##### 修改后的代码 （加了个 NullString 用来返回一个非null 的字符串）

	self.topBannerOperation=[manager GETAndShowExceptionIfErr:JavaCMSHomeQueryContent parameters:@{@"cityId":NullString([STConfig GetInstance].localCity.CityId),@"positionId":NullNumber([OnlineConfigurationManager sharedManager].localConfigurationmodel.landingPage.home.topCarousel.positionId)} success:^(AFHTTPRequestOperation *operation, id responseObject, id Response) {
	    
	    if (responseObject[@"data"]!=nil&&[responseObject[@"data"] isKindOfClass:[NSDictionary class]]) {
	        weakself.topBannerModel=[[Home2017CMSModel alloc]initWithDictionary:responseObject[@"data"] error:nil];
	    }
	    
	    dispatch_group_leave(weakself.group);
	    
	} failure:^(AFHTTPRequestOperation *operation, NSError *error) {
	        
	dispatch_group_leave(weakself.group);
	        
提交修改，下个版本发布的时候，就不会出现闪退了，如果影响用户比较多，可以发临时更新；
谢谢你查看我的文章；如有不足可以指出，谢谢🙏；
