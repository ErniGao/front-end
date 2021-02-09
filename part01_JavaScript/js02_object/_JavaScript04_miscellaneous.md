## call()和apply()

- 这两个方法都是函数对象的方法，需要通过函数对象来调用

- 当对函数调用call()和apply()都会调用函数执行

  ```javascript
  function func(){
  	alert("我是func函数");
  }
  //前两个和第三个效果是一样的
  func.apply();
  func.call();
  func();
  ```

- 在调用call()和apply()时可以将一个对象指定为第一个参数, 此时这个对象将会成为函数执行时的this。

  ```javascript
  function func1(){
  	alert(this.name);
  }
  
  var obj = {name:"obj"};
  var obj2 = {name:"obj2"};
  func1.apply(obj);
  func1.apply(obj2);
  ```

- 参数传递的是哪个对象，执行时方法中传递的this就是这个对象，与是哪个对象调用无关

  ```javascript
  var obj = {
  	name:"obj",
  	sayName:function(){
  		alert(this.name);
  	}
  };
  var obj2 = {name:"obj2"};
  obj.sayName();  //会弹出obj
  //参数是谁，调用的这个函数的this就是谁，无论是那个对象调用的
  obj.sayName.apply(obj2);  //会弹出obj2
  ```

  

