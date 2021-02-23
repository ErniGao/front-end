## JQuery简介

- 为了简化 JavaScript 的开发, 一些 JavsScript 库诞生了. JavaScript 库封装了很多预定义的对象和实用函数。能帮助使用者建立有高难度交互的 Web2.0 特性的富客户端页面, 并且兼容各大浏览器

- JQuery就是当前流行的JavaScript库之一

## JQuery对象和DOM对象的关系

- jQuery 对象就是通过 jQuery($()) 包装 DOM 对象后产生的对象，jQuery对象是jQuery独有的，如果一个对象是 jQuery 对象, 那么它就可以使用 jQuery 里的方法
- jQuery对象无法使用DOM对象的任何方法,同样DOM对象也不能使用 jQuery里的任何方法
- 如果获取的是jQuery对象，那么要在变量前面加上$
  - var $ variable = jQuery 对象
  - var variable = DOM对象

