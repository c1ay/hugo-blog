+++
date = "2016-01-14T13:35:32+08:00"
title = "hugo"
draft = true

+++

## 使用hugo:
一直想学习`golang`，看到了`hugo`，想用hugo弄个博客，找到官方网站，跟着文档一步步来，安装，选主题，配置，没什么问题。步骤和`hexo`一样。

## 踩坑:
* 第一个坑：使用持续集成---`wercker`，官方文档中使用的`wercker`，应该是以前的版本，新版本已经将deploy去掉，变成可配置的工作流，需要自己加一个pipline
* 第二个坑：文档中是没有例子怎么将网站push到github pages，使用`leipert/git-push` push到github，这个项目是有bug:
	
		run.sh: line 5: getAllStepVars: command not found

这个作者已经很久更新了，而且issue里是有人提了这个bug，也提交了pr，作者也没有更新。所以换做`ysqi/git-push`


## 使用`CI`(持续集成):
持续集成，我的感觉是将软件发布的流程自动化：

* 提交：对于开发者而言，是一次`commit`
* 构建：build, 将源码构建为实际运行代码
* 测试：跑测试
* 部署