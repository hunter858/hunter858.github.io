---
layout: post
title: react-native 开发环境安装
date: 2018-01-08
categories: blog
tags: react-native,ios
description: 
---

react-native 实战

安装 HomeBrew

安装Node

```
brew install node
```


###Yarn ，react-native 的命令行工具
Yarn是Facebook提供的替代npm的工具，可以加速node模块的下载。React Native的命令行工具用于执行创建、初始化、更新项目、运行打包服务（packager）等任务。

```
npm install -g yarn react-native-cli
```

###Watchman
Watchman是由Facebook提供的监视文件系统变更的工具。安装此工具可以提高开发时的性能（packager可以快速捕捉文件的变化从而实现实时刷新）。译注：此工具官方虽然是推荐安装，但在实践中，我们认为此工具是必须安装，否则可能无法正常开发。

``` 
brew install watchman
```

###Flow

Flow是一个静态的JS类型检查工具。译注：你在很多示例中看到的奇奇怪怪的冒号问号，以及方法参数中像类型一样的写法，都是属于这个flow工具的语法。这一语法并不属于ES标准，只是Facebook自家的代码规范。所以新手可以直接跳过（即不需要安装这一工具，也不建议去费力学习flow相关语法）

	brew install flow


常用的js 版本工具

	brew install watchman flow git gcc pkg-config cairo libpng jpeg gitlib mongodb
	

Nodejs 的版本管理工具 nvm 安装

	curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash
	
	
	



创建第一个项目

	react-native init AwesomeProject  
	//创建一个项目 AwesomeProject
	
	cd AwesomeProject
	//进入AwesomeProject 项目文件夹内
	
	react-native run-ios	
	//运行ios版本的 AwesomeProject 项目


`react-native run-ios `
//运行ios 项目

`react-native run-android`
//运行安卓项目


报错

```
No bundle URL present
Make sure you’re running a packager server or have included
 a .jsbundle file in your application bundle

```
[http://blog.csdn.net/suyie007/article/details/70768410]()

