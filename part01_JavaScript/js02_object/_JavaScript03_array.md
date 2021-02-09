## 简介

- 三种对象

  - 内建对象
  - 宿主对象
  - 自定义对象

- 数组（Array) 也是一个对象，和普通的对象功能类似，也是用来存储一些值的。不同的是普通对象是使用字符串作为属性名来操作属性，而数组是使用数字来作为索引操作元素的 （属性在对象中叫属性，在数组中叫元素）

- 索引：从0开始的整数

- 数组的作用：

  - 数组的存储性能比普通对象要好，在开发中我们经常使用数组来存储数据

- 数组的操作

  - 对于连续的数组（顺序添加的），使用length可以获取到数组的长度（元素的个数）；对于非连续的数组，使用length会获取到最大的索引加1，非连续的数组没有添加数据的位置也会空出来。因此，尽量不要创建非连续的数组
  - 使用length不仅可以获取数组长度，还可以设置数组的长度。如果修改的length大于原长度，则多出来的部分会空出来；如果修改的length小于原长度，则多出的元素会被删除 (因此我们可以通过修改length来删除一些元素)

  ```javascript
  //创建数组
  var arr = new Array();
  //向数组中添加对象：数组[索引] = 值;
  arr[0] = 10;
  arr[1] = 33;
  arr[2] = 22;
  //读取数组中的元素，如果读取不存在的索引不会报错，而是返回undefined
  console.log(arr[2]); //22
  console.log(arr[3]); //undefined
  //获取数组长度:使用length属性 数组.length
  console.log(arr.length);
  //修改数组的长度
  arr.length = 4;
  //向数组的最后一个位置添加元素
  //数组[数组.length] = 值；
  arr[arr.length] = 70;
  ```

- 使用字面量来创建数组

  - 语法： var arr = []

  - 使用字面量创建数组时，可以在创建时就指定数组中的元素

    ```javascript
    //创建了一个数组，同时向数组中添加6个元素
    var arr = [1,2,3,4,5,10];
    console.log(arr.length); //6
    ```

- 使用构造函数创建数组也可以直接向数组中添加元素，将要添加的元素作为构造函数的参数传递，元素之间使用逗号隔开

  ```javascript
  var arr = new Array(10,20,30);
  ```

- 当只传递一个整数时，使用字面量表示创建一个只有一个元素的数组，而使用构造函数表示创建这个整数的长度的数组

  ```javascript
  //创建一个数组，数组中只有一个元素10
  var arr4 = [10];
  // 创建一个长度为10的数组 （这种形式用的不多，JS中对数组长度没有限制）
  var arr5 = new Array(10);
  ```

- 数组中的元素可以是任意的数据类型， 也可以是对象

  ```javascript
  var arr6 = ["hello", 1, true, null, undefined];
  var obj = {name:"孙悟空"};
  arr6[arr6.length] = obj;
  //数组中放了三个对象
  var arr7 =[{name:"孙悟空"},{name:"猪八戒"},{name:"沙和尚"}]; 
  ```

- 数组中也可以存函数（函数也是对象）

  ```
  var arr8 = [function(){alert(1);},function(){alert(2);},function(){alert(3);}];
  //调用数组中的函数
  arr8[0]();
  ```

- 数组中也可以放数组

  ```
  //数组中也可以放数组，数组中的数组也可以放数组
  var arr9 = [[1,2,3],[4,5,6],[7,8,9]]; //二维数组
  ```

## 数组的方法

- push(): 向数组的末尾添加一个或多个元素，并返回新的长度

  - 可以将要添加的元素作为方法的参数传递，这样这些元素就会自动添加到数组的末尾

    ```javascript
    var arr10 = ["孙悟空","猪八戒","沙和尚"];
    //push可以添加一个或多个元素
    arr10.push("唐僧");
    var result = arr10.push("蜘蛛精","白骨精");
    console.log("result = " + result); //6 
    ```

- pop(): 删除并返回数组的最后一个元素

  ```javascript
  arr10.pop();
  console.log(arr10);
  var result1 = arr10.pop();
  console.log("result1 = " + result1);  //将删除的元素返回
  ```

- unshift(): 向数组的开头添加一个或多个元素并返回新的数组长度

  - 向前面插入元素以后，其他元素的索引会依次调整

    ```javascript
    arr10.unshift("牛魔王");
    console.log(arr10);  //牛魔王被添加到最前头
    ```

- shift(): 删除并返回数组的第一个元素

  ```javascript
  arr10.shift();
  console.log(arr10); //第一个元素牛魔王被删除了
  var result2 = arr10.shift();
  console.log("result2 = " + result2);  //将孙悟空删除并返回
  ```

- slice(): 从某个已有的数组返回选定的元素

  - 语法：arrayObject.slice(start, end), start 截取开始位置的索引（包括开始位置），end 截取结束位置的索引（不包括结束位置，end参数可以省略不写，默认截取从开始索引往后的所有元素）
  - 该方法不会改变原数组，而是将截取到的元素封装到一个新数组中返回
  - 索引可以传递一个负值，如果传递一个负值则从后往前计算，-1表示倒数第一个，-2表示倒数第二个以此类推

