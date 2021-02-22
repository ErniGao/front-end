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

- 事件对象

  - 当事件的响应函数被触发时，浏览器每次都会将一个**事件对象作为实参**传递进响应函数
  - 我们在写响应函数的时候，可以定义一个形参（event）来方便使用这个事件对象
  - 在事件对象中封装了当前事件相关的一切信息，比如：鼠标的坐标  键盘哪个按键被按下  鼠标滚轮滚动的方向。。。
  - 事件对象（event）的属性和方法：
    - 属性：
      1. clientX: 可以获取鼠标指针的水平坐标 （于获取鼠标在当前的可见窗口的坐标）
      2. clientY: 可以获取鼠标指针的垂直坐标
      3. pageX和pageY可以获取鼠标相对于当前页面的坐标，但是这个两个属性在IE8中不支持，所以如果需要兼容IE8，则不要使用
      4. target：event中的target表示的触发事件的对象 （谁触发的事件target就是谁）
    - 方法：
  - 在IE8中，响应函数被触发时，浏览器不会传递事件对象，在IE8及以下的浏览器中，是将事件对象作为window对象的属性保存的， event需要使用window.event获取

- 事件的冒泡：

  - 所谓的冒泡指的就是事件的**向上传导**，当后代元素上的事件被触发时，其祖先元素的**相同事件**也会被触发

  - 在开发中大部分情况冒泡都是有用的,如果不希望发生事件冒泡可以通过事件对象来取消冒泡 (所有浏览器都支持取消冒泡的属性)

    ```
    //可以将事件对象的cancelBubble设置为true，即可取消冒泡
    event.cancelBubble = true;
    ```

  - 事件委派：
    - 我们希望只绑定一次事件就可以应用到多个元素上，即使元素是后添加的也可以应用这个绑定事件，我们可以尝试将其绑定给元素的共同的祖先元素
    - 事件委派指将事件统一绑定给元素的共同的祖先元素，这样当后代元素上的事件触发时，会一直冒泡到祖先元素，从而通过祖先元素的响应函数来处理事件
    - 事件委派是利用了冒泡，通过委派可以减少事件绑定的次数，提高程序的性能
  - 事件传播：
    - 对于事件的传播网景公司和微软公司有不同的理解，微软公司认为事件应该是由内向外传播，也就是当事件触发时，应该先触发当前元素上的事件，然后再向当前元素的祖先元素上传播，也就说事件应该在冒泡阶段执行。
    - 网景公司认为事件应该是由外向内传播的，也就是当前事件触发时，应该先触发当前元素的最外层的祖先元素的事件，然后在向内传播给后代元素
    -  W3C综合了两个公司的方案，将事件传播分成了三个阶段
      1. 捕获阶段：在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件
      2. 目标阶段: 事件**捕获到**目标元素，捕获结束开始在目标元素上触发事件
      3. 冒泡阶段: 事件从目标元素向他的祖先元素传递，依次触发祖先元素上的事件 (从目标元素开始执行事件)
    - 如果希望在捕获阶段就触发事件，可以将addEventListener()的第三个参数设置为true，一般情况下我们不会希望在捕获阶段触发事件，所以这个参数一般都是false
    - IE8及以下的浏览器中没有捕获阶段，它只有冒泡阶段

- 事件绑定：

  - 对象.事件 = 函数 来绑定响应函数

    - 它只能同时为一个元素的一个事件绑定一个响应函数，同一个元素的一个事件只能触发一个响应函数，不能触发多个响应函数

  - addEventListener()

    - 可以为元素绑定响应函数

    - 需要的参数：

      1. 事件的字符串, 直接写事件名不要加on，例如onclick事件，直接写事件名click

      2. 调函数，当事件触发时该函数会被调用

      3. 是否在捕获阶段触发事件，需要一个布尔值，一般都传false

         ```javascript
         btn01.addEventListener("click",function(){
         alert(1);},false);
         ```

    - 可以同时为一个元素的相同事件同时绑定多个响应函数，这样当事件被触发时，响应函数将会按照函数的绑定顺序执行

    - this是绑定事件对象

    - 这个方法不支持IE8及以下的浏览器

  - attachEvent()

    - 在IE8中可以使用attachEvent()来绑定事件
    - 参数：
      1. 事件的字符串，要on
      2. 回调函数
    - 这个方法也可以同时为一个事件绑定多个处理函数，不同的是它是后绑定先执行，执行顺序和addEventListener()相反，但是通常我们为一个事件绑定多个函数是因为这些函数相对独立执行顺序不太重要，执行顺序如果很重要的，通常写在一个函数中
    - this是window，不是绑定事件对象

  - 自定义同时兼容不同浏览器的绑定事件

    - this是谁是由调用方式决定的，this是window说明底层是用函数的形式调用的，this是绑定对象说明底层是用方法的形式调用的。

    - 修改this的方法是使用call，向里面传递对象作为this： function.call(obj), 这个obj就是函数的this

      ```
      function bind(obj , eventStr , callback){
      	if(obj.addEventListener){
      	//大部分浏览器兼容的方式
      	obj.addEventListener(eventStr , callback , false);
      	}else{
      	/*
      	* this是谁由调用方式决定
      	* callback.call(obj)
      	*/
      	//IE8及以下
      	obj.attachEvent("on"+ eventStr , function(){
      	//在匿名函数中调用回调函数，
      	//浏览器调用的是这个匿名函数，在这个匿名函数中调用callback
      	callback.call(obj);});
      	}
      }
      ```

