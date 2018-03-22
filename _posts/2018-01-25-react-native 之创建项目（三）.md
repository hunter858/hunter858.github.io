---
layout: post
title: react-native 之创建项目（三）
date: 2018-01-25
categories: blog
tags: ios,react-native
description: 
---

react-native 官方demo 初体验

[git clone https://github.com/facebook/react-native.git](git clone https://github.com/facebook/react-native.git)


	//帮助
	react-native -h
	
	//查看ReactNative版本
	react-native --version  
	
	//升级
	npm update -g react-native-cli
	
	//查看本地ReactNaitve 版本信息
	npm info react-native
	
	//工程下载安装RN环境,根据配置文件package.json
	npm install 
	
	//初始化一个工程、并下载源代码和依赖包（时间较慢）
	react-native init   项目名称
	
	//运行Android项目
	react-native run-android
	
	//运行iOS项目
	react-native run-ios
	
	//根据package.json配置的RN版本,更新RN环境代码
	react-native upgrade                     
	 
	//项目降级或升级到指定版本,记得react-native upgrade更新一下项目依赖等
	npm install --save react-native@0.46     
	
	//在android目录下操作打包
	gradlew assembleRelease




在项目中使用 react-native-tab-navigator 

（1）安装
在项目根目录下 使用命令行安装 
`npm install react-native-tab-navigator --save`
（2）导入
`import TabNavigator from 'react-native-tab-navigator';`

	<Image source={{uri: 'https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo_top_ca79a146.png'}}
	       style={styles.imageView} />
	       
	  imageView:{
	    width: 300,
	    height: 65,
	    // backgroundColor:'red',
	    // resizeModel:'cover',//图片居中显示且不拉伸图片，超出的部分剪裁掉
	    // resizeModel:'contain',//容器完全容纳图片，图片等比例进行拉伸
	     resizeMode:'stretch',//图片被拉伸至与容器大小一致，可能会发生变形
	
	  }   
	  
	  
	  
scrollview 使用  [http://blog.csdn.net/mengks1987/article/details/70228624]()	  


React.createClass和extends Component的区别 
[https://segmentfault.com/a/1190000005863630]()