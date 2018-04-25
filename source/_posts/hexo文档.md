---
title: hexo文档[一]
date: 2018-04-03 17:10:38
tags: 记录  
---

### 什么是Hexo？ 
Hexo是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
<!--more-->
### 安装  
安装 Hexo 只需几分钟时间，若您在安装过程中遇到问题或无法找到解决方式，请提交问题，我会尽力解决您的问题。

#### 前置  
* Node.js
* Git  

` $ npm install -g hexo-cli `

### 指令  
#### init  

` $ hexo init [folder] `  

新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。

#### new  

` $ hexo new [layout] \<title> `  

新建一篇文章。如果没有设置 `layout` 的话，默认使用 _config.yml 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。 

#### generate  

` $ hexo generate `   

可简写为  
` $ hexo g ` 

| 选项 | 描述 |  
| -----| ----- |  
| -d,--deploy | 文件生成后立即部署网站 |  
|-w,--watch | 监视文件变动 |  

#### publish  
` $ hexo publish [layout] \<filename> ` 
发表草稿。 

#### server  
` $ hexo server ` 

安装 server  
 `$ npm install hexo-server --save`  

启动服务器。默认情况下，访问网址为： http://localhost:4000/
 
| 选项 | 描述 |  
| -----| ----- |  
| -p,--port | 重设端口 |  
|-s,--static | 只使用静态文件 |  
| -l,--log | 启动日记记录，使用覆盖记录格式 |  
 