- 事件种类：

  1. onscroll事件

     - 该事件会在元素的滚动条滚动时触发 （通常用在用户需要阅读协议条款时，要求滚动条滚动到底才能执行下一步或者按其他按钮）

     - 检查垂直滚动条是否滚动到底： 

       ```
       info.scrollHeight - info.scrollTop == info.clientHeight
       ```

  2. onmousemove

     - 该事件将会在鼠标在元素中移动时被触发
     
  3. 拖拽事件：
  
     - 拖拽事件流程
       1. 当鼠标在被拖拽元素上按下时，开始拖拽  onmousedown，将事件绑定给要拖拽的元素
       2. 当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove，将事件绑定给document，如果绑定给被拖拽的元素，元素离开了位置事件就执行不了了。这个事件必须在onmousedown的响应函数里边绑定，不然鼠标移动元素就直接跟着移动了
       3. 当鼠标松开时，被拖拽元素固定在当前位置 onmouseup，将事件绑定给document,这样无论鼠标在哪里松开，上面是否还覆盖了其他元素都可以取消鼠标移动的事件，该事件用来取消document.onmousemove (document.onmousemove = null)。并且松开鼠标的事件只是拖拽事件的一部分，之后再发送松开鼠标的时候不希望还会触发这个事件，因此要将松开鼠标的事件设置为一次性的事件，document.onmouseup = null
     - 当我们拖拽一个网页中的内容时，浏览器会默认去搜索引擎中搜索内容，此时会导致拖拽功能的异常，这个是**浏览器提供的默认行为**，如果不希望发生这个行为，则可以通过return false来取消默认行为，但是这招对IE8不起作用
       - setCapture()是ie8中的一个方法，当调用一个元素的setCapture()方法以后，这个元素将会把下一次所有的鼠标按下相关的事件捕获到自身上 （点其他元素就像点这个设置完setCapture的元素一样，就会触发这个设置了的元素的点击事件）
     
  4. 滚轮事件
  
     - onmousewheel鼠标滚轮滚动的事件，会在滚轮滚动时触发
  
     - 火狐不支持该属性，在火狐中需要使用 DOMMouseScroll 来绑定滚动事件，该事件需要通过addEventListener()函数来绑定
  
     - event.wheelDelta 可以获取鼠标滚轮滚动的方向，向上滚 120 ，向下滚 -120，wheelDelta这个值我们不看大小，只看正负
  
       - wheelDelta这个属性火狐中不支持
       - 在火狐中使用event.detail来获取滚动的方向，向上滚 -3 ，向下滚 3，仍旧是看正负不关心大小
  
     - 当滚轮滚动时，如果浏览器有滚动条，滚动条会随之滚动，这是浏览器的默认行为，如果不希望发生，则可以取消默认行为，使用return false
  
     - 使用addEventListener()方法绑定响应函数，取消默认行为时不能使用return false，需要使用event来取消默认行为event.preventDefault(); 但是IE8不支持event.preventDefault();这个玩意，如果直接调用会报错，因此在调用这个方法之前需要先判断一下是否有preventDefault属性
  
       ```javascript
       event.preventDefault && event.preventDefault();
       ```
  
  5. 键盘事件
  
     - onkeydown： 按键被按下
  
       - 对于onkeydown来说如果一直按着某个按键不松手，则事件会一直触发，当onkeydown连续触发时，第一次和第二次之间会间隔稍微长一点，其他的会非常的快，这种设计是为了防止误操作的发生
  
     - onkeyup：按键被松开
  
       - onkeyup不会连续触发，松开一次就触发一次
  
     - 键盘事件一般都会绑定给一些**可以获取到焦点的对象**或者是document，键盘事件一般不会绑给div，因为无法选中div
  
       - 键盘事件的event对象具有的属性
  
         - 可以通过keyCode来获取按键的编码，通过它可以判断哪个按键被按下
  
           - KeyCode 中37，38，39，40 表示向左键，向上键，向右键，向下键
  
         - altKey，ctrlKey，shiftKey，这个三个用来判断alt ctrl 和 shift是否被按下，如果按下则返回true，否则返回false
  
           ```
           //判断y和ctrl是否同时被按下
           if(event.keyCode === 89 && event.ctrlKey){
           	console.log("ctrl和y都被按下了");
           }
           ```
  
     - 在文本框中输入内容，属于onkeydown的默认行为, 如果在onkeydown中取消了默认行为，则输入的内容，不会出现在文本框中

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
    
    5. children：表示获取父节点向下的所有子元素
    
       ```javascript
       var td = tr.children;
       ```
  
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


