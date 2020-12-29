---
title: Vscode中使用ExperimentalDecorators报错
date: 2018-04-21 13:59:50
tags: 记录
categories: 编程
---
vscode中使用es7的新语法decorator（装饰器）会报错，如图：  
![error](/images/error.png)  
<!--more-->
这是来自于vscode的JS support的错误,只要在项目根目录下创建一个jsconfig.json文件，添加如下内容：  
{% codeblock %}
{
    "compilerOptions": {
        "experimentalDecorators": true
    }
}
{% endcodeblock %}  
![新建jsconfig.json文件](/images/2.png)

添加好后重启生效！
