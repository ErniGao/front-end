## js编写位置

- js代码需要全部编写到**script标签中**

  ```
  <script type ="text/javascript"></script>
  ```

  - type属性写不写都行，不写默认值也是javascrip

  - js也是从上到下一行一行执行

- 写在**标签的属性**中

  1. 可以将js代码编写到标签的onclick属性中，当我们点击按钮时，js代码才会执行，每点一次执行一次

     ```
     <button onclick="alert('讨厌,你点我干嘛');">点我一下</button>
     ```

  2. 可以将js代码写在超链接的href属性中，这样当点击超链接时，会执行js代码

     - 这种方式超链接不会跳转，只会出现一个弹

       ```
       <a href="javascript:alert('让你点你就点！！');">你也点我一下</a>
       ```

     - 如果js内容为空，点超链接不会有任何反应

       ```
       <a href="javascript:;">你也点我一下</a>
       ```

  - 虽然可以写在标签的属性中，但是他们属于结构与行为耦合，不方便维护，不推荐使用

- 可以写在外部的js文件中

  - 通过script标签引入

  - 写到外部文件中可以在不同的页面中同时引用，也可以利用到浏览器的缓存机制

  - 推荐使用的方

    ```
    <script type="text/javascript" src="01_js_output.js"></script>
    ```

- script标签一旦用于引入外部文件了，就不能在标签内写内部代码了，即使编写了浏览器也会忽略。如果需要则可以在创建一个新的script标签用于编写内部代码

## 常用输出功能

#### 1. 弹出警告框

- alter("这是我的第一行JS代码")；

#### 2. 让计算机在页面中输出内容

- document.write("hello world");
- document.write()可以向body中输出一个内容
- 在浏览器中按f12会看见document.write()的内容会显示在body里

#### 3. 在控制台中输出内容

- console.log("会在控制台输出");
- console.log()的作用是向控制台输出一个内容
- 在浏览器中按f12，点击console会看见使用console.log()输出的内容





