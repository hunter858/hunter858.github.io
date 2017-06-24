---
layout: post
title: git 之sourceTree使用
date: 2014-10-1
categories: blog
tags: git
description: 
---
### 主要内容

1. OSChina仓库的配置

2. sourceTree加载OSChina仓库

2. sourceTree加载OSChina仓库

3. sourceTree的基本使用(创建分支，回滚操作，合并分支等)

4. 常见的报警

5. 使用OSChina的注意事项

### 文章开始

* 1.1 配置OSChina仓库
* 1.2 OSChina网址:OSChina(码云)
* 1.3 码云介绍:码云(Git@OSC)是开源中国社区团队推出的基于Git的快速的、免费的、稳定的在线代码托管平台,不限制私有库和公有库数量.为什么选择在码云上布置项目呢，由以下两个主要原因:
原因一：码云是国内的服务器，响应速度快
原因二：码云的私有项目免费
* 1.4 在OSChina上创建项目
使用自己的账号登录之后，点击左下方的项目栏，点击+号，创建新的项目


![](http://opevtrwe5.bkt.clouddn.com/2979388-503a1871b916ef12.png)

#### 项目内容的填写
![](http://opevtrwe5.bkt.clouddn.com/2979388-ec4cd64ba7ea4eb5.png)




#### 2. sourceTree加载OSChina仓库
* 2.1  将git地址复制到sourceTree中，加载远程仓库的项目，
创建项目之后，复制这个项目的远程仓库的地址

![](http://opevtrwe5.bkt.clouddn.com/2979388-5a9fa0e4c3be6cd6.png)

打开SourceTree软件，加载新仓库,将上图的地址黏贴到下图的位置

![](http://opevtrwe5.bkt.clouddn.com/2979388-b174d7af683868d3.png)

黏贴码云远程仓库的地址

![](http://opevtrwe5.bkt.clouddn.com/2979388-6baf5f74f646f7ed.png)



点击‘克隆’之后，这里sourceTree会自动在‘目标路径’下创建一个文件夹本地创建一个文件夹，里面有(看到.git需要打开隐藏文件，在终端中输入):

	```
	.git         ->文件夹
	.gitignore  ->忽略文件
	README.markdown ->说明文档
	```



![](http://opevtrwe5.bkt.clouddn.com/2979388-f807d8d051d9d32f.png )

* 2.2 创建需要管理的代码文件项目到桌面，这里为开发iOS,通过Xcode创建一个项
目:MaYunShow.project

* 2.3 将步骤‘2.2’创建的项目文件夹拖拽到步骤‘2.1’的文件夹中，拖拽后的文件层级为:
	```
	.git         ->文件夹
	.gitignore  ->忽略文件
	README.markdown ->说明文档
	MaYunShow   ->项目文件夹
	```
* 2.4 提交本地修改到本地仓库，添加修改内容

![](http://opevtrwe5.bkt.clouddn.com/2979388-0e9a4dad12798ee5.png )

![](http://opevtrwe5.bkt.clouddn.com/2979388-1644b95f73dfa030.png )

* 2.5 将本地仓库推送到远程仓库


![](http://opevtrwe5.bkt.clouddn.com/2979388-1f0fe991ecf6ae56.png)

![](http://opevtrwe5.bkt.clouddn.com/2979388-9d10f605c4ae6df6.png )

### 3.sourceTree的基本使用

* 3.1 创建分支


![](http://opevtrwe5.bkt.clouddn.com/2979388-b982bbb0ec964a46.png)

* 3.1 提交改动到本地仓库分支-分支1

![](http://opevtrwe5.bkt.clouddn.com/2979388-33e92f49ea83ab65.png )

* 3.3 推送到远程仓库


![](http://opevtrwe5.bkt.clouddn.com/2979388-c3cc24b178a45722.png )

* 3.4 合并分支
有两个分支:分支一 、分支一的分支，合并这两个分支，首先双击分支一，点击菜单栏”合并“

![](http://opevtrwe5.bkt.clouddn.com/2979388-a92a5295bee679bb.png )

![](http://opevtrwe5.bkt.clouddn.com/2979388-4dcf590292d160cb.png )

* 3.4.1 冲突处理

![](http://opevtrwe5.bkt.clouddn.com/2979388-1d77fcbbfbb5ff3d.png )

解决冲突方法一:

查看冲突，可选择'暂存区块'或者选中某行后‘暂存行块’，或者‘放弃区块’或者选中某行后‘暂存行块’


![](http://opevtrwe5.bkt.clouddn.com/2979388-614d045f06d41ca3.png)

解决冲突方法二:

通过菜单栏->动作->解决冲突,一般在冲突较多时候采取该方法


![](http://opevtrwe5.bkt.clouddn.com/2979388-9f5579756425e4aa.png )

* 3.5 回滚操作

这里把"在MJStudent中增加了eat方法"步骤回滚到增加前的状态

![](http://opevtrwe5.bkt.clouddn.com/2979388-e2ebf3ce4a3e9ed4.png )

![](http://opevtrwe5.bkt.clouddn.com/2979388-dbe3633f8702481d.png )

### 4.常见的报警
* 4.1 推送前未提交本地的改动，推送前提交本地改动再推送即可

![](http://opevtrwe5.bkt.clouddn.com/2979388-5a39424c5522d400.png )

* 4.2 网络异常报警
公司网络不稳定，就会时常发生这个报警，待网络情况好转后再次尝试即可

![](http://opevtrwe5.bkt.clouddn.com/2979388-8f53989ef2e9f1a4.png )

* 4.3 推送的远程分支仓库权限受到只读保护，发生此报警，可查看'步骤5'，取消只读权限

![](http://opevtrwe5.bkt.clouddn.com/2979388-c56cfae9bc8c395b.png )

### 5.使用OSChina的注意事项
* 5.1 使用码云创建项目时，需要管理分支的权限，特别是master分支的权限，一般设为只读，其他的分支权限设为常规分支

![](http://opevtrwe5.bkt.clouddn.com/2979388-21d29e8171dafb4a.png )

![](http://opevtrwe5.bkt.clouddn.com/2979388-57fd2f1bb858b615.png )

![](http://opevtrwe5.bkt.clouddn.com/2979388-79a03e3dbd8fb330.png )

* 5.2 执行回滚时，有一定概率会造成代码全部丢失，可双击最新的分支行即可读取‘revert xxx’前的状态


### 三、SourceTree&Git部分名词解释

* 克隆(clone)：从远程仓库URL加载创建一个与远程仓库一样的本地仓库

* 提交(commit)：将暂存文件上传到本地仓库（我们在Finder中对本地仓库做修改后一般都得先提交一次，再推送）

* 检出(checkout)：切换不同分支

* 添加（add）：添加文件到缓存区

* 移除（remove）：移除文件至缓存区

* 暂存(git stash)：保存工作现场

* 重置(reset)：回到最近添加(add)/提交(commit)状态

* 合并(merge)：将多个同名文件合并为一个文件，该文件包含多个同名文件的所有内容，相同内容抵消

* 抓取(fetch)：从远程仓库获取信息并同步至本地仓库

* 拉取(pull)：从远程仓库获取信息并同步至本地仓库，并且自动执行合并（merge）操作，即 
pull=fetch+merge
* 推送(push)：将本地仓库同步至远程仓库，一般推送（push）前先拉取（pull）一次，确保一致

* 分支(branch)：创建/修改/删除分枝

* 标签(tag):给项目增添标签

* 工作流(Git Flow):团队工作时，每个人创建属于自己的分枝（branch），确定无误后提交到master分枝

* 终端(terminal):可以输入git命令行
