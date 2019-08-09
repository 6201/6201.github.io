---
title: Vue中关闭ESLint
date: 2018-07-05 10:00:51
tags: 记录
categories: 编程
---

build文件夹下webpack.base.conf.js文件中，找到

```json
{
   test: /\.(js|vue)$/,
   loader: 'eslint-loader',
   enforce: 'pre',
   include: [resolve('src'), resolve('test')],
   options: {
     formatter: require('eslint-friendly-formatter')
   }
 },
```

注释掉。

Vue-cli3.0呢？有个GUI，里面可以设置（待验证）