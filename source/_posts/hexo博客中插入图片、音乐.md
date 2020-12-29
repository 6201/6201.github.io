---
title: hexo博客中插入图片、音乐
date: 2018-04-20 13:00:01
tags: 记录
categories: 博客
---
### 1.前言  
  用hexo+github pages作个人博客正的是很好很方便很便宜。可以使用markdown直接在本地写好文章，再使用hexo g -d 直接发布。而且hexo还有一些标签插件语法，丰富了markdown生成html后的效果。

### 2.标签插件  
标签插件有许多，今天要用到的是：  
##### iframe  
在文章中插入 iframe。 

`{ % iframe url [width] [height] % }`

##### Image  
在文章中插入指定大小的图片。

`{ % img [class names] /path/to/image [width] [height] [title text [alt text]] % }`  

### 3.使用  
iframe标签插件用处可大了，所有浏览器都支持`iframe`标签，iframe元素会创建包含另外一个文档的内联框架。而一般的视屏网站、音乐网站等都有分享iframe标签的选项，例如： 

\!\[youku的分享选项](hexo博客中插入图片、音乐/youku.png):
![youku的分享选项](/images/youku.png) 


其中iframe的内容为： 
	`<iframe height=498 width=510 src='http://player.youku.com/embed/XMzQyODk1NjMyMA==' frameborder=0 'allowfullscreen'></iframe>`

也可以引用音乐，是一样的。
图片的引用：
首先设置`config.yml`文件中的post_asset_folder 选项为`true`来打开。  

{% codeblock _.config.yml %}
post_asset_folder: true
{% endcodeblock %}  

当资源文件管理功能打开后，Hexo将会在你每一次通过 `hexo new [layout] <title>` 命令创建新文章时自动创建一个文件夹。这个资源文件夹将会有与这个 markdown 文件一样的名字。将所有与你的文章有关的资源放在这个关联文件夹中之后，你可以通过相对路径来引用它们，这样你就得到了一个更简单而且方便得多的工作流。  

### 相对路径引用的标签插件  
通过常规的 markdown 语法和相对路径来引用图片和其它资源可能会导致它们在存档页或者主页上显示不正确。在Hexo 2时代，社区创建了很多插件来解决这个问题。但是，随着Hexo 3 的发布，许多新的标签插件被加入到了核心代码中。这使得你可以更简单地在文章中引用你的资源。  
{% codeblock %}
{ % asset_path slug % }  
{ % asset_img slug [title] % }
{ % asset_link slug [title] % }   
{% endcodeblock %}
比如说：当你打开文章资源文件夹功能后，你把一个 example.jpg 图片放在了你的资源文件夹中，如果通过使用相对路径的常规 markdown 语法 \!\[](/example.jpg) ，它将 不会 出现在首页上。（但是它会在文章中按你期待的方式工作）  
正确的引用图片方式是使用下列的标签插件而不是 markdown ：  
{% codeblock %}
{ % asset_img example.jpg This is an example image % }
{% endcodeblock %}
