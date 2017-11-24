---
layout: post
title: "在Event Handler內不透過抓取DOM來獲取Input元素的value"
author: "Yumi Chen"
categories: Javascript
tags: [Javascript]
---
如下:

HTML(Pug)
```html
input(type=“text” oninput=“inputHandler(this.value)”)
// this會指向Input元素
```
Javascript
```javascript
function inputHandler(newVal){
console.log(newVal);
// or some other things you want to do with the value
}
```

※ 適用於onChange, onInput等監聽會被直接裝在要取值的元素上的事件監聽