## DOM增删改

- appendChild(): 把新的子节点添加到指定节点

  - 向一个父节点中添加一个新的子节点

  - 用法：父节点.appendChild(子节点);

    ```javascript
    li.appendChild(gzText);
    ```

- removeChild()：删除子节点

  - 可以删除一个子节点

  - 语法：

    1. 父节点.removeChild(子节点); (需要先找到父节点才能删除子节点)

       ```
       city.removeChild(bj);
       ```

    2. 子节点.parentNode.removeChild(子节点); (通过子节点直接获取父元素来删除子节点，这种方式不需要获取父节点，可以直接删除)

       ```
       bj.parentNode.removeChild(bj);
       ```

- replaceChild()：替换子节点

  - 可以使用指定的子节点替换已有的子节点

  - 语法：父节点.replaceChild(新节点,旧节点);   (这个方法是父节点调用的)

    ```
    city.replaceChild(li , bj);
    ```

- insertBefore(): 在指定的子节点前插入新的子节点

  - 以在指定的子节点前插入新的子节点

  - 语法：父节点.insertBefore(新节点,旧节点); (这个方法是父节点调用的)

    ```javascript
    //创建一个广州
    var li = document.createElement("li");
    var gzText = document.createTextNode("广州");
    li.appendChild(gzText);
    
    //获取id为bj的节点
    var bj = document.getElementById("bj");
    
    //获取city
    var city = document.getElementById("city");
    city.insertBefore(li,bj);
    ```

- createElement(): 创建元素节点 （html的标签）

  - 可以用于创建一个元素节点对象

  - 它需要一个标签名作为参数，将会根据该标签名创建元素节点对象， 并将创建好的对象作为返回值返回

    ```javascript
    //document的方法，必须使用document来调用
    var li = document.createElement("li");
    ```

- createTextNode()：创建文本节点 （标签在网页中显示的文字内容）

  - 可以用来创建一个文本节点对象

  - 需要一个文本内容作为参数，将会根据该内容创建文本节点，并将新的节点返回

    ```javascript
    var gzText = document.createTextNode("广州");
    ```

- innerHTML： 获取标签内的**html代码**，获取到的是标签内的所有代码

  - 通过innerHTML修改的代码会直接在网页上生效，但是这种方式相当于将ul下面的所有li全部都删除再跟着新的li重新添加一遍，如果ul下的其他li已经绑定了事件就不能使用这种方式

    ```
    //向ul中添加一个li，使用字符串连接的方式
    city.innerHTML += "<li>广州</li>";
    ```

  - 通产会使用innerHTML和dom方法调用相结合的方式

    ```
    //创建一个li
    var li = document.createElement("li");
    //向li中设置文本
    li.innerHTML = "广州";
    //将li添加到city中
    city.appendChild(li);
    ```

## DOM 超链接

- 点击超链接以后，超链接会跳转页面，这是超链接的默认行为，如果不希望出现默认行为需要取消默认行为，要通过在响应函数的最后return false来取消默认行为。也可以在超链接的标签上写href = "javascript:;"
  - 如果a标签不添加href属性，不会显示出超链接的样子
- 响应函数中的this就是绑定事件的元素，因此如果给超链接绑定响应函数了，点击哪个超链接this就是谁

## window对象的其他方法

- confirm(): 显示带有一段消息以及确认按钮和取消按钮的对话框

  - 需要一个字符串作为参数，该字符串将会作为提示文字显示出来

  - 如果用户点击确认则会返回true，如果点击取消则返回false

    ```javascript
    var flag = confirm("确认删除"+name+"吗?");
    ```

- 注：

  1. 在向表格中新添加一行数据的时候，尽量往tbody里面添加，不要直接往table标签下添加。因为在设置样式的时候，如果使用tbody设置的样式，添加在table标签下的数据就无法应用使用tbody设置的样式

