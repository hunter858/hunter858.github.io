---
layout: post
title: ios 关键字assign、weak、strong、copy该怎么用
date: 2018-02-26
categories: blog
tags:ios,weak,assign,strong,copy
description: 
---

在iOS开发中定义@property属性时，经常用到assign、weak、strong、copy等关键字。我们经常会考虑在何时应该使用哪个关键字，尤其是在面试的时候，经常会被问到这些关键字之间的区别，下面详细和大家探讨一下



####assign：

用于对基本数据类型进行赋值操作，不更改引用计数。也可以用来修饰对象，但是，被assign修饰的对象在释放后，指针的地址还是存在的，也就是说指针并没有被置为nil，成为野指针。如果后续在分配对象到堆上的某块内存时，正好分到这块地址，程序就会crash。之所以可以修饰基本数据类型，因为基本数据类型一般分配在栈上，栈的内存会由系统自动处理，不会造成野指针。


####weak：
修饰Object类型，修饰的对象在释放后，指针地址会被置为nil，是一种弱引用。 
delegate为何要用weak修饰: 
在ARC环境下，为避免循环引用，往往会把delegate属性用weak修饰；在MRC下使用assign修饰。weak和strong不同的是：当一个对象不再有strong类型的指针指向它的时候，它就会被释放，即使还有weak型指针指向它，那么这些weak型指针也将被清除。

ARC下的strong等同于MRC下的retain都会把对象引用计数加1。

####copy：
会在内存里拷贝一份对象，两个指针指向不同的内存地址。一般用来修饰NSString等有对应可变类型的对象，因为他们有可能和对应的可变类型（NSMutableString）之间进行赋值操作，为确保对象中的字符串不被修改 ，应该在设置属性是拷贝一份。而若用strong修饰，如果对象在外部被修改了，会影响到属性。

block属性为什么需要用copy来修饰？

因为在MRC下，block在创建的时候，它的内存是分配在栈(stack)上的，而不是在堆(heap)上，可能被随时回收。他本身的作于域是属于创建时候的作用域，一旦在创建时候的作用域外面调用block将导致程序崩溃。通过copy可以把block拷贝（copy）到堆，保证block的声明域外使用。在ARC下写不写都行，编译器会自动对block进行copy操作。

####__block与__weak的区别

__block：在ARC和MRC下都可用，可修饰对象，也可以修饰基本数据类型。

__block对象可以在block被重新赋值，__weak不可以。

__weak：只在ARC中使用，只能修饰对象，不能修饰基本数据类型（int、bool）。

同时，在ARC下，要避免block出现循环引用，经常会：__weak typedof(self) weakSelf = self;