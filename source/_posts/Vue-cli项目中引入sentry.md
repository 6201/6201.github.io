---
title: Vue-cli项目中引入sentry
date: 2020-03-28 14:37:52
tags: 记录
categories: 工具
---

之前在react项目中引入过一次sentry项目，这次需要在Vue-cli项目中引入。基本原理是一样的，还是用webpack-plugin来上传source-map。

sentry后台管理页面可以使用官方版（需要付费），也可以自己搭建。这次直接在官网上配置。

1.新建组织、新建项目。

![](/images/1284F30E-205E-4CB4-A88F-1FDC06EAE8B6.png)

2.生成客户端密钥。

![](/images/205B1300-4B2C-45E4-8583-BA46F0462CE2.png)

3.vue-cli项目中：

```bash
npm install @sentry/browser @sentry/integrations -S
```

4.main.js中添加代码：

```javascript
// sentry
import * as Sentry from '@sentry/browser';
import * as Integrations from '@sentry/integrations';


process.env.NODE_ENV === 'production' && Sentry.init({
  dsn: '你的客户端密钥DNS',
  integrations: [
    new Integrations.Vue({Vue, attachProps: true}),
  ],
});
```

5.使用`@sentry/webpack-plugin`打包时自动上传source-map文件

```bash
npm install @sentry/webpack-plugin -D
```

6.在根目录创建文件`.sentryclirc` 内容:

```
[defaults]
url=https://sentry.io
org=eaton
project=vue

[auth]
token=abe8eada0dc5431681ad6cf49f16f17e975202216aa84e93bcbb7a6047afaa2e //上图中 API Keys 中对应的AUTH TOKEN
```

7.在vue.config.js中添加：

```javascript
const SentryPlugin = require('@sentry/webpack-plugin')

module.exports = {
...
  productionSourceMap: true, // 设置为true打包时包含source-map文件
  chainWebpack: config => {
    if (process.env.ENV === 'production') {
      config.plugin('sentry').use(SentryPlugin, [{
        // 指定忽略文件配置
        ignoreFile: ['node_modules', '.gitignore'],
        // 指定上传目录
        include: './dist',
        // 指定sentry上传配置
        configFile: './.sentryclirc',
        // 指定发布版本
        release: process.env.RELEASE_VERSION,
        // 保持与publicPath相符
        urlPrefix: '~/owner/'
      }])
    }
  },
}
```

8.修改`npm run build`命令在打包上传完成后删除source-map文件：

//package.json

```json
"scripts": {
	"build": "vue-cli-service build && rm -rf dist/static/js/*.map"
}
```

最后可以在管理页面中看到上报的事件：

![](/images/ECB8D8DB-61B4-4C4F-88C6-19ECC88B7CE2.png)

![](/images/7009E16C-66D1-4FEC-8EDD-C4D6A064C300.png)

上传了source-map后可以准确的定位到错误产生的那一行，这里是为了测试使用了未定义的变量a。

