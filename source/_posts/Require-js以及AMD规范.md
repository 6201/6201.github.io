---
title: Require.js以及AMD规范
date: 2018-05-15 10:50:07
tags: 学习
categories: 编程
---

### 概述

RequireJS是一个工具库，主要用于客户端的模块管理。通过特定的语法，可以把分散在各个文件中的代码变成一个一个模块，实现异步或动态加载，从而提高代码的性能和可维护性。它的模块管理遵守AMD规范（Asynchronous Module Definition）。

RequireJS的基本思想是，通过define方法，将代码定义为模块，通过require方法，实现代码的模块加载。

相对于ES6，是export和import。不过用法还是有些不同。

首先，将require.js嵌入网页，然后就能在网页中进行模块化编程了。

`<script data-main="scripts/main" src="scripts/require.js"></script>`

上面大代码的data-main属性不可省略，用于指定主代码所在的脚本文件，上例为scripts子目录下的main.js文件。用户自定义的代码就放在这个main.js文件中。

### define方法：定义模块

#### 1. 独立模块

```Javascript
define({
    method1:function() {},
    method2:function() {},
});
```

或者：

```Javascript
define(function() {
    return {
        method1: function() {},
        method2: function() {},
    };
});
```

#### 2. 非独立模块 

```Javascript
define(['modulel','module2'], function(m1,m2){
    ...
});
```

define方法的第一个参数是一个数组，他的成员是当前模块所依赖的模块。m1对应module1，m2对应module2，这里这个函数必须返回一个对象，供其他模块调用。

### require方法：调用模块

require方法用于调用模块。它的参数与define方法类似。

```javascript
require(['foo','bar'], function (foo, bar) {
    foo.doSomething();
});
```

可以用在define方法内部。

```javascript
define(function(require) {
    var otherModule = require('otherModule');
});
```

require方法允许添加第三个参数，即错误处理的回调函数。

```Javascript
require (
	["backbone"], 
	function(Backbone) {
    	return Backbone.View.extend({/* ... 	*/});
},
	function (err) {
        // ...
	}
);
```

### 配置require.js: config方法

require方法本身也是一个对象，它带有一个config方法，用来配置require.js运行参数。config方法接受一个对象作为参数。

```Javascript
require.config({
    path: {
        jquery: [
            '//cdnjs.cloudflare.com/ajax/libs/jquery/2.0.0/jquery.min/js',
            'lib/jquery'
        ]
    }
});
```

config方法的参数对象有一下主要成员：

1. paths
2. baseUrl
3. shim

### 插件

下面是插入文本数据所使用的text插件的例子。

```Javascript
define([
    'backbone',
    'text!templates.html'
], function( Backbone, template) {
    // ...
});
```

