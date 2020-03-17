---
title: 项目中添加sentry记录一下配置
date: 2019-10-29 09:41:48
tags: 记录
categories: 编程
---

我们的项目使用react+umi+dev 配置sentry基本参考react+webpack就可以了。

在项目中引入'@sentry/webpack-plugin'、'umi-plugin-react'、'umi-plugin-react'

```javascript
// 引入需要的库
yarn add @sentry/webpack-plugin umi-plugin-react umi-plugin-react --dev

```

 /config/config.js中：

添加下列配置项：

其中devtool是配的source-map，chainWebpack内部的options可以参考https://github.com/getsentry/sentry-webpack-plugin

```javascript
  devtool: 'nosources-source-map',
  disableCSSSourceMap: true,
  chainWebpack(config, {}) {
    if (process.env.BUILD_ENV === 'production') {
      config.plugin('sentry').use(SentryPlugin, [
        {
          ignore: ['node_modules', 'mock'],
          include: './dist',
          configFile: './.sentryclirc',
          release: version,
        },
      ]);
    }
  },
```

 新建/.sentryclirc文件

配置 其中选项需要和sentry设置匹配,http://sentry.xiaoyuanhao.com:9000/auth/login/sentry/

```
[defaults]
url = http://47.110.165.108:9000
org = sentry
project = paz


[auth]
token = fae1d54165c54ec589aa467043e24eadb960378dcc16411f910e69c02f1dee93
```

 /src/app.js

增加 其中dsn 需要找运维http://121.43.34.186:40188/pages/viewpage.action?pageId=2036199

```javascript
import * as Sentry from '@sentry/browser';

if (ENV === 'production') {
  Sentry.init({ dsn: 'http://7b24fae9283c4a0caa9d76da82a1d564@47.110.165.108:9000/2' });
}
```





