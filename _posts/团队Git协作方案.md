---
title: 团队Git协作方案 
date: 2017-10-13 14:11:05		
tags: [工作流程,git]            
categories: [团队协作,by杨佳欢]          
---
# 团队Git协作方案


git分支分类：

	1、master 
		当前最新的稳定版本
	2、developer
		用于发布前多人协作时合并


### 一、master分支规则

master分支主要分一下下两种

	1、master
		当前最新的稳定版本
	2、master-项目名称-版本号-封包时间
		例：master-gulugames-2.0.2-20171212

每一个稳定版本需要保存分支，保存的分支超过30个时，从最老的开始删除，保持最新的20个分支

<!-- more -->


### 二、developer分支规则

developer分支主要分为以下两种

	1、developer-项目名称-版本号-开始开发时间
		当前版本的开发版分支，用于合并其他人的分支后出包,在正式上线之后，合并进对应的master分支
		例：developer-gulugames-2.0.2-20171202
	2、人员简拼-developer-项目名称-版本号
		开发人员用于开发自己对应功能的分支，每个阶段开发完成后合并进1中的分支
		例：yangjh-developer-gulugames-2.0.2

用于合并的开发分支以及个人分支在<a name="fenced-code-block">正式封包并上线之后</a>删除

注：在个人developer分支合并进



## 二、git提交备注规范

git提交一般分为三种状况

### 一、jira任务提交

	1、jira-jira任务编号(-进度)		(这种主要是开发某个jira任务时提交，进度部分为可选)
	例：jire-SDK-23-50%(当前任务没有完成时)
		jira-SDK-23(当前任务完成时)


### 二、bug修复
	1、bug(-bugfree编号/bug描述)		(bugfree上的bug填bug编号，否则填bug描述)
	例：bug-6187
		bug-修复了登陆时不显示loading的问题


### 三、优化工作
	1、adv-(jira任务编号/优化描述)	(有jira任务时用jira编号，没有时用描述)
	例：adv-SDK-23
		adv-优化浮窗流畅性


​		
​		
		## 一、git分支管理
### 一、版本号规则：
	产品版本  2.0.0    别名：xxx （可理解为开发代号，可选）
	修订号    2.0.2    第二次修订,修复bug后的稳定版本             
	构建号    2.0.2.156    第156次build (没有jinkens自动打包时可先命名为：2.0.2)
	代码版本    2.0.2-release、更多为开发阶段git代码管理 
	
	发布版本号    一般同修行号一致    2.0.2

​		



