
---
layout: post
title: React-Native 之基础控件使用 （六）
date: 2018-01-29
categories: blog
tags:ios, react-native
description: 
---


引入控件需要这样设置，在你的 React-Native js中；


### 引入系统控件
```
import React, { Component } from 'react';
import {
  Platform,
  StyleSheet,
  Text,
  View,
  TextInput,
  TabBarIOS,
  Dimensions,
  ScrollView,
  Image,
  ListView,
  NavigatorIOS,
} from 'react-native';

```

### 获取屏幕宽、高、比例

需要引入系统 `Dimensions`；
 
```
const ScreenWidth = Dimensions.get('window').width; //屏幕宽
const ScreenHeight = Dimensions.get('window').height; //高
const ScreenScale = Dimensions.get('window').scale;//比例
```

### 自定义控件

创建 一个 TopView.js 的文件 （文件名首字母要大写);

```
/* 模版案例 */
	
import React ,{Component} from 'React';
import  {
  AppRegistry ,
  View,
  Text,
  Dimensions,
  StyleSheet,
 }from 'react-native';
	
const ScreenWidth = Dimensions.get('window').width; //屏幕宽
const ScreenHeight = Dimensions.get('window').height; //高
const ScreenScale = Dimensions.get('window').scale;//比例
	
	
export default class TopView extends Component {
  render() {
    return (
      <View style={styles.showTop}>
          <Text>测试一下自己封装的-控件<Text/>
      </View>
    );
  }
}
	
const styles = StyleSheet.create({
  showTop:{
    flex:1,
    width:ScreenWidth,
    height:50,
    marginTop:20,
    backgroundColor:'#F5FCF0',
  },
});
module.exports = TopView;  

```

在别的js 内引入这个js 模块
./ 表示在当前目录下
../ 表示在上层目录下
	
	import TopView from './TopView.js';


###Image 控件

	 <Image style={{width:100,height:100}} source={require('../img/timg.gif')} />
	 <Image style={{width:100,height:100}} source ={{uri:'http://media.china-sss.com/img/M00/00/09/wKjFbVpdhpqAKoPYAAC_jThbSRo029.jpg'}} />
	 
	 注意：Image 控件需要第一次需要设置一个宽高 ，否则无法显示出来
 
###Text 控件
 
	<Text style={{width:320,height:50}}> {这里放显示的文字内容}  </Text>
	

###View 控件
	<View style={{width:320,height:50,backgroundColor:'#F5FCF0'}}>	
	
###TextInput 控件	
```
<TextInput
        style={styles.textView}
        placeholder="搜索....."
        placeholderTextColor='#6435c9'
        // autocorrect ={false}
        // editable={false}
        //keyboardType="numeric"                  //键盘类型 'email-address' 'url' 'web-search'
        //multiline  			                    //是否多行显示
        //clearButtonMode = 'while-editing'       //'unless-editing'
        //clearTextOnFocus ={true}
        // enablesReturnKeyAutomatically={true}   // 显示return 按钮
        //autoFocus ={true}
        returnkeyType="send"                      //'send' 'join' return按钮显示的文字
        onFocus={() => console.log('onFocus')}    //对焦触发的事件
        onBlur={() => console.log('onBlur')}      //onBlur触发的事件  
        onChange= {() => console.log('onChange')}
        onChangeText={(text) => {
                   
          console.log('text:'+ text);
   
        }}									          //input输入框值改变触发的事件
        onEndEditing ={()=> console.log('onEndEditing')}  //停止编辑触发的事件
        onSubmitEditing ={()=> {
        
          this.FetchSearchData();
          
        }} //点击提交按钮触发的事件 ,FetchSearchData 是一个自定义事件

      />	
      
```



###TabBarIOS 控件

```

	<TabBarIOS
		      style={{height:49,width:ScreenWidth}}
		      tintColor="green" //被选中的标签的颜色
		      barTintColor="white" //tabbarIOS 背景色
		      translucent={false}     // TabBarIOS不需要半透明效果
		      >
	</TabBarIOS>     

```
###TabBarIOS.Item 子控件-系统

```
	<TabBarIOS
          style={{height:49,width:ScreenWidth}}
          tintColor="green" 			//被选中的标签的颜色
          barTintColor="white" 			//tabbarIOS 背景色
          translucent={false}    		// TabBarIOS不需要半透明效果
          >
            <TabBarIOS.Item
              systemIcon="bookmarks"
              badge="15"    			//设置显示在右上角的值
              title="首页"   			   //如果是系统图标，则标题不会出现
              tintColor="green"   		// 被选中标签颜色
              barTintColor="black"      // TabBarIOS背景色
              translucent={false}       // TabBarIOS不需要半透明效果
              /*下面写一些 点击select 的动作*/
              onPress={() => {this.setState({selectedTabItem:0})}}
              selected={this.state.selectedTabItem == 0}
            >
            </TabBarIOS.Item>
            
            <TabBarIOS.Item
                systemIcon="contacts"    // 系统图标(contacts)
            >
            </TabBarIOS.Item>
            
            <TabBarIOS.Item
                systemIcon="downloads"    // 系统图标(downloads)
            >
            </TabBarIOS.Item>
            
            <TabBarIOS.Item
                systemIcon="favorites"    // 系统图标(favorites)
            >
            </TabBarIOS.Item>
            
        </TabBarIOS>     

```    


###TabBarIOS.Item 自定义icon 图标和文字


```
<TabBarIOS.Item
              
              icon ={{uri:Icons.home,scale:4.6}}
              selectedIcon = {{uri:Icons.homeActive,scale:4.6}}
              badge="15"
              title="首页"  //如果是系统图标，则标题不会出现
              //icon={require('.image!home')} //自定义图标- 目前只支持本地图片
              //selectedIcon={require('image!baker')} //自定义高亮图标
              /*下面写一些 点击select 的动作*/
              onPress={() => {this.setState({selectedTabItem:0})}}
              selected={this.state.selectedTabItem == 0}
              >
</TabBarIOS.Item>


```

注意： 
这里的 `uri:Icons.home `是自己创建了一个Icons 的js 文件，export 图片的base64 编码；
`scale:4.6` 设置图标的显示比例；



###ListView 控件

```




```
