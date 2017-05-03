---
layout: post
title: CocoaPods简单使用
date: 2015-3-02
categories: blog
tags: [web,VUE]
description: 
---



### 1.为什么需要CocoaPods

在进行iOS开发的时候，总免不了使用第三方的开源库，比如SBJson、AFNetworking、Reachability等等。使用这些库的时候通常需要：

下载开源库的源代码并引入工程

向工程中添加开源库使用到的framework

解决开源库和开源库以及开源库和工程之间的依赖关系、检查重复添加的framework等问题

如果开源库有更新的时候，还需要将工程中使用的开源库删除，重新执行前面的三个步骤，顿时头都大了。。。

自从有了CocoaPods以后，这些繁杂的工作就不再需要我们亲力亲为了，只需要我们做好少量的配置工作，CocoaPods会为我们做好一切！

### 2.安装CocoaPods

#### 2.1 利用Alcatraz安装

在终端输入：

	curl -fsSL https://raw.github.com/supermarin/Alcatraz/master/Scripts/install.sh | sh
重启Xcode，在Xcode->Window->Package Manager,点击，如图：

![](/img/cocoapods/menu@2x.png)

使用Alcatraz
搜索到CocoaPods，点击左侧图标安装，如图：

![](/img/cocoapods/100552-0ddf42844c669b69.png)

安装CocoaPods
使用CocoaPods,如图：

![](/img/cocoapods/menu.png)
menu.png

使用CocoaPods
---
#### 2.2 一般性安装 
CocoaPods是用Ruby实现的，要想使用它首先需要有Ruby的环境。幸运的是OS X系统默认的已经可以运行Ruby了，因此我们只需要执行以下命令：

	$ sudo gem install cocoapods
CocoaPods是以Ruby gem包的形式被安装的。在安装执行的过程中，可能会问我们是不是更新rake，输入y即可。这是因为rake gem包会在安装的过程中检查更细，如果有可用的新版本就会出现刚才的选项。

在安装进程结束的时候，执行命令：

	$ pod setup


### I 安装过程中可能遇到的问题
执行完install命令半天没反应
这有可能是因为Ruby的默认源使用的是cocoapods.org，国内访问这个网址有时候会有问题，网上的一种解决方案是将远替换成淘宝的，替换方式如下：

	$ gem sources --remove https://rubygems.org/
	//等有反应之后再敲入以下命令
	$ gem sources -a https://ruby.taobao.org/
要想验证是否替换成功了，可以执行：

	$ gem sources -l
正常的输出是：

	*** CURRENT SOURCES ***
	
	https://ruby.taobao.org/
如图：

![](/img/cocoapods/100552-3f1629ada18307f4.png.jpeg)

> * 没有翻墙，这步应该是必须的，图中我一开始把参数"-l"打成了"-1"……
> * gem版本过老
> * gem是管理Ruby库和程序的标准包，如果它的版本过低也可能导致安装失败，解决方案自然是升级gem，执行下述命令即可：

	$ sudo gem update --system
如图，

![](/img/cocoapods/100552-956b7b767787843c.png.jpeg)


我这台新Mac没有升级过Ruby，所以失败了

最终成功
安装完成后，执行pod setup命令时报错：

	/Users/wangzz/.rvm/rubies/ruby-1.9.3-p448/lib/ruby/site_ruby/1.9.1/rubygems/dependency.rb:298:in `to_specs': Could not find 'cocoapods' (>= 0) among 6 total gem(s) (Gem::LoadError)
	from /Users/wangzz/.rvm/rubies/ruby-1.9.3-p448/lib/ruby/site_ruby/1.9.1/rubygems/dependency.rb:309:in `to_spec'
	from /Users/wangzz/.rvm/rubies/ruby-1.9.3-p448/lib/ruby/site_ruby/1.9.1/rubygems/core_ext/kernel_gem.rb:53:in `gem'
	from /Users/wangzz/.rvm/rubies/ruby-1.9.3-p448/bin/pod:22:in `<main>'
