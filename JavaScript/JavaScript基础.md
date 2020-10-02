## JavaScript基础

### 一、三句话

#### 1.alert("你好！")

+ 效果：在页面上弹出一个提示框



#### 2.console.log

> 向浏览器的控制台中输出一句话

+ 作用：用来进行代码的调试



#### 3.prompt("")

> 弹出一个提示框，给用户输出信息



### 二、开发人员工具的使用

> 右键，检查元素，如果有错误在控制台右上角会显示红叉

+ 快捷键F12



### 三、简单数据类型

#### 1.string字符串

> 由字符组成的串，用双引号或者单引号

+ 字符转义
  + \n:换行
  + \t:缩进
  + \b:空格
  + \t:回车
  + \\\\:斜杠
  + \\':单引号
  + \\":双引号

+ 字符串的**不可变**

  + 不可变指的是字符串不可以改变，同一个字符串就指向同一个地址

    ```javascript
    var str = 'hello';	//假设这里的str指向的地址是0x00ff，存放在栈中
    str = str + 'itcast';	//这里会在栈重新开辟空间，存放字符串'helloitcast'，地址为0x00cc
    //并且此时的str的地址不再指向0xff，而是指向0xcc。0xff地址存放的依然是'hello'
    console.log(str);	
    ```

    



#### 2.number数值类型

> 整数，小数点，NaN

+ NaN:not a number
  + 作用：用来表示数值的一种不正常状态
  + 一般在计算错误的时候出现
  
+ isNaN():判断当前数据是否为非数字
  + 非数字：返回true
  + 数字：返回false

+ 浮点数的最高精度是17位小数，但进行算数计算时精度远远不如整数

  ```javascript
  var result = 0.1 + 0.2;	//结果是0.3000..004
  console.log(0.07*100);	//结果是7.000...001
  ```

  + **永远不要判断两个浮点数是否相等**



##### 加号+的作用

1. 两个字符串用+连接：连接两个字符串
2. 两个数值用+连接：加法运算符的作用
3. 一个是字符串一个是数值：连接作用



#### 3.boolen类型

> true 和 false



#### 4.undefined

> 如果一个变量声明了但是没有赋值，它的结果就是undefined

+ undefined在页面上不会报错



### 四、判断数据的类型

`typeof`

```javascript
var a = 100;
var b;
// 1.typeof 变量
// 2.typeof 直接量
// 3.typeof(直接量/变量)
console.log(typeof a);  
console.log(typeof "你好！");   
console.log(typeof(b));
```



 ### 五、变量

>  声明变量的关键字：`var`

+ 变量名的注意点
  1. 变量名智能用英文字母、数字、下划线以及$符号组成，并且数字不能放在名称开头
  2. 命名不能用JavaScript中的关键字和保留字
  3. 区分大小写
  4. 驼峰命名法



### 六、运算符

#### 1.算数运算符

1. 加 ：+
2. 减：-
3. 乘：*
4. 除：/
5. 取余/取模：%
6. 改变运算优先级：()

#### 2.复杂的算术运算

```javascript
Math.pow(2,53);     //2的53次幂
Math.round(.6);     //四舍五入
Math.ceil(.6);      //向上取整（天花板函数）
Math.floor(.6);     //向下取整（地板函数）
Math.abs(-5);       //求绝对值
Math.max(x,y,z);    //返回最大值
Math.min(x,y,z);    //返回最小值
Math.random();      //生成一个大于等于0小于1的伪随机数
```

+ Math对象有很多方法
+ 方法：在调用的时候后面有括号



### 七、逻辑运算符

1. 与："&&"
2. 或："||"
3. 非："!"
4. 逻辑运算符的优先级：!>&&>||



### 八、比较运算符

1. <

2. \>

3. <=

4. \>=

5. ==(是否相等)

   + 判断的仅仅只是数据的内容，没有判断数据的类型

   ```javascript
   var a = true;
   var b = "true"
   var c = "1";
   var i = a == b;
   var j = a == c;
   console.log(i); //false
   console.log(j); //true ，boolean本质上是0(false)和1(true)
   ```

6. ===(是否全等)

   + 既判断内容又判断类型
   + 有一个比较特殊的数字NaN，它特殊到自己不等于自己

   ```javascript
   var a = NaN == NaN;
   var b = NaN === NaN;
   console.log(a); //false
   console.log(b); //false
   ```

7. !=
   
   + 判断内容，不关心类型
8. ！==
   
   + 既判断内容又判断类型



### 九、数据类型的转换

> 通过`prompt("")`输入数据的类型，皆为string

#### 1.转Number

##### `Number()`

```javascript
var a = prompt("请输入一个数字");
console.log(typeof a); //string
a = Number(a);
console.log(typeof a); //number
```

1. 如果可以转换成数字，那么返回数字
2. 如果不可以转换成数字，就返回NaN
3. 如果内容出现**小数**，**小数保留**
4. 如果内容为空，转换为0

##### `parseInt()`

1. 如果可以转换成数字，那么返回数字
2. 如果不可以转换成数字，就返回NaN
3. 如果内容出现**小数**，**去掉小数取整数**
4. **如果第一个是数字 ，则继续解析直至字符串解析完毕或者遇到一个非数字符号为止（与Number的区别）**

##### `parseFloat()`

+ 与`parseInt()`一样，唯一的区别是可以保留小数

 #### 2.转string

##### toSting()

> 直接调用变量的toString()方法可以将内容转换成字符串

```javascript
var a = 123;
a.toString();
console.log(a); //123
console.log(typeof a); //string
```

##### String()

> 直接将要转的内容放在string后的括号中，就可以将内容转成字符串

```javascript
var a = 123;
a = String(a);
console.log(a); //123
console.log(typeof a); //string
```



#### 3.转Boolean

##### `Boolean()`

> 用法同Number()、String()一样

+ false、""(空字符串)、0、NaN、undefined(声明没定义)，除了这5种特殊情况，其余任何值都会被转换为true（注：字符串“false”也是true）



#### 4.隐式转换

##### 1）隐式转换成number

> 直接在要转换的内容前加上“+”

```javascript
var a = "123";
console.log(typeof a); //string
a = +a;
console.log(typeof a); //number
```

+ +: `a = +a;`
+ -: `a = a-0`
+ \*: `a= a*1;`
+ /: `a = a/1;`

##### 2）隐式转换成string

`a = a+"";`（即加一个空字符串）

##### 3）隐式转换成Boolean

`a = !!a;`

### 十、流程控制

#### 1.if

#### 2.if__else

+ if的大括号后面不能加分号

#### 3.if_\_else if__else

#### 4. switch case

+ case的变量值后面要加冒号，结束部分必须有break
+ 70<a<80的写法为`a>70 && a<80`

### 十一、代码的调试

1. 打开开发人员工具

2. 找到sorce，并且找到要查看代码的页面

   ![image-20200501144754915](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200501144754915.png)

3. 打断点

4. 刷新页面，我们会发现程序命中了这个断点

![image-20200501145800427](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200501145800427.png)



### 十二、三目运算符

> boolean表达式？操作一：操作儿；

`a>b?alert(a):alert(b);`



### 十三、循环语句

#### 1.white循环

#### 2.终止循环break

#### 3.continue

> 立即结束本次循环，开始下一次循环

#### 4.do while

#### 5.for循环



### 十四、数据类型

1. string
2. number
3. boolean
4. undefined
5. Null
6. object
7. Aarry
8. Function

+ 总结：在js中数据类型分为两大类

> 简单数据类型：1~4
>
> 复杂数据类型：5~8

#### 堆栈

> 一般情况下简单数据类型是存储在栈里面的（值类型）
>
> 一般情况下复杂数据类型是存储在堆里面的（引用类型）

![image-20200501211543182](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200501211543182.png)

#### 基本类型和应用类型

> 基本类型是保存在栈内存中的简单数据段，它们的值都有固定的大小，保存在栈空间，通过按值访问
>
> 引用类型是保存在堆内存中的对象，值大小不固定，栈内存中存放的该对象的访问地址指向堆内存中的对象

```javascript
var a1 = 0;
var a2 = "this is string";
var a3 = null;
var b = {
	x: 10
};
var c = [1, 2, 3];
```

