---
title: hexo在github建个博客
date: 2018-03-09 10:15:42
tags: 记录
---
### 前言 
	
在建立这个个人博客的时候遇到了许多的问题，解决问题的过程也是学习的过程，在这里做一些记录，加强记忆，以防一段时间后遗忘。

### 今天完成了域名的设置

github 相当于提供了免费的服务器 只要以github做仓库，设置github pages 可以展示为，静态页面的个人博客。

之前脑抽买了一个域名，闲置了一段时间，闲置打算设置为个人博客。
用HEXO生成个人博客，另外用vue做一个首页。个人博客设置为二级域名blog.yzczjp.com,首页设置为yzczjp.com 挺好！  

1. 需要记录的是： DNS管理中设置A githubserveIP（192.30.252.153)。  
2. 另外设置: CNAME属性到 github上的博客项目的6201.github.io/blog  
3. github 仓库中新建一个CNAME文件，内容为blog.yzczjp.com  