这就是路径设置的问题，可以通过执行：

	$ rvm use ruby-1.9.3-p448
（这个问题我没有遇到~）

### II 升级CocoaPods

升级很简单，再次执行安装命令即可：

	$ sudo gem install cocoapods
需要注意的是，如果安装的时候使用了sudo，升级的时候一样需要使用该关键字，不然升级完了以后又会出现路径不匹配问题。

---

### 3. 使用CocoaPods

用Alcatraz管理的，在上一节的截图中，已经展示怎么使用了，我们接下来描述一般性的，更有借鉴意义（当然，平常使用的时候，还是用Alcatraz的方式更简洁明了）。

为了演示这个过程，我创建了一个名为CocoaPodsTest的工程。

#### 3.1 创建Podfile

CocoaPods的一切都是从一个名为Podfile的文件开始的，我们需要先创建这个文件。个人习惯使用命令行，我会这样做：

	$ cd /Users/user_name/Desktop/CocoaPodsTest
	$ touch Podfile
首先进入到工程的根目录下，创建空白的Podfile文件，创建完毕的目录结构如下图：


![](/img/cocoapods/100552-d30591cfe6d9608c.png)

创建空白Podfile
（PS：Podfile文件也可以不放在工程的根目录下，只是会稍微麻烦点)

#### 3.2 编辑Podfile

根据需要，我们可以在Podfile文件中写入需要用到的第三方库，以SBJson、AFNetworking、Reachability三个库为例，我的Podfile内容如下：
	
	platform :ios
	pod 'Reachability',  '~> 3.0.0'
	pod 'SBJson', '~> 4.0.0'
	
	platform :ios, '7.0'
	pod 'AFNetworking', '~> 2.0'

#### 3.3 执行导入命令

准备工作都完成后，开始导入第三方库：

	$ cd /Users/wangzz/Desktop/CocoaPodsTest
	$ pod install
首先进入工程根目录，然后执行pod install命令，CocoaPods就开始为我们做下载源码、配置依赖关系、引入需要的framework等一些列工作，命令的执行结果打印出来如下：
	
	Analyzing dependencies
	Downloading dependencies
	Installing AFNetworking (2.1.0)
	Installing JSONKit (1.5pre)
	Installing Reachability (3.0.0)
	Generating Pods project
	Integrating client project
	
	[!] From now on use `CocoaPodsTest.xcworkspace`.
这就说明pod install命令执行成功了。再来看看工程根目录发生的变化，如下图：

![](/img/cocoapods/100552-784f41776c00d1e6.png)

成功
可以看到，工程的根目录下多了三个东西：CocoaPodsTest.xcworkspace、Podfile.lock文件和Pods目录。

再看看刚才执行完pod install命令打印出来的内容的最后一行：

	[!] From now on use `CocoaPodsTest.xcworkspace`.
提示我们从现在起，我们需要使用CocoaPodsTest.xcworkspace文件来开发。

#### 3.4 对于工程发生的变化，有几点需要说明：

第三方库会被编译成静态库供我们正真的工程使用

CocoaPods会将所有的第三方库以target的方式组成一个名为Pods的工程，该工程就放在刚才新生成的Pods目录下。整个第三方库工程会生成一个名称为libPods.a的静态库提供给我们自己的CocoaPodsTest工程使用。

我们的工程和第三方库所在的工程会由一个新生成的workspace管理

为了方便我们直观的管理工程和第三方库，CocoaPodsTest工程和Pods工程会被以workspace的形式组织和管理，也就是我们刚才看到的CocoaPodsTest.xcworkspace文件。

原来的工程设置已经被更改了，这时候我们直接打开原来的工程文件去编译就会报错，只能使用新生成的workspace来进行项目管理。

打开CocoaPodsTest.xcworkspace，界面如下：

![](/img/cocoapods/100552-784f41776c00d1e6.png)

依赖库设置
工程的目录结构还是非常明显的。

在项目中引用刚才添加的第三方库的头文件，执行编译操作，果断成功！