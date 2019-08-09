---
title: gulp文档【一】
date: 2018-04-26 22:13:08
tags: 记录
categories: 编程
---

gulp是基于Nodejs的自动任务运行器， 她能自动化地完成javascript/coffee/sass/less/html/image/css 等文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。在实现上，她借鉴了Unix操作系统的管道（pipe）思想，前一级的输出，直接变成后一级的输入，使得在操作上非常简单。通过本文，我们将学习如何使用Gulp来改变开发流程，从而使开发更加快速高效。  

gulp 和 grunt 非常类似，但相比于 grunt 的频繁 IO 操作，gulp 的流操作，能更快地更便捷地完成构建工作。

### 入门指南

1. 全局安装gulp:  

	`$ npm install --global gulp`

2. 作为项目的开发依赖（devDependencies）安装：

	`$ npm install --save-dev gulp`

3. 在项目根目录下创建一个名为gulpfile.js的文件：  

	```
	var gulp = require('gulp');

	gulp.task('default', function() {
  	// 将你的默认的任务代码放在这
	});   
	```

4. 运行gulp：

 	`$ gulp` 



默认的名为 default 的任务（task）将会被运行，在这里，这个任务并未做任何事情。

想要单独执行特定的任务（task），请输入 `gulp <task> <othertask>`。  

## 下一步做什么呢？

你已经安装了所有必要的东西，并且拥有了一个空的 gulpfile。那怎样才算是__真的__入门了呢？可以查看这些 [秘籍](https://www.gulpjs.com.cn/docs/recipes/) 和这个 [文章列表](https://www.gulpjs.com.cn/docs/#articles/) 来学习更多的内容。