- splice: 删除元素并向数组添加新元素 （可以删除元素，替换元素和在指定位置添加新元素）

  - 使用splice会影响到原数组，会将指定元素从原数组中删除，并将被删除的元素作为返回值返回

  - splice方法也传递两个参数，第一个表示开始位置索引，第二个表示删除的数量，第三个及以后可以传递一些新的元素，这些元素将会自动插入到开始位置索引前边(替换删除掉的元素)

  - 如果第二个参数写0，表示不删除元素，但是在第一个参数所在的索引位置前边添加新元素

    ```javascript
    var arr13 = ["孙悟空","猪八戒","沙和尚","唐僧","白骨精"];
    var result6 = arr13.splice(0,2);
    console.log(arr13);  //["沙和尚","唐僧","白骨精"]
    console.log(result6); //["孙悟空","猪八戒"]
    
    var arr14 = ["孙悟空","猪八戒","沙和尚","唐僧","白骨精"];
    //第三个及以后的参数表示要向原数组中添加的元素 （替换了被删除的元素）
    var result7 = arr14.splice(0,1,"牛魔王","铁扇公主");
    console.log("arr14 = " + arr14);
    console.log("result7 = " + result7);
    ```

- concat():可以连接两个或多个数组，并将新的数组返回，该方法可以传多个数组或元

  ```javascript
  var arr16 = ["孙悟空","猪八戒","沙和尚"];
  var arr17 = ["白骨精","玉兔精","蜘蛛精"];
  var arr18 = ["二郎神","太上老君","玉皇大帝"];
  arr16.concat(arr17);
  //该方法不会对原数组产生影响
  console.log(arr16);
  console.log(arr17);
  var res = arr16.concat(arr17);
  console.log(res); //新数组
  //该方法可以传多个数组或元素
  var res1 = arr16.concat(arr17,arr18,"牛魔王","铁扇公主");
  console.log(res1);
  ```

- join(): 将数组的所有元素放到字符串中（将数组转换成字符串）

  ```javascript
  var arr16 = ["孙悟空","猪八戒","沙和尚"];
  var res2 = arr16.join();
  console.log(res2); //将所有元素转换为字符串，并用逗号连接
  console.log(typeof res2); //string
  //可以指定一个字符串作为参数，该参数为元素对连接符
  //如果不指定则默认使用逗号作为连接符
  var res3 = arr16.join("hello");
  console.log(res3);
  var res4 = arr16.join("-");
  console.log(res4);
  //如果不需要连接符默认使用空串
  var res5 = arr16.join("");
  console.log(res5);
  ```

- reverse():颠倒数组中元素的顺序，会影响原数组

  ```javascript
  var arr16 = ["孙悟空","猪八戒","沙和尚"];
  //reverse会直接修改原数组
  arr16.reverse();
  console.log(arr16);
  ```

- sort(): 对数组的元素进行排序，默认按照unicode的顺序排序，会影响原数组

  ```javascript
  var arr19 = ["b","d","e","a","c"];
  arr19.sort();
  console.log(arr19);
  //即使对于纯数字的数字，使用sort也会按照unicode编码排序
  //所以对数字进行排序时会得到错误的结果
  var arr20 = [3,1,2,11,4,5];
  arr20.sort();
  console.log(arr20);
  
  //我们可以自己来指定排序规则
  //我们可以在sort中添加一个回调函数，来指定排序规则
  //回调函数中需要定义两个形参，浏览器将会分别使用数组中的元素作为实参去调用回调函数
  //使用那个元素调用不确定，但是肯定的时数组中a一定在b的前边
  //浏览器会根据回调函数的返回值来决定元素的顺序，如果返回一个大于0的值，则元素会交换位置，如果返回小于0的值则元素位置不变
  //如果返回等于0的值，则认为两个元素相等，相等也不交换位置
  var arr21 = [3,1,2,11,4,5];
  arr21.sort(function(a,b){
  	return a-b;  //升序排列
  });
  arr21.sort(function(a,b){
    return b-a;  //降序排列
  })
  ```

## 数组遍历

- for循环遍历

  ```javascript
  var arr11 = ["孙悟空","猪八戒","沙和尚"];
  //for循环遍历
  for(var i=0; i<arr11.length;i++){
  	console.log(arr11[i]);
  }
  ```

- forEach遍历

  - 这个方法只支持ie8以上的浏览器，和其他浏览器

  - 需要一个函数作为参数，通常我们直接在括号中创建一个函数。像这种由我们创建，但是不由我们调用的函数称为回调函数

  - 数组中有几个元素函数就会执行几次，每次执行时，浏览器会将遍历到的元素以实参的形式传递进来，我们可以定义形参来读取这些内容

  - 浏览器会在回调函数中传递三个参数，第一个参数是当前正在遍历的元素，第二个参数是当前正在遍历的元素的索引，第三个参数是当前正在遍历的数组对象

    ```javascript
    //数组中有几个元素，函数就执行几次
    arr11.forEach(function(){
    	console.log("hello");
    });
    
    arr11.forEach(function(value,index,obj){
    	console.log("value = " + value);  //这个参数是浏览器传过来的，就是数组中的每个元素
        console.log("index = " +index);
        console.log("obj = " +obj);
    });
    ```

