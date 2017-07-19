---
layout: post
title: 九个console命令，让js 调试更简单
---
### 一、显示信息的命令

	 console.log('详情');
	 console.error('错误');
	 console.warn('警告');


### 二：占位符console上述的集中度支持printf的占位符格式，支持的占位符有：字符（%s）、整数（%d或%i）、浮点数（%f）和对象（%o）

	 console.log("%d年%d月%d日",2015,6,28);


### 三、信息分组

	console.group("我的信息");
	console.log("用户名:tpythoner");
	console.log("我的博客:OSCHINA(http://my.oschina.net/tpythoner)");
	console.groupEnd();


### 四、查看对象的信息

	  console.dir()可以显示一个对象所有的属性和方法。
	
	
	 var info = {'username' : 'tpythoner', 'email' : 'admin@gmail.com'};
	 console.dir(info);

### 五、显示某个节点的内容

	console.dirxml()用来显示网页的某个节点（node）所包含的html/xml代码。


	<div id="info">
	    <p>程序爱好者:tpyhoner</p>
	</div>
	<script type="text/javascript">
	    var info = document.getElementById('info');
	    console.dirxml(info);
	</script>

### 六、判断变量是否是真

	console.assert()用来判断一个表达式或变量是否为真。如果结果为否，则在控制台输出一条相应信息，并且抛出一个异常。
	
	var result = 1;
	console.assert(result);
	var year = 2015;
	console.assert(year == 2016);
	
	1是非0值，是真；而第二个判断是假，在控制台显示错误信息 

### 七、追踪函数的调用轨迹。


	console.trace()用来追踪函数的调用轨迹。
	
	<script type="text/javascript">
	/*函数是如何被调用的，在其中加入console.trace()方法就可以了*/
	　　function add(a,b){
	        console.trace();
	　　　　return a+b;
	　　}
	　　var x = add3(1,1);
	　　function add3(a,b){return add2(a,b);}
	　　function add2(a,b){return add1(a,b);}
	　　function add1(a,b){return add(a,b);}
	</script>

### 八、计时功能

	console.time()和console.timeEnd()，用来显示代码的运行时间。
	
	<script type="text/javascript">
	　　console.time("控制台计时器一");
	　　for(var i=0;i<1000;i++){
	　　　　for(var j=0;j<1000;j++){}
	　　}
	　　console.timeEnd("控制台计时器一");
	</script>

### 九、console.profile()的性能分析
	
	function doTask(){
	  doSubTaskA(1000);
	  doSubTaskA(100000);
	  doSubTaskB(10000);
	  doSubTaskC(1000,10000);
	}
	function doSubTaskA(count){
	  for(var i=0;i<count;i++){}
	}
	 
	function doSubTaskB(count){
	  for(var i=0;i<count;i++){}
	}
	 
	function doSubTaskC(countX,countY){
	  for(var i=0;i<countX;i++){
	    for(var j=0;j<countY;j++){} 
	  }
	}
	console.profile();
	doTask();
	console.profileEnd();

性能分析`（Profiler）`就是分析程序各个部分的运行时间，找出瓶颈所在，使用的方法是`console.profile()`。