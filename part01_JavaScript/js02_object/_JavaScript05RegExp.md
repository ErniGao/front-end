## 正则表达式

- 正则表达式可以用户定义一些字符串的规则。计算机可以根据正则表达式来检查一个字符串是否符合规则，或将字符串中符合规则的内容提取出来

- 创建正则表达式对象

  - 使用构造函数

    - 语法： var 变量名 = new RegExp("正则表达式"，"匹配模式")；

    - 匹配模式可以是i （忽略大小写），或者g （全局匹配模式）
    - 构造函数中的正则表达式可以传递一个变量，不一定要是单一的一个字符串了

  - 使用字面量

    - var 变量 = /正则表达式/匹配模式

- 使用test()方法可以使用检查一个字符串是否符合正则表达式的规则，如果符合则返回true，否则返回false

## 正则表达式语法

- 使用|表示或者的意思

- 使用[ ]表示或的关系

  - [a-z] 表示任意的小写字母
  - [A-Z] 表示任意的大写字母
  - [A-z] 表示任意字母
  - a[bde]c: 表示前面是a，最后是c，中间bde任选其一
  - \[^ab]: 表示除了a和b
  - \[0-9]:   表示任意的数字
  - \[^0-9]: 表示除了数字

- 量词：通过量词可以设置一个内容出现的次数

  - 量词只对它前边的一个内容起作用，如果想对前边的多个内容同时起作用要使用（）将这些内容括起来

  - {n} 正好出现n此
  - {m,n}: 表示出现m-n次
  - {m,}:  出现m次以上
  - \+ 表示至少出现一次，相当于{1,}
  - \* 表示0或多个，相当于{0,}
  - ? 表示0个或1个，相当于{0,1}

- ^a: 检查是否以a开头 （如果将这个表达式放在大括号中表示除了a）

- a$：表示以a结尾

- 如果正则表达式中同时使用^和$则要求字符串必须**完全符合正则表达式** (不能再额外添加内容)

- . (点) 表示任意字符

- 如果要检查一个字符串中是否含有点，需要使用\作为转义字符，要检查字符串中是否有\要使用两个\ (在字符串中也需要使用两个斜杠来代表一个斜杠)

  - 使用构造函数时，由于它的参数是字符串，而\是字符串中的转义字符，如果要使用斜杠，需要使用两个斜杠来代替 （构造函数中如果需要使用一个斜杠就要写两个斜杠）

  ```javascript
  var reg = new RegExp("\\.");   \\表示匹配点
  ```

  

- 特殊意义的字符：

  - \w: 任意字母数字，下划线，相当于 [A-z0-9_]

  - \W：除了字母数字，下划线， 相当于 \[^A-z0-9_]

  - \s：空格

  - \S：除了空格

  - \b：单词边界, 检查字符串中是否具备独立的单词

    ```javascript
    var reg17 = /\bchild\b/;
    console.log(reg17.test("hello children"));
    ```

  - \B：除了单词边界  

  - \d: 任意数字，相当于 [0-9]

  - \D: 除了数字, 相当于 \[^0-9]

## 和正则表达式相关的字符串方法

- search()：搜索字符串中是否含有指定内容

  - 如果搜素到指定内容则会返回第一次出现的索引，如果没有搜索到则返回-1
  - 它可以接收一个正则表达式作为参数，然后会根据正则表达式去检索字符串
  - search只会查找第一个，即使设置全局匹配也没有用

- split(): 可以将字符串拆分成数组

  - 方法中可以传递一个正则表达式作为参数，这样方法可以根据正则表达式去拆分字符串
  - 这个方法即使不指定全局匹配也会全部拆分

- match(): 可以根据正则表达式，从一个字符串中将符合条件的内容提取出来

  - 默认情况下只会找到第一个符合要求的内容，找到之后就停止检索
  - 我们可以设置正则表达式为全局匹配模式，这样就会匹配到所有的内容
  - 可以为一个正则表达式设置多个匹配模式且顺序无所谓
  - match会将匹配到的内容封装到一个数组中返回，即使只查询到一个结果也是使用数组返回

- replace()：将字符串中指定的内容替换为新的内容

  - 需要两个参数，第一个是被替换的内容 （可以使用正则表达式作为参数），第二个是新的内容

  - 默认只会替换第一个，但是可以使用正则表达式的全局模式

    ```javascript
    //使用空串替换空格来去除空格
    var str = "   hello   ";
    str = str.replace(/\s/g,"");
    console.log(str)
    //去除开头的空格
    str = str.replace(/^\s*/g,"");
    //去除结尾的空格
    str = str.replace(/\s*$/g,"");
    //去除开头和结尾的空格
    str = str.replace(/^\s*|\s*$/g,"")
    ```

    