## DOM操作CSS

- 通过JS修改元素样式：

  - 语法：元素.style.样式名 = 样式值

  - 样式值需要是字符串

    ```javascript
    box1.style.width = "300px";
    box1.style.backgroundColor = "yellow";
    ```

  - 如果CSS的样式名中含有-，这种名称在JS中是不合法的比如background-color （因为-在JS中会认为是做减法），需要将这种样式名修改为驼峰命名法，去掉-，然后将-后的字母大写

  - 我们通过style属性设置的样式都是内联样式，而内联样式有较高的优先级，所以通过JS修改的样式往往会立即显示

  - 如果在样式中写了!important，则此时样式会有最高的优先级，即使通过JS也不能覆盖该样式，此时将会导致JS修改样式失效，所以尽量不要为样式添加!important

- 获取元素的内联样式

  1. 通过style属性设置和读取内联样式, 这种方式无法读取样式表中的样式

     - 语法：元素.style.样式名

       ```
       box1.style.width
       ```

  2. 获取元素的当前显示的样式

     - 语法：元素.currentStyle.样式名

     - 它可以用来读取当前元素**正在显示**的样式，如果当前元素没有设置该样式，则获取它的默认值

     - currentStyle只有IE浏览器支持，其他的浏览器都不支持。在其他浏览器中可以使用getComputedStyle()这个方法来获取元素当前的样式，这个方法是window的方法，可以直接使用

       - 需要两个参数，第一个：要获取样式的元素，第二个：可以传递一个伪元素，一般都传null

       - 该方法会返回一个对象，对象中封装了当前元素对应的样式。 可以通过对象.样式名来读取样式。如果获取的样式没有设置，则会获取到真实的值，而不是默认值，比如：没有设置width，它不会获取到auto，而是一个长度

         ```
         getComputedStyle(box1,null).width)
         ```

       - 该方法不支持IE8及以下的浏览器

       - 通过currentStyle和getComputedStyle()读取到的样式都是只读的，不能修改，如果要修改必须通过style属性

     - 为了兼容正常浏览器和ie8， 可以自己定义一个兼容两种样式的方法

       ```javascript
       /*
       * 定义一个函数，用来获取指定元素的当前的样式
       * 参数：
       * 		obj 要获取样式的元素
       * 		name 要获取的样式名
       */
       
       function getStyle(obj , name){
       
       	if(window.getComputedStyle){
       		//正常浏览器的方式，具有getComputedStyle()方法
               //判断条件中必须使用window，没有window是一个变量需要去作用域中寻找，加上window是window的一个属性，变量没找到会报错，而属性没找到返回undefined
               //getComputedStyle()这个方法返回的是对象，样式是这个对象的属性
       		return getComputedStyle(obj , null)[name];
       	}else{
       		//IE8的方式，没有getComputedStyle()方法
       		return obj.currentStyle[name];
       	}
       
           //直接使用三元表达式获取样式，如果有getComputedStyle就使用这个方法，如果没有就换currentStyle方法
       	//return window.getComputedStyle?getComputedStyle(obj , null)[name]:obj.currentStyle[name];
       
       }
       ```

- element.clientHeight: 返回元素可见高度， element.clientWidth: 返回元素可见宽度
  - 这两个属性可以获取元素的可见宽度和高度
  - 这些属性都是不带px的，返回都是一个数字，可以直接进行计算
  - 获取的元素宽度和高度会包括内容区和内边距，但是不包括边框
  - 这些属性都是只读的，不能修改，因为它是多个属性相加得到的值，如果修改无法确定要修改的是哪个属性。如果修改只能通过style来修改
  
- element.offsetHeight，element.offsetWidth

  - 获取元素的整个高度和宽度，包括内容区、内边距和边框

- element.offsetParent 定位父元素

  - 会获取到离当前元素最近的开启了定位的祖先元素 （只要position值不是static就是开启定位了）
  - 如果所有的祖先元素都没有开启定位，则返回body

- offsetLeft： 当前元素相对于其定位父元素的水平偏移量

- offsetTop： 当前元素相对于其定位父元素的垂直偏移量

- scrollWidth， scrollHeight

  - 可以获取元素**整个**滚动区域的宽度和高度

- scrollLeft，scrollTop

  - 可以获取水平、垂直滚动条滚动的距离

  - chrome认为浏览器的滚动条是body的，可以通过body.scrollTop来获取，火狐等浏览器认为浏览器的滚动条是html的

    ```javascript
    var st = document.body.scrollTop || document.documentElement.scrollTop;
    
    var sl = document.body.scrollLeft || document.documentElement.scrollLeft;
    ```

    

  