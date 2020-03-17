---
title: 如何在dva中写轮询
date: 2019-08-21 09:41:48
tags: 记录
categories: 编程
---

项目需要使用轮询，现在的开发环境已经从vue变化到了，react、dva、umi、antd这一系列。

轮询咱之前也写过，使用setTimeout递归调用。

但是在dva中好像会导致卡死，（不知道什么原因，没有时间去研究，吐槽一下这家公司加班加成狗）

然后搜索时看到在dva/redux-saga中使用generator函数实现：

写一个延时函数：

```javascript
function delay(millseconds) {
  return new Promise(function(resolve) {
    setTimeout(resolve, millseconds);
  });
}
```

在dva的effects中写一个循环：

```javascript
    *pollingNewMessage(_, { call, put, select }) {
      while (true) {
        yield call(delay, 5000);
        const { content: oldContent } = yield select(state => state.message);
        const lastId = getlastId(oldContent);
        const res = yield call(getListInfo, { way: 'new', leavingMessageId: lastId, corpId });
        yield put({
          type: 'saveState',
          payload: {
            content: res,
          },
        });
      }
    },
```

这样就实现了一个不能停止的轮询了。



但是要注意如果在componentDidMount生命周期中dispatch的话，每次组件从新加载都会再发器一个effects，

我的方法是在model中设置一个first字段，第一次进入的时候才会发起effects，防止多次调用。





参考链接：[怎样在dva中写轮询逻辑](https://github.com/frontend9/fe9-library/issues/25)

