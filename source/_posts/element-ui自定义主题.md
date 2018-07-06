---
title: element-ui自定义主题
date: 2018-07-05 10:12:00
tags: 学习
categories: 
- Element-ui
---

#### Element-ui自定义主题

* 仅替换主题色
* 在项目中改变SCSS变量
* 命令行主题工具
  - 安装工具  `npm i element-theme -g`
  - 安装主题`npm i element-theme-chalk -D  或 npm i`
  - `https://github.com/ElementUI/theme-chalk -D`
  - 初始化变量文件  `et -i [可以自定义变量文件]`
  - 修改生成的变量文件
  - 编译主题 `et 或 et -W（watch）-c （文件名）`
  - main.js中引入自定义主题 `import '../theme/index.css'`

#### 第三方iconfont

iconfont，svg的fill属性，可继承。需要特定的颜色时可以在svg文件中定义好，但是需要可根据不同状态变更颜色的svg就可以不添加fill这个属性，在父元素上添加就可以像控制font-color一样用css控制了。