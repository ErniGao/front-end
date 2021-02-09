## this

- 浏览器（解析器）在调用函数时，每次都会向函数内部传递仅一个隐含的参数，这个隐含的参数就是this

- this指向的是一个对象，这个对象我们称为函数执行的上下文对象

- 根据函数的**调用方式**的不同 （与创建方式无关），this会指向不同的对象

  - 以函数的形式调用时，this永远都是window
  - 以方法的形式调用时，this就是调用方法的对象
  - 以构造函数的形式调用时，this就是新创建的那个对象

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

- 构造函数的执行流程 （只有第三步的代码是我们写的，剩下的全部是浏览器做的）

  1. 立刻创建一个新的对象 （堆内存中开辟新空间创建对象）
  2. 将新建的对象设置为函数中的this （当函数以构造函数形式调用时，this就是新创建的对象）。因此，在构造函数中可以使用this来引用新创建的对象
  3. 逐行执行函数中的代码
  4. 将新建的对象作为返回值返回

- 使用同一个构造函数创建的对象，称为一类对象，也将一个构造函数称为一个类

- instanceof 可以检查一个对象是否是一个类的实例（通过这个类的构造函数创建的实例）

  - 语法： 对象 instanceof 构造函数

  - 所有的对象都是Object的后代，所以任何对象和Object做instanceof检查时都会返回true

    ```
    console.log(per instanceof Person);
    ```


- 我们将方法写在构造函数内部，构造函数每执行一次就会创建一个新的方法，而这些方法都是一样的，这是没有必要的，我们可以使所有对象共享同一个方法。解决方法：将方法定义到全局作用域中

  ```javascript
  function func(){
    alert(this.name);
  }
  function Person(name,age,gender){
  	this.name = name;
    this.age = age;
    this.gender = gender;
    this.sayName = func;
  }
  var per2 = new Person("孙悟空",18,"男");
  var per3 = new Person("猪八戒",18,"男");
  console.log(per2.sayName == per3.sayName); //true
  ```

## 原型对象

- 将函数定义在全局作用域，污染了全局作用域的命名空间，而且定义在全局作用域中也很不安全 （可能会有函数名相同被覆盖）。为了解决这个问题，我们可以使用原型
- 我们所创建的每个函数，解析器都会向函数中添加一个属性prototype。这个属性对应着一个对象，这个对象就是我们所谓的原型对象（这个属性指向原型对象）。如果函数作为普通函数调用，prototype没有任何作用；如果函数以构造函数形式调用时 （使用new），它所创建的对象中都会有一个隐含的属性，指向该构造函数的原型对象，这个属性通常是不允许访问的，但是浏览器給我们提供了\_\_proto_\_的方式来让我们访问该属性

- 原型对象就相当于一个公共的区域，所有同一个类的实例都可以访问到原型对象，我们可以将对象中共有的内容统一设置到原型对象中。当我们访问对象的一个属性或者方法时，会现在对象的自身中寻找，如果有则直接使用，如果没有则会去原型对象中寻找。

- 我们创建构造函数时，可以将这些对象共有的属性和方法统一添加到构造函数的原型对象中，这样不用分别为每一个对象添加，也不会影响到全局作用域，就可以使每个对象都具有这些属性和方法了

- 使用in检查对象中是否含有某个属性时，如果对象中没有，但是原型中有也会返回true。如果要检查mc自己是否有的属性，而不是原型中的属性要使用hasOwnProperty() 

  ```javascript
  function MyClass(){
      
  }
  //向原型中添加属性
  MyClass.prototype.name = "我是原型中的名字";
  var mc = new MyClass();
  mc.age = 18;
  console.log("name" in mc);  //true
  console.log(mc.hasOwnProperty("name")); //false
  console.log(mc.hasOwnProperty("age")); //true
  ```

- 自己没有添加但是有的方法都在原型对象中

- 原型对象本身也是对象，它自身也有一个\_\_proto\_\_属性并且它也有原型，当我们使用一个对象的属性或方法时，会 先在自身中寻找，自身中如果有，则直接使用；如果没有则去原型对象中寻找，如果原型对象中有，则去使用；如果原型对象中也没有，则去原型的原型中寻找，直到找到object对象的原型。Object对象的原型没有原型，如果在Object中依然没找到，则返回undefined （原型链）

  - hasOwnProperty()这个方法就是在原型的原型中

  ```javascript
  console.log(mc.__proto__); //这个是原型对象
  console.log(mc.__proto__.__proto__); //这是原型的原型，也是个object
  console.log(mc.__proto__.__proto__.hasOwnProperty()); //true
  console.log(mc.__proto__.__proto__.__proto__); //null 
  ```

## toString

- 将任意数据类型转换为字符串可以调用toString()方法

- 当我们直接在页面中打印一个对象时，实际上时输出对象的toString()方法的返回值，toString方法在原型的原型中（object中），如果我们希望在输出对象时，按照我们的要求输出，我们可以为对象添加一个toString()方法，toString方法要的是字符串，我们必须返回的数据是字符串

- 如果希望所有的实例都按照我们写的方式，应该修改原型的toString方法

  ```javascript
  Person.prototype.toString = function(){
  	return "Person[name= " + this.name + ", age = " + this.age + "gender = " + this.gender + "] ";
  };
  ```

## 垃圾回收

- 程序运行过程中会产生垃圾，这些垃圾如果积攒过多，会导致程序运行速度过慢，所以我们需要一个垃圾回收机制，来处理程序运行过程中产生的垃圾
- 垃圾：当一个对象没有任何的变量或属性对它进行引用，此时我们将永远无法操作该对象，此时这种对象就是垃圾，这种对象过多会占用大量的内存空间，导致我们成勋运行变慢，所以这种垃圾必须进行清理
- 在JS中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁，我们不需要也不能进行垃圾回收操作，而且不同的浏览器处理的方式也不一样
- 但是浏览器是不能判断一个对象对你来说是否还有用，因此我们需要将我们不在使用的要回收的对象设置为null

