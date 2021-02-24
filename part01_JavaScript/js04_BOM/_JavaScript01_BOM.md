## BOM简介

- BOM （browser object model），浏览器对象模型，BOM可以使我们通过JS来操作浏览器，在BOM中为我们提供了一组对象，用来完成对浏览器的操作
- BOM对象
  1. Window
     - 代表的是整个浏览器的窗口，同时window也是网页中的全局对象
  2. Navigator
     - 代表的当前浏览器的信息，通过该对象可以来识别不同的浏览器
  3. Location
     - 代表当前浏览器的地址栏信息，通过Location可以获取地址栏信息，或者操作浏览器跳转页面
  4. History
     - 代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记
     - 由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器向前或向后翻页, 而且该操作只在当次访问时有效
  5. Screen
     - 代表用户的屏幕的信息，通过该对象可以获取到用户的显示器的相关的信息
- 这些BOM对象在浏览器中都是作为window对象的属性保存的，可以通过window对象来使用，也可以直接使用

## Navigator

- navigator.appName: 多数结果显示都是Netscape
  
- 由于历史原因，Navigator对象中的大部分属性都已经不能帮助我们识别浏览器了
  
- 一般我们只会使用userAgent来判断浏览器的信息

  - userAgent是一个字符串，这个字符串中包含有用来描述浏览器信息的内容，不同的浏览器会有不同的userAgent， 使用这个属性可以判断是什么浏览器

    - 火狐的userAgent： Mozilla/5.0 (Windows NT 6.1; WOW64; rv:50.0) Gecko/20100101 Firefox/50.0
    - Chrome的userAgent：Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.82 Safari/537.36
    - IE8：Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)
    - IE9： Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)
    - IE10：Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)
    - IE11：Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; rv:11.0) like Gecko
      - 在IE11中已经将微软和IE相关的标识都已经去除了，所以我们基本已经不能通过UserAgent来识别一个浏览器是否是IE了，但是可以通过一些其他ie特有的属性来判断ie浏览器：例如ActiveXObject （但是经常用这个属性来判断是否是ie浏览器，所以这个属性在ie11中不让转成布尔值，需要使用"ActiveXObject" in window来进行判断）

    ```javascript
    var ua = navigator.userAgent;
    console.log(ua);
    if(/firefox/i.test(ua)){  //使用正则表达式进行判断
        alert("你是火狐！！！");
    }else if(/chrome/i.test(ua)){
        alert("你是Chrome");
    }else if(/msie/i.test(ua)){
        alert("你是IE浏览器~~~");
    }else if("ActiveXObject" in window){  //in用来检查一个对象中是否包含一个属性
        alert("你是IE11，枪毙了你~~~");
    }
    ```

## History

- 对象可以用来操作浏览器向前或向后翻页
- history的属性
  1. history.length：可以获取到当成访问的链接数量 （浏览器如果重新打开关闭之前访问的记录就没有了，就会重新计数）
- history的方法：
  1. history.back(): 可以用来回退到上一个页面，作用和浏览器的回退按钮一样
  2. history.forward(): 可以跳转下一个页面，作用和浏览器的前进按钮一样
  3. history.go(): 可以用来跳转到指定的页面
     - 它需要一个整数作为参数:
       - 1:表示向前跳转一个页面 相当于forward()
       - 2:表示向前跳转两个页面
       - -1:表示向后跳转一个页面
       - -2:表示向后跳转两个页面

## Location

- 该对象中封装了浏览器的地址栏的信息，如果直接打印location，则可以获取到地址栏的信息（当前页面的完整路径）

- 如果直接将location属性修改为一个完整的路径，或相对路径，则我们页面会自动跳转到该路径，并且会生成相应的历史记录

  ```
  location = "http://www.baidu.com";
  location = "01.BOM.html";
  ```

- location的方法：

  1. location.assign(): 用来跳转到其他的页面，作用和直接修改location一样

     ```
     location.assign("http://www.baidu.com");
     ```

  2. location.reload(): 用于重新加载当前页面，作用和刷新按钮一样

     - 如果在方法中传递一个true，作为参数，则会强制清空缓存刷新页面，相当于ctl + f5的作用

       ```
       location.reload(true);
       ```

  3. location.replace(): 可以使用一个新的页面**替换**当前页面，调用完毕也会跳转页面

     - 不会生成历史记录，不能使用回退按钮回退

       ```
       location.replace("01.BOM.html");
       ```

## Window

- window对象的方法 (alert, confirm, prompt都是window对象的方法）：

  1. setInterval()： 定时调用

     - JS的程序的执行速度是非常非常快的，如果希望一段程序，可以每间隔一段时间执行一次，可以使用定时调用
     - setInterval()可以将一个函数，每隔一段时间执行一次
     - 参数:
       1. 回调函数，该函数会每隔一段时间被调用一次
       2. 每次调用间隔的时间，单位是毫秒
     - 返回值: 返回一个Number类型的数据, 这个数字用来作为定时器的唯一标识 (页面中打开一个定时器就这个数字就是1，打开两个就是1和2)
   - 通常每个对象都应该有自己的定时器，使用obj.timer来绑定setInterval函数
  
2. clearInterval()可以用来关闭一个定时器，方法中需要一个定时器的标识作为参数，这样将关闭标识对应的定时器
  
     - clearInterval()可以接收任意参数，如果参数是一个有效的定时器的标识，则停止对应的定时器，如果参数不是一个有效的标识，则什么也不做
     
     ```javascript
     var num = 1;			
     var timer = setInterval(function(){
     	count.innerHTML = num++;
     	if(num == 11){
     		//关闭定时器,这个不能写到setInterval的外面，否则setInterval中的内容可能还没执行完定时器就被关闭了
             //这个方法用于设置关闭，当满足一定条件时关闭定时器
     		clearInterval(timer);
   	}
  },1000);
     ```
     
  
  3. setTimeout：
  
     - 延时调用一个函数不马上执行，而是隔一段时间以后在执行，而且只会执行一次
     - 延时调用和定时调用的区别，定时调用会执行多次，而延时调用只会执行一次，延时调用和定时调用实际上是可以互相代替的，在开发中可以根据自己需要去选择
  
  4. clearTimeout : 关闭延时
  
     - 使用clearTimeout()来关闭一个延时调用
  
     ```
     var timer = setTimeout(function(){
     	console.log(num++);
     },3000);
     
     //关闭延时调用
     clearTimeout(timer);
     ```
  
     

