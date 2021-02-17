## DOM

- DOM，全称Document Object Model文档对象模型

- S中通过DOM来对HTML文档进行操作。只要理解了DOM就可以随心所欲的操作WEB页面 (通过JS可以操作网页)

- Document （文档）：文档表示的就是整个的HTML网页文档 （一个HTML页面就是一个文档）

- Object（对象）：对象表示将网页中的每一个部分都转换为了一个对象 （一个文档中有标签，标签中属性，属性中还有文本，对象就是将网页中每个东西都转换成对象）

- Model（模型）：使用模型来表示对象之间的关系，这样方便我们获取对象 

- 节点（Node）：是构成我们网页的最基本的组成部分，网页中的每一个部分都可以称为是一个节点。

  - 节点分为不同的类型，节点的类型不同（是不同的对象），属性和方法也都不同

    1. 文档节点：整个HTML文档
    2. 元素节点：HTML文档中的HTML标签
    3. 属性节点：元素的属性
    4. 文本节点：HTML标签中的文本内容

  - 节点的属性

    - 通过nodeType可以判断节点类型
    - 节点值使用最多的就是文本节点的文本内容

    |          | nodeName | nodeType | nodeValue |
    | -------- | -------- | -------- | --------- |
    | 文档节点 | #documen | 9        | null      |
    | 元素节点 | 标签名   | 1        | null      |
    | 属性节点 | 属性名   | 2        | 属性值    |
    | 文本节点 | #text    | 3        | 文本内容  |

## 事件

- 事件就是文档或浏览器窗口中发生的一些特定的交互瞬间 （用户和浏览器交互的行为），JavaScript 与HTML 之间的交互是通过事件实现的
- 我们可以在事件对应的属性中设置一些js代码，这样当事件被触发时，这些代码就会执行
  - 这种方式结构和行为耦合，不方便维护，不推荐使用
- 我们也可以为对应的事件绑定处理函数的形式来响应事件（将事件写到script标签中），这样当事件被触发时，其对应的函数会被调用。为单击事件绑定的函数称为单击响应函数
- 在事件的响应函数中，响应函数是给谁绑定的this就是谁

## 文档的加载

- 浏览器在加载一个页面时，是按照至上而下的顺序加载的，读取一行就运行一行，如果将script标签写到页面的上面，在代码执行时，页面还没加载。将我们的js代码编写到下部，就是为了可以在页面加载以后再执行js代码

- onload事件：会在整个页面加载完成之后才触发，可以为window绑定onload事件
  - 为window绑定onload事件，该事件对应的响应函数将会在页面加载完成之后执行，这样可以确保我们的代码执行时，所有的DOM对象已经加载完毕了，不会出现获取不到DOM对象的问题
  - 通常会将js代码写在上面的onload 方法中，方便管理
  
- 按钮点击事件，绑定单击响应函数

  ```javascript
  /*
  * 定义一个函数，专门用来为指定元素绑定单击响应函数
  * 	参数：
  * 		idStr 要绑定单击响应函数的对象的id属性值
  * 		fun 事件的回调函数，当单击元素时，该函数将会被触发
  */
  function myClick(idStr , fun){
  	var btn = document.getElementById(idStr);
  	btn.onclick = fun;
  }
  ```

  

## dom查询

- 获取元素节点
  - **通过document对象调**用：
    1. getElementById()： 通过id属性获取**一个**元素节点对象

    2. getElementsByTagName(): 通过**标签名**获取**一组**元素节点对象
       
       - 这个方法会返回一个**类数组对象**，所有查询到的元素都会封装到对象中， 即使查询到的元素只有一个，也会封装到数组中返回
       
       - 如果要使用这个方法获取body标签需要使用：var body = document.getElementsByTagName("body")[0]; 因为直接使用getElementsByTagName获取的是一个类数组对象，但是一个html文档中只有一个body标签，所以可以直接使用索引0
       
         - document中有一个属性body，它保存的就是body的引用, 可以直接用这种方式获取body
       
           ```javascript
           var body = document.body;
           ```
       
    3. getElementsByName(): 通过name属性获取**一组**元素节点对象 （一般是用来获取表单对象的）
       - innerHTML用于获取元素内部的HTML代码，但是对于自结束标签，是没有内部的HTML，这个属性没有意义
       - innerText和innerHTML类型，不同的是它会自动将html去除
       - 直接使用元素.属性名可以获取元素的属性，例如：元素.id 元素.name 元素.value， 但是class属性需要使用元素.className来读取不能使用元素.class。因为class是js中的保留字，不能直接作为属性名
         - 文本框的value属性值，就是文本框中填写的内容
       
    4. 获取html根标签：document.documentElement

    5. 获取页面中所有的元素：document.all，但是这个方法直接打印的结果是undefined，只有遍历时候才会看到里面的元素

       ```javascript
       var all = document.all;
       for (var i=0; i<all.length;i++){
       	console.log(all[i]);
       }
       //document.all方法等同于document.getElementsByTagName("*")
       ```

    6. 根据元素的class属性只查询一组元素节点对象，但是该方法不支持ie8以下的浏览器

       ```javascript
       var box1 = document.getElementsByClassName("box1");
       ```

    7. 根据一个css选择器来查询一个元素节点对象，需要一个选择器的字符串作为参数，可以使用这个方法根据元素的class属性查询元素节点对象。但是这个方法查询只会返回唯一一个元素，如果满足条件的元素有多个，那么它只会返回第一个

       ```javascript
       document.querySelector(".box1 div");
       ```

    8. document.querySelectorAll(), 该方法和querySelector()用法类似，不同的是它会将符合条件的元素封装到一个数组中返回，即使符合条件的元素只有一个，它也会返回一个数组

- 获取元素的子节点 
  
  - **通过具体的元素节点调用**：
    1. getElementsByTagName(): 返回当前节点的指定标签名后代节点
    2. childNodes (这个是属性)：表示当前节点的所有子节点
       - 会获取包括文本节点在内的所有节点，根据DOM标签标签间空白也会当成文本节点，但是在IE8及以下的浏览器中，不会将空白文本当成子节点
       - 元素还有一个children属性（元素.children) 可以获取当前元素的所有子元素，这样获取到的全部是元素，不会获取到空白文本
    3. firstChild (这个是属性)：表示当前节点的第一个字节点（包括空白文本节点）
       - firstElementChild获取当前元素的第一个子元素 （不建议使用，因为对于ie浏览器只支持9以上的）
    4. lastChild(这个是属性)：表示当前节点的最后一个子节点
  
- 获取元素父节点和兄弟节点
  - 通过具体的节点调用
    1. parentNode：属性，表示当前节点的父节点
    2. previousSibling：属性，表示当前节点的前一个兄弟节点 （会获取到空白文本）
       - previousElementSibling获取前一个兄弟元素，IE8及以下不支持
    3. nextSibling: 属性，表示当前节点的后一个兄弟节点

- 元素属性

  - input的checkbox

    1. 通过多选框的checked属性可以来获取或设置多选框的选中状态

       ```javascript
       var items = document.getElementsByName("items");
       for(var i=0 ; i<items.length ; i++){
         //通过多选框的checked属性可以来获取或设置多选框的选中状态
         //alert(items[i].checked);
       
         //设置四个多选框变成选中状态
         items[i].checked = true;
       }
       ```

- 