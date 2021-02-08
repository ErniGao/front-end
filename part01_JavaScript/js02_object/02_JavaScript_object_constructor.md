## this

- 浏览器（解析器）在调用函数时，每次都会向函数内部传递仅一个隐含的参数，这个隐含的参数就是this

- this指向的是一个对象，这个对象我们称为函数执行的上下文对象

- 根据函数的**调用方式**的不同 （与创建方式无关），this会指向不同的对象

  - 以函数的形式调用时，this永远都是window
  - 以方法的形式调用时，this就是调用方法的对象

- this可以根据调用者的不同输出不同的值

  ```javascript
  var name = "全局";
  function func(){
      console.log(this.name);
  }
  var obj1 = {
      name:"孙悟空",
      sayName:func
  };
  var obj2 = {
      name: "沙和尚",
      sayName:func
  };
  obj1.sayName();  //孙悟空
  obj2.sayName();  //沙和尚
  func(); //全局
  ```

## 使用工厂方法创建对象

- 用来减少创建对象的过程中出现的大量的重复性的代码

- 只需要把属性传进去，直接可以返回对象

  ```javascript
  function createPerson(name,age,gender){
  	//创建一个新的对象,这个obj是局部的
      var obj = new Object();
      //向对象中添加属性
      obj.name = name;
      obj.age = age;
      obj.gender = gender;
      obj.sayName = function(){
      	alert(this.name);
      };
      //将新的对象返回
      return obj;
  }
  	var obj4 = createPerson("猪八戒",28,"男");
      var obj5 = createPerson("白骨精",18, "女");
      var obj6 = createPerson("蜘蛛精",16,"女");
      console.log(obj4.name);
      console.log(obj5.name);
      console.log(obj6.name);
  ```

- 使用工厂方法创建的对象，使用的构造函数都是Object，所以创建的对象都是Object这个类型，这就导致我们无法区分出多种不同类型的对象

## 构造函数

- 希望创建对象的时候可以区分对象的类型

- 创建一个构造函数，专门用来创建指定类型的对象

- 构造函数就是一个普通的函数，创建方式和普通函数没有区别，不同的是构造函数习惯上首字母大写。构造函数和普通函数的区别就是调用方式的不同，普通函数是直接调用，而构造函数需要使用new关键字来调用

  ```javascript
  function Person(){
      //构造函数中使用this来引用新建的对象
  	this.name = name;
      this.age = age;
      this.gender = gender;
      this.sayName = function(){
      	alert(this);
      };
  }
  //将构造函数当作普通函数来调用
  //结果就是这个函数的返回值，而这个函数没有返回值，结果为undefined
  var per = Person();
  console.log(per);  //undefined
  //当作构造函数来调用
  //函数没写返回值，但是得到的是一个对象
  var per1 = new Person();
  console.log(per1);  //object
  ```

- 构造函数的执行流程

  1. 立刻创建一个新的对象 （堆内存中开辟新空间创建对象）
  2. 将新建的对象设置为函数中的this （当函数以构造函数形式调用时，this就是新创建的对象）。因此，在构造函数中可以使用this来引用新创建的对象
  3. 逐行执行函数中的代码
  4. 将新建的对象作为返回值返回

- 使用同一个构造函数创建的对象，称为一类对象，也将一个构造函数称为一个类

- instanceof 可以检查一个对象是否是一个类的实例（通过这个类的构造函数创建的实例）

  - 语法： 对象 instanceof 构造函数

    ```
    console.log(per instanceof Person);
    ```

- 