![img](https://upload-images.jianshu.io/upload_images/12665637-b7878064411df56a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800/format/webp)

+ 当我们要访问堆内存中的引用数据类型时
  1. 从栈中获取该对象的地址引用
  2. 再从堆内存中取得我们需要的数据

#### 基本类型的复制行为

```javascript
var a = 20;
var b = a;
b = 30;
console.log(a); // 20
```

![img](https://upload-images.jianshu.io/upload_images/12665637-2c146471c6ced07b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800/format/webp)

+ 在栈内存中的数据发生复制行为时，系统会自动为新的变量分配一个新值，最后这些变量都是相互独立互不影响的。

#### 引用类型发生复制行为

```javascript
var a = { x: 10, y: 20 }
var b = a;
b.x = 5;
console.log(a.x); // 5
```

![img](https://upload-images.jianshu.io/upload_images/12665637-efd7b9913c0e23a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800/format/webp)

1. 引用类型的复制，同样为新的变量b分配一个新的值，保存在栈内存中，不同的是，这个值仅仅是引用类型的一个地址指针
2. 他们两个指向同一个值，也就是地址指针相同，在堆内存中访问到的具体对象实际上是同一个
3. 因此改变b.x时，a.x也发生了变化，这就是引用类型的特性

#### 总结

![img](https://upload-images.jianshu.io/upload_images/12665637-aa862638a1e26ae5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/648/format/webp)



### 十五、object对象

#### 1.对象的创建

`var a = new Object();`

+ 内存中开辟空间，创建一个对象，并且返回刚刚创建的对象

#### 2.对象属性的添加

`a.name = "zhangsan";`

`a.chengji = 99;`

#### 3,对象属性的取值

`alert(a.name);`

#### 3.面向对象和基于对象

+ 面向对象

  > 可以创建自定义的类型，很好的支持继承和多态（c++/java/c#）

+ 基于对象

  > 无法创建自定义的类型，不能很好的支持继承和多态。（JavaScript）

#### 4.自定义构造函数

```javascript
// 自定义构造函数
function Student(name, age, sex, score) {
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.score = score;
    this.sayHi = function() {
  	  console.log("大家好，我是" + this.name);
	}
}
// 创建对象
var s1 = new Student("张三", 18, "nan", 10);
var s2 = new Student("李四", 20, "nan", 20);
s1.sayHi();
s2.sayHi();
```

+ **构造函数的命名：第一个字母要大写**

> 1. 内存开辟空间，存储新创建的对象new Student
> 2. 会把this设置为当前对象
> 3. 执行函数内部的代码，设置对象的属性和 方法
> 4. 返回新创建的对象

#### 5.对象的字面量

> 直接用花括号给一个变量赋值一个对象就是字面量

`var obj = {};`

```javascript
var o = {
    // 键：值  的形式，值可以是任何类型
    name: "zs",
    age: 18,
    sex: 'w',
    salary: 1000,
    dog: {},
    cats: [],
    sayHi: function() {
  	  console.log("大家好，我是" + this.name);
    }
    // 最后一个不需要逗号或者分号
};
o.sayHi();
```

#### 6.输出对象的属性和方法

> **for...in** 语句用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）

```javascript
for (var key in o) {
    console.log(key); //输出o的键
    console.log(o[key]); //输出o的值
}
console.log("-----------------------");
for (var key in o) {
    console.log(key + ':' + o[key]);
}
```

+ 有些系统提供的对象的属性和方法无法遍历，原因是这些属性和方法被设置为不可遍历

#### 7.JSON

> JavaScript Object Notaion（JavaScript对象表示形式）
>
> json是描述数据的一种标准规范

+ json的格式和对象字面量的区别，仅仅是属性需要使用双引号引起

```javascript
var o = {
    "name": "zs",
    "age": 18,
    "sex": 'w',
    "salary": 1000,
    "dog": {},
    "cats": [],
    "sayHi": function() {
    	console.log("大家好，我是" + this.name);
    }
};
```

#### 8.内置对象Array

**数组**

> 引用类型，JavaScript中的内置对象

+ 复习数组的两种创建方式
  + `var array = [3,56,3];`
  + `var array = new Array();`

+ Array对象的属性

  + length获取数组的长度（元素个数）

+ 常用方法

  + 检测数组

    + `instanceof`

      检测对象的类型

      > + `typeof`可以获取任意变量的类型，任意类型的对象使用`typeof`获取到的都是`object`
      >   + `instanceof`只能精确判断对象的类型，

    + `Array.isArray()`

      *HTML5中新增*

  + 转换数组

    + `toString()`

      把数组转换成字符串，每一项用`,`分割

    + `valueOf()`

      返回数组对象本身

    + `join()`

      把数组转换成字符串，参数为分隔符（用引号引起来），如果缺省该值，分隔符则为`,`

  + 栈操作（先进后出）

    + `push()`

    + `pop()`

      取出数组中的最后一个元素，修改length属性

  + 队列操作（先进先出）

    + `push()`

    + `shift()`

      取出数组中的最后一个元素，修改length属性

    + `unshift()`

      在数组最前面插入项，返回数组的长度

  + 排序方法

    + `reverse()`

      翻转数组

    + `sort()`

      对数组的元素进行排序，并返回数组

  + 操作方法

    + `concat()`

      把参数拼接到当前数组

    + `slice()`

      从当前数组中截取一个新的数组，不影响原来的数组，参数`start`从0开始，`end`从1开始

    + `splic()`

      删除或者替换当前数组的某些项目

  + 位置方法

    + `indextOf()`
    + `lastIndexOf()`

  + 迭代方法

    + `every()`
    + `filter()`
    + `forEach()`
    + `map()`
    + `some()`



### 十六、数组

#### 1.数组创建

`var a = new Aarray();`

#### 2.数组的赋值

```javascript
a[0] = "81";
a[1] = "82";
a[2] = "98";
```

#### 3.数组在堆栈中存储的方式

> 数组存放在堆中，数组的首地址存放在栈中

![image-20200501213208246](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200501213208246.png)

#### 4.注意点

+ js中的数组定义好了之后就是一个无穷大的容器
+ 元素可以任意添加：数量不限制、类型不限制
+ 下标从0开始 

#### 5.数组的属性：length

+ 遍历数组

```javascript
for(var i = 0;i < a.length;i++){
	console.log(a[i]);
}
```

>  **字符串也可以看成一个数组**



### 十七、函数

#### 1.作用

> 封装常用的代码

#### 2.函数的两种方式

> ①函数声明

```javascript
function f(a, b) {
	return a + b;
}
console.log(f(5, 6));
```

+ 这里的函数声明和函数的调用，调换位置输出正常

> ②函数表达式

```javascript
var f = function(a, b) {
	return a + b;
};
console.log(f(5, 6));
```

+ 这里的函数表达式和函数的调用，调换位置输出**错误**

+ 函数表达式后面**有分号**

  ![image-20200504180123744](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200504180123744.png)

+ **这是预解析的问题**

#### ！预解析（面试题）

> 解析器首先会预解析，找到var和function之后，把var和function提前（只是声明提前了，没有值）
>
> 预解析完之后再从上到下一行行执行代码

##### ①输出的num是什么

```javascript
var num = 10;
fun();

function fun() {
    console.log(num);
    var num = 20;
}
```

+ 预解析	全局作用域	

  + num（只是声明没有值） function fun()

  ```javascript
  //提前声明
  var num;
  function fun() {
      console.log(num);
      var num = 20;
  }
  
  num = 10;
  fun();
  ```

+ 从上到下一行一行执行代码

  + `num = 10;`

  + `fun();`	//执行到fun后，找到fun函数，进入局部作用域

    + 预解析	fun函数局部作用域	

      + num

      ```javascript
      function fun(){
          //提前声明
          var num;
      
          console.log(num);
          num = 20;
      }
      ```

    + 从上到下一行一行执行代码

      + `console.log(num);`	//此时num在预解析的时候声明了但还没有赋值，所以输出为undefined



##### ②输出的结果为？

```javascript
var a = 18;
f1();
function f1(){
    var b = 9;
    console.log(a);
    console.log(b);
    var a = '123';
}
```

+ 输出a为undefined，b为9
+ **作用域链：先在当前作用域找变量a，如果当前作用域没有变量a，会去上一级作用域找变量a**



##### ③输出结果为？

 ```javascript
f1();
console.log(c);
console.log(b);
console.log(a);

function f1() {
    var a = b = c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}
 ```

+ 预解析	全局作用域	

  + function f1()

  ```javascript
  //提前声明
  function f1() {
      var a = b = c = 9;
      console.log(a);
      console.log(b);
      console.log(c);
  }
  
  f1();
  console.log(c);
  console.log(b);
  console.log(a);
  ```

+ 从上到下一行一行执行代码
  + `f1();`	//执行到f1后，找到f1函数，进入局部作用域

    + 预解析	fun函数局部作用域

      + `var a;`

      ```javascript
      function f1() {
          var a;
          
          a = b = c = 9;
          console.log(a);
          console.log(b);
          console.log(c);
      }
      ```

    + 从上到下一行一行执行代码

      + `a = b = c = 9;`	//b和c没有var声明，则为全局变量
      + `console.log(a);`  //a = 9
      + `console.log(b); `  //b = 9
      + `console.log(c);`  //c = 9

  + `console.log(c);`  //c = 9，c为全局变量

  + `console.log(b);`  //b = 9，b为全局变量

  + `console.log(a);`  //a只在f1函数的局部作用域声明，函数结束后就被销毁了，在全局作用域中找不到a的声明和赋值，所以会报错

  ![image-20200504211109112](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200504211109112.png)



#### 3.函数的定义

+ 驼峰命名法

#### 4.函数的使用



#### 5.函数的参数

+ 函数的个数可以和形参个数不相等
+ **我们始终认为用户输入的值是不安全的，一般都会对用户输入的值进行判断和处理（特别要防止NaN）**

#### 6.函数的返回值

+ 一般情况下函数如果没有`return`或者`return`后面没有跟内容，那么这个函数默认返回 `undefined`

#### 7.js没有重载

+ 在js中，后面相同名称的函数会覆盖前面的函数
+ 重载：函数名字相同，但参数个数不同

#### 8.变量的作用域

> 全局作用域

+ 在任何位置都可以访问
+ 不用var声明的变量是全局变量（不提倡这种做法）

> 局部作用域

+ 在**函数内部**声明一个变量，只能在该函数内部使用
+ 当变量超出作用域之后，变量会被销毁
+ 没有c语言的块级作用域，比如for循环等定义的变量，**js里for循环外可以使用**

#### 9.匿名函数

> 没有命名的函数

##### ①作用

+ 一般用在绑定事件的时候

##### ②语法

+ `function(){}`

##### ③自调用函数

+ 只执行一次

```javascript
(function() {
	alert('Hello');
})();	//加括号调用函数
```

#### 10.递归函数

> 函数自己调用自己

```javascript
//计算一个数的各位数字之和
function getSum(n) {
// 结束的条件
    if (n < 10) {
    	return n;
    }
    // %就是取余的算术运算符
    // parseInt 将一个字符串 string 转换为 radix 进制的整数 ,radix 默认为 10
    // 要被解析的值。如果参数不是一个字符串，则将其转换为字符串(使用  ToString 抽象操作)。字符串开头的空白符将会被忽略
	return n % 10 + getSum(parseInt(n / 10));
}
console.log(getSum(123));
```

+ 执行过程：

   getSum(123);
   3 + getSum(12);
         2 + getSum(1);
               1

+ 比较消耗资源

#### 11.函数是一种数据类型

>  function类型

+ 函数可以作为另一个函数的参数

```javascript
function getResult(a, b, fn) {
	return fn(a, b);
}
//function(a,b){return a+b;}匿名函数作为getResult函数的参数
var result = getResult(5, 6, function(a, b) {
	return a + b;
});
console.log(result);
```



### 十八、介绍

#### 1.浏览器是如何工作的

http://www.2cto.com/kf/201202/118111.html

#### 2.JavaScript语言

> 脚本语言：不需要编译，边解析边执行（速度较慢）
>
> 客户端的脚本语言

+ JavaScript的组成：

> ECMAScript：js语法规范（JavaScript基础）
>
> DOM：js操作网页元素的API（Web APIs）
>
> BOM：操作浏览器部分功能的API（Web APIs）



### 十九、script标签

+ 属性：

  1. `typt = "text/javascript"`

     可以省略

  2. `asunc = "async"`

     可以省略，立即异步下载外部js，不影响页面其他的操作，js下载完毕立即执行

  3. `defer = "defer"`

     值可以省略，脚本延迟到文档完全被分解和显示后再执行，只有外部脚本可以使用

     

### 二十、预解析

#### 1.变量提升

> 定义变量的时候，变量的声明会被提升到作用域的最上面，变量的赋值不会提声。

#### 2.函数提升

> javascript 解析器首先会把当前作用域的函数声明提前到整个作用域的最前面



### 二十一、BOM和DOM

#### 1.什么是DOM

> 文档对象模型，又称为文档树模型。是一套操作HTML和XML文档的API
>
> DOM可以把HTML和XML描述为一个文档树，树上的每一个分支都可以视为一个对象，通过DOM可以添加、修改和移除文档上的某一部分。

#### 2.DOM的相关概念

> DOM就是把HTML视为一个层次结构（树形结构）的文档

+ 文档

  > 就是指HTML或者XML文件

+ 节点

  > HTML文档中的所有内容都可以称之为节点

+ 元素

  > HTML文档中的标签可以称为元素

+ 文档元素（根元素）

  > 文档中的第一个元素，HTML文档元素就是`<html>`

+ 文本节点

+ 属性节点

+ 父节点：parent

+ 子节点：child

+ 兄弟节点：silbing

#### 3.DOM可以做什么

1. 找对象（元素）
2. 设置元素的属性
3. 设置元素的样式
4. 动态创建和删除元素
5. 事件——触发响应
   + 事件的触发者
   + 事件名称
   + 事件响应程序

#### 4.案例：小樱与小狼相册

![image-20200505194416185](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200505194416185.png)

##### 占位符图片网址

http://placehold.it/400x250(需要多大就改成多大)

+ HTML代码

```html
<ul>
    <li>
        <a href="images/小樱和小狼01.jpg" title="小樱和小狼01">
            <img src="images/小樱和小狼01.jpg" alt="小樱和小狼01">
        </a>
    </li>
    <li>
        <a href="images/小樱和小狼02.jpg" title="小樱和小狼02">
            <img src="images/小樱和小狼02.jpg" alt="小樱和小狼02">
        </a>
    </li>
    <li>
        <a href="images/小樱和小狼03.jpg" title="小樱和小狼03">
            <img src="images/小樱和小狼03.jpg" alt="小樱和小狼03">
        </a>
    </li>
    <li>
        <a href="images/小樱和小狼04.jpg" title="小樱和小狼04">
            <img src="images/小樱和小狼04.jpg" alt="小樱和小狼04">
        </a>
    </li>
    <li>
        <a href="images/小樱和小狼05.jpg" title="小樱和小狼05">
            <img src="images/小樱和小狼05.jpg" alt="小樱和小狼05">
        </a>
    </li>
    <li>
        <a href="images/小樱和小狼06.jpg" title="小樱和小狼06">
            <img src="images/小樱和小狼06.jpg" alt="小樱和小狼06">
        </a>
    </li>
</ul>
<div>
    <img src="images/placeholder.png" alt="" id="image">
    <p>选择一个图片</p>
</div>
```

+ JavaScript代码

```javascript
var links = document.querySelectorAll("a");
var img = document.querySelector('#image');
var p = document.querySelector('p');
for (var i = 0; i < links.length; i++) {
    links[i].onclick = function() {
        img.src = this.href;
        p.innerText = this.title;
        return false;
    }
}
```

##### 同步事件`for`与异步事件`onclick`

> 在该案例中，有一点值得注意的是，`onclick`是异步事件，会出现这样的问题

```javascript
for (var i = 0; i < links.length; i++) {
    links[i].onclick = function() {
        //因为for是同步事件、onclick是异步事件，实际上当页面加载完之后for循环就已经完成并且退出了，此时i = 6
        // 所以links[i]并不存在，用this就可以解决这个问题
        console.log(this);  //正确输出links[i]
        console.log(links[i]);  //undefined
        console.log(i); //6
        return false;
    }
}
```

+ 在`for`循环中的`onclick`事件里，要小心使用`i`

##### 新增要求：点击其他地方恢复原状

+ JavaScript代码

```javascript
var body = document.querySelector('body');
var links = document.querySelectorAll("a");
var img = document.querySelector('#image');
var p = document.querySelector('p');

for (var i = 0; i < links.length; i++) {
    links[i].onclick = function(e) {
        img.src = this.href;
        p.innerText = this.title;
        console.log('a');
        e.stopPropagation();
        e.preventDefault();
    }
}

body.onclick = function(e) {
    img.src = "images/placeholder.png";
    p.innerText = "选择一张图片";
    console.log('body');
    e.stopPropagation();
    e.preventDefault();
};
```



## JavaScript高级

### 一、Web、APIs和JS基础关联性

#### 1.Js的组成

+ 在基础知识：十八、介绍



#### 2.Js基础阶段以及Web APIs阶段

> js基础学习ECMAScript基础语法为后面做铺垫，Web APIs是js的应用，大量使用js基础语法做交互效果

+ js基础阶段
  + 我们学习的是ECMAScript 标准规定的基本语法
  + 要求掌握Js基础语法
  + 只学习基本语法，做不了常用的网页交互效果
  + 目的是为了 js后面的课程打基础、做铺垫
+ Web APIs阶段
  + Web APIs是w3c组织的标准
  + Web APIs我们主要学习DOM和BOM
  + Web APIs是我们js所独有的部分
  + 我们主要学习页面交互功能
  + 需要使用js基础的课程内容做基础



### 二、API和Web APIs

#### 1.API

> API是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。

+ 简单理解：**API是给程序员提供一种工具，一边能更轻松的实现想要实现的功能。**



#### 2.Web API

> Web API是浏览器提供的一套操作浏览器功能和页面元素的API（BOM和DOM）。

现阶段我们主要针对于浏览器讲解常用的API，主要针对浏览器做 交互效果。

+ MDN详细API：https://developer.mozilla.org/zh-CN/docs/Web/API



#### 3.API和Web APIs总结

1. API是为我们程序员提供的一个接口，帮助我们实现某种功能，我们会使用就可以了，不必纠结内部如何实现。
2. Web API主要是针对于浏览器提供的接口，主要针对于浏览器做交互效果。
3. Web API一般都有输入和输出（函数的传参和返回值），Web API很多都是方法（函数）
4. 学习Web API可以结合前面学习内置对象方法的思路学习



### 三、DOM简介

#### 1.什么是DOM

> 文档对象模型，是w3c组织推荐的处理可扩展标记语言（HTML或者XML）的标准编程接口。

+ w3c已经定义了一系列的DOM接口，通过这些DOM接口可以改变网页的内容、结构和样式。



#### 2.DOM树

![DOM HTML tree](http://www.runoob.com/images/htmltree.gif)

+ Document：文档，一个页面就是一个文档。
+ Element：元素，页面中的所有标签都是元素。
+ Node：节点，网页中的所有内容都是节点（Element、Attribute、Text、注释等）。***具体可以看JavaScript高级7.2介绍***

**DOM把以上内容都看做是对象**



###  四、获取元素

#### 1.如何获得页面元素

1. 根据ID获取
   + 使用`getElementById()`方法可获得带有id的元素对象
2. 根据标签名获取
   + 使用`getElementsByTagName()`方法可以返回带有指定标签名的对象的集合
   + 注意：
     1. 因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历
     2. 得到的元素对象是动态的（会跟着内容变）
3. 根据类名获取
   + `getElementsByClassName('类名')`根据类名返回元素对象的集合
4. 通过HTML5新增的方法获取
   + `querySelector('选择器')`根据指定选择器 返回第一个元素对象
   + `querySelectorAll('选择器')`根据指定选择器返回元素对象集合
5. 特殊元素获取
   + 获取body元素：`document.body`返回body对象
   + 获取html元素：`document.documentElement`返回html元素对象



### 五、事件基础

#### 1.事件概述

> JavaScript使我们有能力创建动态页面，而事件是可以被JavaScript侦测到的行为

简单理解：触发——响应机制。

+ 网页中的每个元素都可以产生某些可以触发JavaScript的事件，例如，我们可以在用户点击某按钮时产生一个事件，然后去执行某些操作。



#### 2.事件三要素

+ 事件源：事件被触发的对象：谁
+ 事件类型：如何触发 什么事件：比如鼠标点击（onclick）还是鼠标经过（onmouseover） 还是键盘按下
+ 事件处理程序：通过一个函数赋值的方式完成



#### 3.执行事件的步骤

1. 获得事件源
2. 注册事件（绑定事件）
3. 添加事件处理程序（采用函数赋值形式）



#### 4.常见的鼠标事件

+ `onclick`：鼠标点击左键触发
+ `onmouseover`：鼠标经过触发
+ `onmouseout`：鼠标离开触发
+ `onfocus`：获得鼠标焦点触发
+ `onblur`：失去鼠标焦点触发
+ `onmousemove`：鼠标移动触发
+ `onmouseup`：鼠标弹起触发
+ `onmousedown`:鼠标按下触发



### 六、操作元素

#### 1.改变元素内容

1. `element.innerText`（非标准）

   从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉

2. `element.innerHTML`（w3c标准）

   起始位置到终止位置的全部内容，包括html标签，同时保留空格和换行



##### 案例：获得系统当前时间并显示到页面上

![image-20200510110203027](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200510110203027.png)

+ JavaScript代码

```javascript
var btn = document.querySelector('button');
var displayTime = document.querySelector('#displayTime');
btn.onclick = function() {
    // displayTime.innerText = '2020-5-10';
    displayTime.innerText = getDate();
}

function getDate() {
    var date = new Date();
    var year = date.getFullYear();
    var month = date.getMonth() + 1; //获得的月份是从0开始
    var dates = date.getDate(); //getDate是获得几号
    var day = date.getDay(); // 星期天是0 星期一是1
    var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
    var hour = date.getHours();
    var minute = date.getMinutes();
    var second = date.getSeconds();
    todayTime = '今天是：' + year + '年' + month + '月' + dates + '日 ' + arr[day] + ' ' + hour + ':' + minute + ':' + second;
    return todayTime;
}
```



#### 2.表单元素的属性操作

+ 利用DOM可以操作如下表单元素的属性：
  + `type`、`value`、`checked`、`selected`、`disabled`

##### 案例：仿京东显示和隐藏密码

![image-20200510130955498](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200510130955498.png)

![image-20200510131021407](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200510131021407.png)

+ JavaScript代码

```javascript
var eye = document.querySelector('#eye');
var pwd = document.querySelector('#pwd')
var flag = 0;
eye.onclick = function() {
    if (flag == 0) {
        eye.innerText = '';
        eye.innerText = ''; //字体图标
        pwd.type = 'text';
        flag = 1;
    } else {
        eye.innerText = '';
        eye.innerText = '';
        pwd.type = 'password'; //字体图标
        flag = 0;
    }
}
```

+ **在这里我用的是字体图标代替黑马教程上的图片，具体查看文件里的代码**



#### 3.样式属性操作

+ 我们可以通过JS修改元素的大小、颜色、位置等样式。
  1. `element.style` 行内样式操作
  2. `element.className` 类名样式操作
+ **JS里面的样式采用驼峰命名法**，比如`fontSize`、`backgroundColor`
+ JS修改style样式操作，产生的是行内样式，css权重比较高



##### 案例：淘宝点击关闭二维码

![image-20200510160154947](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200510160154947.png)

##### 案例：循环精灵图背景

+ 思路
  1. 首先精灵图图片排列有规律的
  2. 核心思路：利用for循环，修改精灵图片的背景位置`background-position`
  3. 让循环里面的`i`索引号*44就是每个图片的`y`坐标。
+ JavaScript代码

```javascript
var lis = document.querySelectorAll('li');
for (var i = 0; i < lis.length; i++) {
	// 让索引号乘以44积水每个li的背景坐标y index就是 我们的y坐标
	var index = i * 44;
	lis[i].style.backgroundPosition = '0-' + index + 'px';
	//注意js代码的样式名是驼峰法的样式的
}
```

+ 这个用的比较少，这里列出js代码简单了解一下思路即可。

##### 案例：显示隐藏文本框内容

![image-20200510165645760](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200510165645760.png)

+ HTML代码

```javascript
<div class="search">
    <input type="text" class="searchInput" value="手机">
    <button class="searchButton">搜索</button>
</div>
```

+ JavaScript代码

```javascript
var searchText = document.querySelector('.searchInput');
searchText.onfocus = function() {
    if (this.value === '手机') {
        this.value = ' ';
    }
    this.style.color = '#333';
}
searchText.onblur = function() {
    // 这里应该先用正则表达式先对value进行处理？
    this.value = this.value.replace(/(^\s*)/g, "");//删掉前面的空格
    if (this.value == '') {

        this.value = '手机';
    }
    this.style.color = '#ccc';
}
```

+ 我们可以通过JS修改元素的大小、颜色、位置等样式
  1. `element.style`行内样式操作
  2. `element.className`类名样式操作
+ 注意 ：
  1. 如果样式修改的较多，可以采取操作类名更改元素样式
  2. `className`会直接更改元素的类名，会覆盖原先的类名

```javascript
//js代码
var test = document.querySelector('div');
test.onclick = function() {
	this.className = 'change';
}
```

```css
/*css代码*/
.change {
    background-color: purple;
    color: #fff;
    font-size: 25px;
    margin-top: 100px;
}
```



##### 案例：密码框格式提示错误信息

```javascript
var ipt = document.querySelector('.ipt');
var message = document.querySelector('.message');
ipt.onblur = function(){
	if(this.value.length<6||this.value.length > 16){
		message.className = 'message wrong';//这里是两个类名
		message.innerHTML = '您输入的位数不对，要求6~16位';
	} else {
		message.className = 'message right';
		message.innerHTML = '您输入的正确';
	}
}
```



#### 4.排他思想

> 在同一种元素，想要某一个元素实现某种样式，需要用到循环的排他思想算法

1. 所有元素全部清除样式（干掉其他人）
2. 给当前元素设置样式（留下我自己）

**顺序不能颠倒**

```javascript
var btns = document.querySelectorAll('button');
for (var i = 0; i < btns.length; i++) {
    btns[i].onclick = function() {
        for (var i = 0; i < btns.length; i++) {
            btns[i].style.backgroundColor = '';
        }
        this.style.backgroundColor = 'pink';
    }
}
```

##### 案例：换肤效果

![image-20200521165952056](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200521165952056.png)

+ html代码

```html
<ul>
    <li><img src="images/小樱和小狼01.jpg" alt=""></li>
    <li><img src="images/小樱和小狼02.jpg" alt=""></li>
    <li><img src="images/小樱和小狼03.jpg" alt=""></li>
    <li><img src="images/小樱和小狼04.jpg" alt=""></li>
</ul>
```

+ css代码

```css
body {
    background-image: url(images/placeholder.png);
    background-size: 100%;
}

ul {
    display: flex;
    justify-content: center;
    margin-top: 100px;
}

li {
    height: 100px;
    list-style: none;
    cursor: pointer;
}

img {
    height: 100%;
}
```

+ JavaScript代码

```javascript
imgs = document.querySelectorAll('img');
for (var i = 0; i < imgs.length; i++) {
    imgs[i].onclick = function() {
   		document.body.style.backgroundImage = 'url(' + this.src + ')';
    }
}
```



##### 案例：表格隔行变色

![image-20200521172537420](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200521172537420.png)

+ javascript代码

```javascript
var trs = document.querySelector('tbody').querySelectorAll('tr');
for (var i = 0; i < trs.length; i++) {
    trs[i].onmouseover = function() {
        this.style.backgroundColor = 'pink';
    }
    trs[i].onmouseout = function() {
        this.style.backgroundColor = '';
    }
}
```



#### 5.自定义属性的操作

##### 1）获取属性值

+ `element.属性`
  + 获取内置属性值（元素本身自带的属性）
+ `element.getAttribute('属性')`
  + 主要获取程序员自定义的属性

```html
<body>
    <div id="demo" index='1'>文本</div>
    <script>
        var div = document.querySelector('div');
        // 1.elemnet.属性
        console.log(div.id);
        // 2.element.getAttribute('属性')
        console.log(div.getAttribute('id'));
        console.log(div.getAttribute('index'));
    </script>
</body>
```

##### 2）设置属性值

+ `element.属性 = '值'`
  + 设置内置属性值
+ `element.setAttribute('属性','值')`
  + 设置自定义的属性（标准）

##### 3）移除属性

+ `element.removeAttribute('属性')`

```javascript
var div = document.querySelector('div');
div.id = 'test';
div.className = 'navs'; //className才是html标签自带的class属性
div.setAttribute('index', 2);
div.setAttribute('class', 'footer'); //class是自定义属性，和className不同
console.log(div.class); // undifined
console.log(div.getAttribute('class')); // footer
div.removeAttribute('index');
```

+ 注意：`class`不是内置属性值，`className`才是内置属性值`class`



##### 案例：tab栏切换（重点案例）

![image-20200521211123302](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200521211123302.png)

+ html代码

```html
<ul class="tab_list">
    <li>模块一</li>
    <li>模块二</li>
    <li>模块三</li>
    <li>模块四</li>
    <li>模块五</li>
</ul>
<div>
    <div class="item">模块一的内容</div>
    <div class="item">模块二的内容</div>
    <div class="item">模块三的内容</div>
    <div class="item">模块四的内容</div>
    <div class="item">模块五的内容</div>
</div>
```

+ JavaScript代码

```javascript
var tab_list = document.querySelector('.tab_list');
var lis = tab_list.querySelectorAll('li');
var items = document.querySelectorAll('.item');
for (var i = 0; i < lis.length; i++) {
    lis[i].setAttribute('index', i);
    lis[i].onclick = function() {
        for (var i = 0; i < lis.length; i++) {
            lis[i].className = '';
        }
        this.className = 'current';
        for (var i = 0; i < items.length; i++) {
            items[i].style.display = 'none';
        }
        items[this.getAttribute('index')].style.display = 'block';
    }
}
```

+ 这里用到自定义属性index，正好index就是items集合的下标



#### 6.H5自定义属性

> 自定义属性的目的：为了保存并使用数据，有些数据可以保存到页面中而不用保存到数据库中。

1. 设置H5自定义属性

   > H5规定自定义属性`data-`开头作为属性名并且赋值

   + 比如`<div data-index = '1'><div>`或者使用JS设置`element.seAttribute('data-index',2)`

2. 获取H5自定义属性

   + 兼容性湖区`element.getAttribute('data-index')`
   + `dataset`是一个集合，里面存放了所有以`data`开头的自定义属性
     + H5新增`element.dataset.index`或者`element.dataset['index']`(ie11才开始支持)
   + 如果自定义属性里面有多个-链接的单词，我们获取的时候采取驼峰命名法

```javascript
var div = document.querySelector('div');
console.log(div.getTime); //undefined 这是自定义属性
console.log(div.getAttribute('getTime'));
console.log(div.getAttribute('data-index'));
// dataset是一个集合，里面存放了所有以data开头的自定义属性
console.log(div.dataset); // DOMStringMap {index: "2", listName: "andy"}
console.log(div.dataset.index);
console.log(div.dataset['listName']);
```



### 七、节点操作

#### 1.为什么学节点操作

+ 获取元素通常用两种方式

  1. 利用DOM提供的方法获取元素
     + `getElementById()`
     + ​	`querySelector()`等
     + 逻辑性不强，繁琐

  2. 利用节点层级关系获取元素
     + 利用父子兄节点关系获取元素
     + 逻辑性强，但是兼容性稍差



#### 2.节点概述

> 关于节点的介绍可以查看***JavaScript高级3.2***

+ 节点至少拥有`nodeType`(节点类型)、`nodeName`(节点名称)和`nodeValue`(节点值)这三个基本属性
  + 元素节点 `nodeType=1`
  + 属性节点`nodeType=2`
  + 文本节点`nodeType=3`（文本节点包括文字、空格、换行等）
+ 我们在实际开发中，节点操作主要操作的是**元素节点**



#### 3.节点层级

1. 父级节点`node.parentNode`

	+ `parentNode`属性可返回某节点的父节点，注意是**最近的一个父节点**
	+ 如果指定的节点没有父节点则返回`null`

2. 子节点

   + `parentNode.childNodes`（标准）
     + 返回指定节点的子节点的集合，该集合为即时更新的集合
     + 返回值里面包含了所有的子节点，包括元素节点、文本节点等
     + 如果只是想要获取里面的元素节点，则需要专门处理。**所以一般不提倡使用`childNodes`**
   + `parentNode.children`（非标准）
     + `parentNode.children`是一个只读属性，返回所有的子元素节点。**它只返回子元素节点，其余节点不返回**（需重点掌握）
     + 虽然`children`是一个非标准，但是得到了各个浏览器的支持
   + `parentNode.firstChild`
     + 返回第一个子节点，找不到则返回`null`。**同样包含所有的节点**
   + `parentNode.lastChild`
     + 返回最后一个子节点，找不到则返回`null`。**同样包含所有的节点**
   + `parentNode.firstElementChild`
     + 返回第一个子元素节点，找不到则返回`null`。**这个可以返回子元素节点，但有兼容性（IE9以上才支持）**
   + `parentNode.lastElementChild`
     + 返回最后一个子元素节点，找不到则返回`null`。**这个可以返回子元素节点，但有兼容性**

```javascript
var ol = document.querySelector('ol');
// 1. firstChild第一个子节点，不管是文本节点还是元素节点
console.log(ol.firstChild);
console.log(ol.lastChild);
// 2. firstElementChild返回第一个子元素节点 有兼容性
console.log(ol.firstElementChild);
console.log(ol.lastElementChild);
// 3. 实际开发的写法 既没有兼容性问题又能返回第一个子元素
console.log(ol.children[0]);
console.log(ol.children[ol.children.length - 1]);
```



##### 案例：下拉菜单

![image-20200522145051695](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200522145051695.png)

+ html的结构：
  + 导航栏用ul，每个选项卡用li
  + 每个选项卡里面有两个children，一个a放选项卡的名称，一个ul放一个选项的下拉菜单
  + 即 `ul>li>a+(ul>li)` 
+ 案例分析：
  + `li`的`a`（选项卡）一直显示，当鼠标经过`li`时，第二个孩子`ul`（下拉菜单）显示，当鼠标离开，则`ul`隐藏
+ html代码：

```html
<ul class="nav">
    <li>
        <a href="#">微博</a>
        <ul>
            <li>个人中心</li>
            <li>消息通知</li>
        </ul>
    </li>
    <li>
        <a href="#">博客</a>
        <ul>
            <li>博客评论</li>
            <li>未读提醒</li>
        </ul>
    </li>
    <li>
        <a href="#">QQ</a>
        <ul>
            <li>登陆</li>
            <li>注册</li>
            <li>qq空间</li>
        </ul>
    </li>
</ul>
```

+ javascript代码

```javascript
var nav = document.querySelector('.nav');
var lis = nav.children;
for (var i = 0; i < lis.length; i++) {
    lis[i].onmouseover = function() {
        this.children[1].style.display = 'block';
    }
    lis[i].onmouseout = function() {
        this.children[1].style.display = 'none';
    }
}
```



3. 兄弟节点

   1. `node.nextSibling`
      + 返回当前元素的下一个兄弟节点，找不到则返回`null`。**包含所有节点**
   2. `node.previousSibling`
      + 返回当前元素的下一个兄弟节点，找不到则返回`null`。**包含所有节点**
   3. `node.nextElementSibling`
      + 返回当前元素的下一个兄弟元素节点，找不到则返回`null`，有兼容性问题
   4. `node.previousElementSibling`
      + 返回当前元素的上一个兄弟元素节点，找不到则返回`null`，有兼容性问题

   + **如何解决兼容性问题**

     + 自己封装一个兼容性函数

     ```javascript
     function getNextElementSibling(element) {
         var el = element;
         while (el = el.nextSibling) {
             if (el.nodeType === 1) {
                 return el;
             }
         }
         return null;
     }
     ```

     

#### 4.添加一个新节点

1. 创建节点

	+  `document.createElement('tagName')`
		+ 该方法创建由`tagName`指定的HTML元素。因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为动态创建元素节点。

2.  添加节点：

	+  `node.appendChild(child)`
    	+ 该方法将一个节点添加到指定父节点的子节点列表末尾。类似于css里面的after伪元素
	+ `node.insertBefore(child, 指定元素)`
      		+ 该方法将一个节点添加到父节点的指定子节点前面，类似于css里面的before伪元素

##### 案例：简单版发布留言案例

```javascript
var btn = document.querySelector('button');
var text = document.querySelector('textarea');
var ul = document.querySelector('ul');
btn.onclick = function() {
    if (text.value == '') {
        alert("您没有输入内容！");
        return false;
    } else {
        var li = document.createElement('li');
        li.innerHTML = text.value;
        ul.insertBefore(li, ul.children[0]);
        text.value = '';
    }
}
```



#### 5.删除节点

+ `node.removeChild(child)`
  + 从DOM中删除一个子节点，返回删除的节点。



##### 案例：删除留言案例

+ 案例分析：
  + 当我们吧文本域里面的值赋给`li`的时候，多添加一个删除的链接
  + 需要把所有的链接获取过来，当我们点击当前的链接的时候，删除当前链接所在的`li`
  + 阻止链接跳转需要添加`javascript:void(0)`或者`javascript:;`

```javascript
var btn = document.querySelector('button');
var text = document.querySelector('textarea');
var ul = document.querySelector('ul');
btn.onclick = function() {
    if (text.value == '') {
        alert("您没有输入内容！");
        return false;
    } else {
        var li = document.createElement('li');
        li.innerHTML = text.value + '<a href="javascript:;">删除</a>';
        ul.insertBefore(li, ul.children[0]);
        text.value = '';
        adele = document.querySelectorAll('a');
        // 这个for循环只能放在这里，这是让我迷惑的地方
        for (var i = 0; i < adele.length; i++) {
            adele[i].onclick = function() {
                ul.removeChild(this.parentNode);
            }
        }
    }
}
```



#### 6.复制节点（克隆节点）

+ `node.cloneNode()`
  + 返回调用该方法的节点的一个副本，也称为克隆节点/拷贝节点
  + 如果括号参数为**空或false**，则是**浅拷贝**，即只克隆复制节点本身，不克隆里面的子节点
    + 浅拷贝：只复制标签不复制里面的内容
  + 如果括号参数为**true**，则是**深拷贝**，会复制节点本身以及里面所有的子节点。
    + 深拷贝：复制标签复制里面的内容

##### 案例：动态生成表格

![image-20200522222307632](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200522222307632.png)

+ HTML代码

```html
<table>
    <thead>
        <tr>
            <th>姓名</th>
            <th>科目</th>
            <th>科目</th>
            <th>操作</th>
        </tr>
    </thead>
    <tbody>

    </tbody>
</table>
```

+ javascript代码

```javascript
var datas = [{
    name: '张三',
    subject: 'JavaScript',
    score: 100
}, {
    name: '李四',
    subject: 'python',
    score: 99
}, {
    name: '王五',
    subject: 'c++',
    score: 59
}, {
    name: '锐涵',
    subject: 'java',
    score: '100'
}];

var tbody = document.querySelector('tbody');
for (var i = 0; i < datas.length; i++) {
    var tr = document.createElement('tr');
    tbody.appendChild(tr);
    for (var k in datas[i]) {
        var td = document.createElement('td');
        td.innerHTML = datas[i][k];
        tr.appendChild(td);
    }
    var td = document.createElement('td');
    td.innerHTML = '<a href="javascript:;">删除</a>';
    tr.appendChild(td);
}
var dele = document.querySelectorAll('a');
for (var i = 0; i < dele.length; i++) {
    dele[i].onclick = function() {
        tbody.removeChild(this.parentNode.parentNode);
    }
}
```



#### 7.三种动态创建元素区别

+ `document.write()`

  + 直接将内容写入页面的内容流，但是文档流执行完毕，则他会**导致页面全部重绘**

+ `element.innerHTML`

  + 将内容写入某个DOM节点，不会导致页面全部重绘
  + 创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂

  ```javascript
  var inner = document.querySelector('.inner');
  //innerHTML采用字符串拼接
  for(var i = 0;i <= 100;i++){
  	inner.innerHTML += '<a href='#'>百度</a>';
  }
  //innerHTML数组形式拼接
  var arr = []
  for(var i = 0;i <= 100;i++){
  	arr.push('<a href='#'>百度</a>');
  }
  ```

+ `document.createElement`

  + 创建多个元素效率稍低一点点，但是结构更清晰

+ **总结**：不同浏览器下，`innerHTML`效率要比`creatElement`高



### 八、DOM重点核心

+ 基本介绍详情看JavaScript高级的**三、DOM简介**

1. 对于JavaScript，为了能够使JavaScript操作HTML，JavaScript就有了一套自己的dom编程接口
2. 对于HTML，dom使得html形成一棵dom树，包含文档、元素、节点

#### 1.创建

1. `document.write`
2. `innerHTML`
3. `createElement`

#### 2.增

1. `appendChild`
2. `insertBefore`

#### 3.删

1. `removeChild`

#### 4.改

主要修改dom的元素属性、dom元素的内容、属性、表单的值等

1. 修改元素的属性：src、href、title等
2. 修改普通元素内容：innerHTML、innerText
3. 修改表单元素：value、type、disabled等
4. 修改元素样式：style、className

#### 5.查

主要获取查询dom的元素

1. DOM提供的API方法：`getElementById`、`getElementsByTagName`古老方法不太推荐
2. H5提供的新方法：`querySelector`、`querySelectorAll`提倡
3. 利用节点操作获取元素：`parentNode`、`children`、`previousElementSibling`、`nextElementSibling` 提倡

#### 6.属性操作

主要针对于自定义属性

1. `setAttribute`：设置dom的属性值
2. `getAttribute`：得到dom的属性值
3. `removeAttribute`：移除属性

#### 7.事件操作

给元素注册事件，采取 事件源.事件类型 = 事件处理程序

+ onclick：鼠标点击左键触发
+ onmouseover：鼠标经过触发
+ onmouseout：鼠标离开触发
+ onfocus：获得鼠标焦点触发
+ onblur：失去鼠标焦点触发
+ onmousemove：鼠标移动触发
+ onmouseup：鼠标弹起触发
+ onmousedown：鼠标按下触发

### 八、注册事件

#### 1.注册事件概述

> 给元素添加事件，称为注册事件或者绑定事件
>
> 注册事件有两种方式：**传统方式**和**方法监听注册方式**

#### 2.`addEventListener`事件监听方式

`eventTarget.addEventListener(type, listener[, useCapture])`

+ `eventTarget.addEventListener()`方法将指定的监听器注册到`eventTarget`（目标对象）上，当该对象触发指定的事件时，就会执行事件处理函数。
+ 该方法接收三个参数：
  + type：事件类型字符串，比如click、mouseover、注意这里不要带on
  + listener：事件处理函数，事件发生时，会调用该监听函数
  + useCapture：可选参数，是一个布尔值，默认是false。

#### 3.`attachEvent`事件监听方式

`eventTarget.attachEvent(eventNameWithOn, callback)`

+ `eventTarget.attachEvent()`方法将指定的监听器注册到eventTarget上，当该对象触发指定的事件时，指定的回调函数就会被执行。
+ 该方法接收两个参数：
  + eventNameWithOn：事件类型字符串，比如onclick、onmouseover、这里要带on
  + callback：事件处理函数，当目标触发事件时回调函数被调用

**注意：IE8及早期版本支持**

### 九、删除事件（解绑事件）

#### 1.删除事件的方式

1. 传统注册方式

`eventTarget.onclick = null;`

2. 方法监听注册方式
   + `eventTarget.removeEventListener(type, listener[, useCapture]);`
   + `eventTarget.detachEvent(eventNameWithOn, callback);`



### 十、DOM事件流

> **事件流**描述的是从页面中接收事件的顺序
>
> **事件**发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流

比如我们给一个div注册了点击事件：

+ DOM事件流分为3个阶段：
  1. 捕获阶段
  2. 当前目标阶段
  3. 冒泡阶段
+ 事件冒泡：IE最早 提出，事件开始时由最具体的元素接收，然后逐级向上传播到DOM最顶层节点的过程
+ 事件捕获：网景最早提出，由DOM最顶层节点开始，然后逐级向下传播到最具体的元素接收的过程

> 事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流

**注意：**

1. js代码中只能执行捕获或者冒泡其中的一个阶段
2. onclick和attachEvent只能得到冒泡阶段
3. `addEventListener(type, listener[, useCapture])`第三个参数如果是true，表示在事件捕获阶段调用事件处理程序；如果是false（不写默认就是false），表示在事件冒泡阶段调用事件处理程序。
4. 实际开发中我们很少使用事件捕获，我们更关注事件冒泡。
5. 有些事件是没有冒泡的，比如onblur、onfocus、onmouseenter、onmouseleave
6. 事件冒泡有时候会带来麻烦，有时候又会帮助很巧妙的做某些事件



### 十一、事件对象

#### 1.什么是事件对象

```javascript
eventTarget.onclick = function(event){}
eventTarget.addEventListener('click',function(event){})
//这个event就是事件对象，我们更喜欢写成 e 或者 evt
```

> event对象代表事件的状态，比如键盘按键的状态、鼠标的位置、鼠标按钮的状态

+ 事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面，这个对象就是事件对象event，它有很多属性和方法。
+ 比如：
  1. 谁绑定了这个事件
  2. 鼠标触发事件的话，会得到鼠标的相关信息，如鼠标位置
  3. 键盘触发事件的话，会得到键盘的相关信息，如按了哪个键

#### 2.事件对象的使用语法

```javascript
eventTarget.onclick = function(event){}
eventTarget.addEventListener('click',function(event){})
//这个event就是事件对象，我们更喜欢写成 e 或者 evt
```

+ 这个event是个形参，系统帮我们设定为事件对象，不需要传递实参过去
+ 当我们注册事件时，event对象就会被系统自动创建，并依次传递给事件监听器（事件处理函数）

#### 3.事件对象的兼容性

事件对象本身的获取存在兼容性问题：

1. 标准浏览器中是浏览器给方法传递的参数，只需要定义形参e就可以获取到。
2. 在IE6~8中，浏览器 不会给方法传递参数，如果需要的话，需要到window.event中获取查找

#### 4.事件对象的常见属性和方法

+ `e.target`：返回触发事件的对象	标准
+ `e.srcElement`：返回触发事件的对象     非标准 ie6~8使用
+ `e.type`：返回事件的类型 比如click mouseover 不带on
+ `e.cancelBubble`：该属性阻止冒泡   非标准 ie6~8使用
+ `e.returnValue`：该属性阻止默认事件（默认行为） 非标准
+ `e.preventDefault()`：该方法阻止默认事件（默认行为） 标准
+ `e.stopPropagation()`：阻止冒泡 标准



### 十二、阻止事件冒泡

#### 1.阻止事件冒泡的两种方式

+ `e.stopPropagation()`：阻止冒泡 标准
+ `e.cancelBubble`：该属性阻止冒泡   非标准 ie6~8使用

#### 2.阻止事件冒泡的兼容性解决方案

```javascript
if(e && e.stopPropagation){
	e.stopPropagation();
}else{
	window.event.cancelBubble = true;
}
```



### 十三、事件委托（代理、委派）

事件冒泡本身的特性，会带来坏处，也会带来好处，需要我们灵活掌握 ，程序中也有如此场景：

```html
<ul>
	<li>知否知否，应该有弹框在手</li>
	<li>知否知否，应该有弹框在手</li>
	<li>知否知否，应该有弹框在手</li>
	<li>知否知否，应该有弹框在手</li>
	<li>知否知否，应该有弹框在手</li>
	<li>知否知否，应该有弹框在手</li>
</ul>
```

点击每个li都会弹出对话框，以前需要给每个li注册事件，是非常辛苦的，而且访问DOM的次数越多，这就会延长整个页面的交互就绪时间。

#### 事件委托

> 事件委托也称为事件代理，在jQuery里面称为事件委派

#### 事件委托的原理（重要）

> **不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点**

#### 事件委托的作用

+ 我们只操作了一次DOM，提高了程序的性能



### 十四、常用的鼠标事件

#### 1.常用的鼠标事件

+　JavaScript高级：**7.3事件操作**

1. 禁止鼠标右键菜单

   + contextmenu主要控制应该合适显示上下文菜单，主要用于程序员取消默认的上下文菜单

   ```javascript
   document.addEventListener('contextmenu', function(e){
   	e.preventDefault();
   })
   ```

2. 禁止鼠标选中（selectstart 开始选中）

```javascript
document.addEventListener('selectstart',function(e){
	e.preventDefault();
})
```

#### 2.鼠标事件对象

> event对象代表事件的状态，跟事件相关的一系列信息的集合。现阶段我们主要是用鼠标事件对象MouseEvent和键盘事件对象KeyboardEvent

| 鼠标事件对象 | 说明                                      |
| :----------- | ----------------------------------------- |
| e.clientX    | 返回鼠标相对于浏览器窗口可视区的 X 的坐标 |
| e.clientY    | 返回鼠标相对于浏览器窗口可视区的 Y 的坐标 |
| e.pageX      | 返回鼠标相对于文档页面的 X 坐标 IE9+ 支持 |
| e.pageY      | 返回鼠标相对于文档页面的 Y 坐标 IE9+ 支持 |
| e.screenX    | 返回鼠标相对于电脑屏幕的 X 坐标           |
| e.screenY    | 返回鼠标相对于电脑屏幕的 Y 坐标           |

#### 案例：跟随鼠标的青蛙

![image-20200528160258136](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200528160258136.png)

+ 案例分析
  1. 鼠标不断的移动，使用鼠标移动事件：mousemove
  2. 在页面中移动，给document注册事件
  3. 图片要移动距离，而且不占位置，我们使用绝对定位即可
  4. 核心原理：每次鼠标移动，我们都会获得最新的鼠标坐标，把这个x和y坐标作为图片的top和left值就可以移动图片



+ JavaScript代码：

```javascript
img = document.querySelector('img');
document.addEventListener('mousemove', function(e) {
    var x = e.pageX;
    var y = e.pageY;
    img.style.top = y - 38 + 'px';
    img.style.left = x - 38 + 'px';
})
```



### 十五、常用的键盘事件

#### 1. 常用键盘事件

| 键盘事件   | 触发条件                                                     |
| ---------- | ------------------------------------------------------------ |
| onkeyup    | 某个键盘按键被松开时触发                                     |
| onkeydown  | 某个键盘按键被按下时触发                                     |
| onkeypress | 某个键盘按键被按下时触发**但是它不识别功能键 比如ctrl shift 箭头等** |

+ **注意：**
  1. 如果使用addEventListener不需要加on
  2. onkeypress和前面2个的区别是，它不识别功能键，比如左右箭头，shift等
  3. 三个事件的**执行顺序**是：keydown -- keypress -- keyup

#### 2,键盘事件对象

+ 属性：keyCode
  + 返回该键的ASCII值
+ **注意**：
  + onkeydown和onkeyup不区分字母大小写，onkeypress区分字母大小写。
  + 在我们实际开发中，我们更多的使用keydown和keyup，它能识别所有键
  + keypress不识别功能键，但是keyCode属性能区分大小写，返回不同的ASCII值
  + `console.log(e.keyCode)`

#### 案例：模拟京东按键输入内容

+ 案例分析：
  1. 核心思路：检测用户是否按下了s键，如果按下了s键，就把光标定位到搜索框里面
  2. 使用键盘事件对象里面的keyCode判断用户按下的是否是s键
  3. 搜索框获得焦点：使用js里面的focus()方法
+ JavaScript代码

```javascript
var seacrh = document.querySelector('input');
document.addEventListener('keyup', function(e) {
    if (e.keyCode == 83) {
        seacrh.focus();
    }
})
```

+ 这里**用keyup而不用keydown**。如果用keydown的话按下s就触发该事件，获得焦点后会输入s



### 十六、BOM概述

#### 1.什么是BOM

> BOM(Browser Object Model)即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是window

+ BOM由一系列相关的对象构成，并且每个对象都提供了很多方法与属性。
+ BOM缺乏标准，JavaScript语法的标准化组织是ECMA，DOM的标准化组织是W3C，BOM最初是Netscape浏览器标准的一部分。

| DOM                                     | BOM                                             |
| --------------------------------------- | ----------------------------------------------- |
| 文档对象模型                            | 浏览器对象模型                                  |
| DOM就是把【文档】当做一个【对象】来看待 | 把【浏览器】当做一个【对象】来看待              |
| DOM的顶级对象是document                 | BOM的顶级对象是window                           |
| DOM主要学习的是操作页面元素             | BOM学习的是浏览器窗口交互的一些对象             |
| DOM是W3C标准规范                        | BOM是浏览器厂商在各自浏览器上定义的，兼容性较差 |

#### 2.BOM的构成

+ BOM比DOM更大，它包含DOM
+ window(BOM)
  + document(DOM)
  + location
  + navigation
  + screen
  + history

+ window对象是浏览器的顶级对象，它具有双重角色
  1. 它是js访问浏览器窗口的一个接口
  2. 它是一个全局对象，定义在全局作用域中的变量、函数都会变成window对象的属性和方法
+ 在调用的时候可以省略window，前面学习的对话框都属于window对象方法，如alert()、prompt()等
+ **注意：window下的一个特殊属性window.name**

### 十七、window对象的常见事件

#### 1.窗口加载事件

```javascript
window.onload = function(){};
//或者
window.addEventListener('load',function(){});
```

+ window.onload是窗口（页面）加载事件，当文档内容完全加载完成会触发该事件（包括图像、脚本文件、css文件等），就调用的处理函数
+ **注意：**
  1. 有了window.onload就可以**把js代码写到页面元素的上方**（一般都是要等页面加载完再执行js代码，就要**将代码放在最后**），因为onload是等页面内容全部加载完毕，再去执行处理函数。
  2. window.onload传统注册事件方式只写一次，如果有多个，会以最后一个window.onload为准
  3. **如果使用addEventListener则没有**

#### 2.调整窗口大小事件

```javascript
window.onresize = function(){}
window.addEventListener('resize',function(){})
```

`window.onresize`是调整窗口大小加载事件，当触发时就调用的处理函数

+ **注意：**
  1. 只要窗口大小发生像素变化，就会触发这个事件。
  2. **我们经常利用这个事件完成响应式布局。`window.innerWidth`当前屏幕的宽度**



### 十八、定时器

#### 1.两种定时器

window对象给我们提供了2个非常好用的方法-定时器

+ `setTimeout()`
+ `setInterval()`

#### 2.`setTimeout()`定时器

`window.setTimeout(调用函数,[延迟的毫秒数]);`

setTimeout()方法用于设置一个定时器，该定时器在定时器到期后执行调用函数

**注意：**

1. window可以省略。
2. 这个调用函数可以**直接写函数**，或者**写函数名**或者采取字符串'函数名()'三种形式。第三种不推荐
3. 延迟的毫秒数省略默认是0，如果写，必须是毫秒
4. 因为定时器可能有很多，所以我们经常给定时器赋值一个标识符

```javascript
function callback(){
	console.log('爆炸了');
}
var timer1 = setTimeout(callback, 3000);
```

#### 3.回调函数

`window.setTimeout(调用函数, [延迟的毫秒数]);`

+ setTimeout()这个调用函数我们也称为**回调函数callback**
+ 普通函数是按照代码顺序直接调用，而这个函数，需要等待时间，时间到了才去调用函数，因此称为回调函数
+ 简单理解：回调，就是回头调用的意思。上一件事干完，再回头调用这个函数。
+ 以前学习的`element.onclick = function(){}`或者`element.addEventListener('click',fn)`里面的函数也是回调函数。

##### 案例：5秒之后自动关闭广告

```javascript
var ad = document.querySelector('.ad');
setTimeout(function(){
	ad.style.display = 'none';
},5000);
```

#### 3.停止setTimeout()定时器

`window.clearTimeout(timeoutID)`

+ clearTimeout()方法取消了先前调用setTimeout()建立的定时器
+ **注意：**
  1. window可以省略
  2. 里面的参数就是定时器的标识符

#### 4.setInterval()定时器

`window.setInterval(回调函数,[间隔的毫秒数]);`

+ setInterval()方法重复调用一个函数，每隔这个时间，就去调用一次回调函数
+ **注意：**
  1. window可以省略
  2. 这个调用函数可以直接写函数，或者写函数名或者采取字符串'函数名()'三种形式
  3. 间隔的毫秒数省略默认是0，如果写，必须是毫秒，表示每个多少毫秒就自动调用这个函数
  4. 因为定时器可能有很多，所以我们经常给定时器赋值一个标识符

##### 案例：倒计时

![image-20200528203211111](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200528203211111.png)

+ 案例分析
  1. 这个倒计时是不断变化的，因此需要定时器来自动变化（setInterval）
  2. 三个黑色盒子里面分别存放时分秒
  3. 三个黑色盒子利用innerHTML放入计算的小时分钟秒数
  4. 第一次执行也是间隔毫秒数，因此刚刷新页面会有空白
  5. 最好采取封装函数的方式，这样可以先调用一次这个函数，防止刚开始刷新有页面空白问题

+ JavaScript代码

```javascript
var hour = document.querySelector('.hour');
var minute = document.querySelector('.minute');
var second = document.querySelector('.second');
var inputTime = +new Date('2020-5-29 00:00:00');
//先调用一次这个函数，防止第一次刷新页面有空白
countDown();
// +new Date()，结果跟Date对象的getTime()，valueOf()是一样的，他们返回的都是1970年1月1日午夜以来的毫秒数

setInterval(countDown, 1000);

function countDown() {
    var nowTime = +new Date();
    var times = (inputTime - nowTime) / 1000;
    var h = parseInt(times / 60 / 60);
    h = h < 10 ? '0' + h : h;
    hour.innerHTML = h;
    var m = parseInt(times / 60 - h * 60);
    m = m < 10 ? '0' + m : m;
    minute.innerHTML = m;
    var s = parseInt(times - h * 3600 - m * 60);
    s = s < 10 ? '0' + s : s;
    second.innerHTML = s;
}
```

#### 5.停止setInterval()定时器

`window.clearInterval(intervalID)`

+ clearInterval()方法取消了先前通过调用setInterval()建立的定时器
+ **注意：**
  1. window可以省略
  2. 里面的参数就是定时器的标识符

##### 案例：发送短信

点击按钮之后，该按钮60秒之内不能再次点击，防止重复发送短信

+ 案例分析：
  1. 按钮点击之后，会禁用disable为true
  2. 同时按钮里面的内容会变化，注意button里面的内容通过innerHTML修改
  3. 里面秒数是有变化的，因此需要用到定时器
  4. 定义一个变量，在定时器里面，不断递减
  5. 如果变量为0说明到了时间，我们需要停止定时器，并且复原按钮初始状态
+ JavaScript代码

```javascript
var btn = document.querySelector('button');
var time = 5;
btn.addEventListener('click', function() {
    btn.disabled = true;
    btn.innerHTML = '还剩下' + time + '秒';
    var timer = setInterval(function() {
        if (time == 0) {
            clearInterval(timer);
            btn.disabled = false;
            btn.innerHTML = '发送信息';
            time = 5;
        } else {
            time--;
            btn.innerHTML = '还剩下' + time + '秒';
        }
    }, 1000);
})
```

#### 6.this

> this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，一般情况下this的最终指向的是那个调用它的对象。

1. 全局作用域或者普通函数中this指向全局对象window（注意定时器里面的this都是指向window）

```javascript
console.log(this);

function fn(){
	console.log(this);
}
window.fn();
window.setTimeout(function(){
	console.log(this);
},1000);
```

2. 方法调用中，谁调用this就指向谁

```javascript
var o = {
	sayHi:function(){
		console.log(this);	//这个this指向的是 o 这个对象
	}
}
o.sayHi();

var btn = document.querySelector('button');
btn.addEventListener('click',function(){
	console.log(this);//this指向的是btn这个按钮对象
})
```

3. 构造函数中this指向构造函数的实例

```javascript
function Fun(){
	console.log(this);	//this指向的是fun实例对象
}
var fun = new Fun();
```



### 十九、JS执行机制

#### 1.JS是单线程

+ JavaScript语言的一大特点就是**单线程**，也就是说，**同一个时间只能做一件事**。
+ 单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。这样所导致的问题是：如果JS执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

#### 2.一个问题

+ 以下代码执行的结果是什么？

```javascript
console.log(1);
setTimeout(function(){
	console.log(3);
},1000);
console.log(2);
```

>  结果是：1 2 3

+ 以下代码执行的结果又是什么？

```javascript
console.log(1);
setTimeout(function(){
	console.log(3);
},0);
console.log(2);
```

> 结果是：1 2 3

#### 3.同步和异步

+ 为了解决这个问题，利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程，于是，JS中出现了**同步**和**异步**

+ **同步**

  > 前一个任务结束再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。比如做饭的同步做法：我们要烧水煮饭，等水开了（10分钟之后），再去切菜，炒菜。

+ **异步**

  > 你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。比如做饭的异步做法，我们在烧水的同时，利用这10分钟，去切菜，炒菜。

+ 他们的本质区别：这条流水线上各个流程的执行顺序不同。

+ **同步任务**

  同步任务都在主线程上执行，形成一个执行栈。

+ **异步任务**

  JS的异步是通过回调函数实现的。一般而言，异步任务有以下三种类型：

  1. 普通事件，如click、resize等
  2. 资源加载，如load、error等
  3. 定时器，包括setInterval、setTimeout等

  异步任务相关**回调函数**添加到**任务队列**中（任务队列也称为消息队列）

> 19.2一个问题的执行栈和任务队列：

+ 执行栈
  + `console.log(1)`
  + `setTimeout(fn,0)`
  + `console.log(2)`
+ 任务队列
  + `fn`

#### 4.JS执行机制（重要）

1. 先执行执行栈中的同步任务。
2. 异步任务（回调函数）放入任务队列中
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取**任务队列**中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。

![image-20200529150717604](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200529150717604.png)

+ 举例

![image-20200529150737542](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200529150737542.png)



#### 5.事件循环（重要）

![image-20200529151119108](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20200529151119108.png)

**由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为事件循环**



### 二十、location对象

#### 1.什么是location对象

>  window对象给我们提供了一个location属性用于**获取或设置窗体的URL**，并且可以用于**解析URL**。因为这个属性返回的是一个对象，所以我们将这个属性也称为location对象

#### 2.URL

> 统一资源定位符（URL）是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的URL，它包含的信息指出文件的位置以及浏览器应该怎么处理它。

+ URL的一般语法格式为：
  + `protocol://host[:port]/path/[?query]#fragment`
  + `http://www.itcast.cn/index.html?name=andy&age=18#link`

| 组成     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| protocol | 通信协议 常用的http，ftp，maito等                            |
| host     | 主机（域名） `www.itheima.com`                               |
| port     | 端口号，可选，省略时使用方案的默认端口 如http的默认端口为80  |
| path     | 路径 由零或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址 |
| query    | 参数 以键值对的形式，通过&符号分隔开来                       |
| fragment | 片段 #后面内容 常见于链接 锚点                               |

#### 3.location对象的属性

| location对象属性  | 返回值                              |
| ----------------- | ----------------------------------- |
| location.href     | 获取或者设置 整个URL                |
| location.host     | 返回主机（域名） `www.itheima.com`  |
| location.port     | 返回端口号 如果未写返回空字符串     |
| location.pathname | 返回路径                            |
| location.search   | 返回参数                            |
| location.hash     | 返回片段 #后面内容 常见于链接  锚点 |

#### 案例：5秒钟后跳转页面

+ javascript代码

```javascript
var btn = document.querySelector('button');
var div = document.querySelector('div');
btn.addEventListener('click', function() {
    location.href = 'http://www.itcast.cn';
})
var timer = 5;
setInterval(function() {
    if (timer == 0) {
        location.href = 'http://www.itcast.cn';
    } else {
        div.innerHTML = '您将在' + timer + '秒之后跳转到首页';
        timer--;
    }
}, 1000);
```

#### 案例：获取URL参数数据

主要练习数据在不同页面中的传递

+ 案例分析
  1. 第一个登陆页面，里面有提交表单，action提交到index.html页面
  2. 第二个页面，可以使用第一个页面的参数，这样实现了一个数据不同页面之间的传递效果
  3. 第二个页面之所以可以使用第一个页面的数据，是利用了URL里面的location.search参数
  4. 在第二个页面中，需要把这个参数提取。
  5. 第一步：利用`substr`去掉？
  6. 第二步：利用`split('=')`分割键和值。
  7. 第三步：将数据写入div中
+ login.html

```html
<form action="index.html">
    用户名：<input type="text" name="unmae">
    <input type="submit" value="登陆">
</form>
```

+ index.html的JavaScript代码

```javascript
var div = document.querySelector('div');
console.log(location.search);
// 1.先去掉？    substr('起始的位置',截取几个字符)
var params = location.search.substr(1);
// 2. 利用=把字符串分割为数组 split('=')
var arr = params.split('=');
// 3.把数据写入div中
div.innerHTML = arr[1] + '欢迎您';
```

#### 4.location 对象的方法

| location对象方法   | 返回值                                                       |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 跟href一样，可以跳转页面（也称为重定向页面）**可以后退页面** |
| location.replace() | 替换当前页面，因为不记录历史，所以**不能后退页面**           |
| location.reload()  | 重新加载页面，相当于刷新按钮或者 f5 如果参数为true强制刷新 ctrl + f5 |



### 二十一、navigation对象

+ navigator对象包含有关浏览器的信息，它有很多属性，我们最常用的是userAgent，该属性可以由客户机发送服务器的user-agent头部的值。

+ 下面前端代码可以判断用户那个终端打开页面，实现跳转

```javascript
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrower|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))){
    window.location.href = '';  //手机
}else{
    window.location.href = '';  //电脑
}
```



### 二十二、history对象

+ window对象给我们提供了一个history对象，与浏览器历史记录进行交互。该对象包含用户（在浏览器窗口中）访问过的URL。

| history对象方法 | 作用                                                     |
| --------------- | -------------------------------------------------------- |
| back()          | 可以后退功能                                             |
| forward()       | 前进功能                                                 |
| go(参数)        | 前进后退功能 参数如果是1前进1个页面 如果是-1后退一个页面 |

+ history对象一般在实际开发中比较少用，但是会在一些OA办公系统中见到



































































































































































