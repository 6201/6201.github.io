---
title: 移动端css适配
date: 2018-12-29 17:47:57
tags: 记录
categories: 编程
---

### 移动端适配方案（rem，vw）

现在看到主流的移动端适配有rem [《使用Flexible实现手淘H5页面的终端适配》](https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html)，随着viewport单位被越来越多的浏览器支持，也出现了使用vw来做移动端的适配问题 [如何在Vue项目中使用vw实现移动端适配](https://www.w3cplus.com/mobile/vw-layout-in-vue.html)。



先说说flexible适配中的代码：

```javascript
(function flexible (window, document) {
  var docEl = document.documentElement
  var dpr = window.devicePixelRatio || 1

  // adjust body font size
  function setBodyFontSize () {
    if (document.body) {
      document.body.style.fontSize = (12 * dpr) + 'px'
    }
    else {
      document.addEventListener('DOMContentLoaded', setBodyFontSize)
    }
  }
  setBodyFontSize();

  // set 1rem = viewWidth / 10
  function setRemUnit () {
    var rem = docEl.clientWidth / 10
    docEl.style.fontSize = rem + 'px'
  }

  setRemUnit()

  // reset rem unit on page resize
  window.addEventListener('resize', setRemUnit)
  window.addEventListener('pageshow', function (e) {
    if (e.persisted) {
      setRemUnit()
    }
  })

  // detect 0.5px supports
  if (dpr >= 2) {
    var fakeBody = document.createElement('body')
    var testElement = document.createElement('div')
    testElement.style.border = '.5px solid transparent'
    fakeBody.appendChild(testElement)
    docEl.appendChild(fakeBody)
    if (testElement.offsetHeight === 1) {
      docEl.classList.add('hairlines')
    }
    docEl.removeChild(fakeBody)
  }
}(window, document))
```



代码的作用就是动态修改html的font-size属性为vw的1/10(例：如果clientWidth为375的iphone6、对应的font-size为37.5)，如果dpr>=2在在html上设置class=hairlines，harilines{border-width:0.5px}。

在使用postcss-pxtorem的插件的情况下，只要按设计稿对应的宽高使用px来写就可以了

