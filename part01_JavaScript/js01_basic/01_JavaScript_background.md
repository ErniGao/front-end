# JavaScript简介

#### 起源

- JavaScript诞生于1995年，它的出现主要是用于处理网页中的前端验证，如用户名的长度，密码的长度，邮箱的格式 （当时网速比较慢，将这些验证放在服务器去验证会非常慢，需要浏览器直接做检查，这样几乎不需要花费到浏览器一去一回的请求时间）
- 现在JavaScript已经不局限于做前端验证，几乎所有的动态效果都是用JavaScript完成的

#### ECMAScript

- ECMAScript是一个标准，而这个标准需要由各个厂商去实现
- 不同的浏览器厂商对该标准会有不同的实现 （不同的浏览器使用的引擎是不同的）
  1. FireFox：SpiderMonkey
  2. Internet Explorer：JScript/Chakra
  3. Safari：JavaScriptCore
  4. Chrome：v8 （JS中最快的引擎）
  5. Carakan：Carakan
- 一个完整的JavaScript实现应该由以下三个部分构成: ECMAScript，DOM （文档对象模型，提供了一组对象，让我们可以去操作我们的网页，如何通过js去操作网页）， BOM（浏览器对象模型，提供一组对象可以去操作浏览器，如何通过js去操作浏览器）

#### JS特点

- 解释型语言 （不用编译，写完直接运行）
- 类似于 C 和 Java 的语法结构
- 动态语言
- 基于原型的面向对象

