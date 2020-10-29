[TOC]



## 第 1 章 什么是JavaScript

JavaScript就是由以下三个部分组成

### 1. ECMAScript

> 在我看来就是一种标准，而Web、Node.js则是实现了该标准



### 2. DOM

> DOM是一个应用编程接口（API），并且DOM将整个页面抽象为一组分层节点。

使用DOM API，可以轻松地删除、添加、替换、修改节点。



### 3. BOM

> 使用BOM，开发者可以操控浏览器显示页面之外的部分。

+ BOM API用于支持访问和操作浏览器的窗口。
+ 在HTML5之前，没有统一的标准，而HTML5以正式规范的形式涵盖了尽可能多的BOM特性。



## 第 2 章 HTML中的JavaScript

JavaScript是通过`<script>`元素插入到HTML页面

### 1. 两种方式：

+ 将js代码嵌入到`script`标签中
+ 使用src属性引用外部js文件的URL
  + **可跨域**，浏览器在解析这个资源的时候，会向src属性指定的URL发送一个GET请求，获取相应资源。（注意：`integrity`属性）
  + 使用src属性后，script标签内的代码会被忽略



### 2. defer和async：

+ defer是推迟执行脚本，异步下载，页面解析完之后再运行

  + HTML5规范是按照顺序执行，在DOMContentLoaded事件之前执行

    > 实际开发中不一定吗？

+ async是异步执行脚本，异步下载，下载完就执行

  + `defer -> async -> DOMContentLoaded ->load` / `defer -> DOMContent -> async -> load`



### 3. 动态加载脚本

```js
let script = document.createElement('script');
script.src = ".....";
document.head.appendChild(script);
```

这种方式创建的script元素默认添加了async属性

> 如果想要设置给同步加载，可以加一句代码`script.async = false;`
>
> 并且要让预加载器知道，需要在文档头部显式声明：`<link rel="preload" href="....">`



## 第 3 章 语言基础

> 过于枯燥？？有点看不下去，先学别的了

### 1. var、let和const

+ var任何版本都能用，const和let只能在ES6及以上用

+ var声明的范围是函数作用域，let和const声明的是块级作用域

+ var声明的变量会自动提升到函数作用域顶部，而let和const不会

+ const声明变量的时候必须同时初始化，并且该变量的引用地址不能变

+ 在**全局作用域**中，var声明的变量会成为window对象的属性，而**let和const都不会**。

  ```js
  var name = "Matt";
  console.log(window.name); //Matt
  
  let age = 16;
  console.log(window.age); //undefined
  ```

+ **for循环中的let声明**

  + var定义的迭代变量：

    ```js
    for (var i = 0;i < 5;i++) {
    	setTimeout(() => {
    		console.log(i);
    	}, 0);
    }
    //实际输出 5 5 5 5 5
    ```

    setTimeout是使用的是 i 退出循环的值：5

  + let定义的迭代变量：

    ```js
    for (let i = 0;i < 5;i++) {
    	setTimeout(() => {
    		console.log(i);
    	}, 0);
    }
    //实际输出 0 1 2 3 4
    ```

    使用 let 声明迭代变量时，JS引擎在后台会为每个迭代循环**声明一个新的迭代变量**。每个 setTimeout 引用的都是不同的变量实例。所以 console.log 输出的是我们期望的值，也就是循环执行过程中每个迭代变量的值。

  + **这种每次迭代声明一个独立变量实例的行为适用于所有风格的 for 循环，包括 for-in 和 for-of 循环。**



### 2. typeof 操作符

`typeof`可以判断七种类型：`undefined`、`boolean`、`string`、`number`、`object`、`function`、`symbol`（表示符号）

> + null本意是对一个空对象的引用，而本身是一种**简单数据类型**，但是调用`typeof null`返回的是object。
>
> + function严格来说也是object，但是由于function的特殊性，typeof会区分来开
>
> + 可以用`instanceof`判断对象的具体类型（不管是父类型还是祖先类型都会返回true）
>
> + 用Object.prototype.toString方法判断会更加准确
>
>   ```js
>   Object.prototype.toString.call(1) // "[object Number]"
>   
>   Object.prototype.toString.call('hi') // "[object String]"
>   
>   Object.prototype.toString.call({a:'hi'}) // "[object Object]"
>   
>   Object.prototype.toString.call([1,'a']) // "[object Array]"
>   
>   Object.prototype.toString.call(true) // "[object Boolean]"
>   
>   Object.prototype.toString.call(() => {}) // "[object Function]"
>   
>   Object.prototype.toString.call(null) // "[object Null]"
>   
>   Object.prototype.toString.call(undefined) // "[object Undefined]"
>   
>   Object.prototype.toString.call(Symbol(1)) // "[object Symbol]"
>   
>   ```
>
>   



### 3. 数据类型

1. Undefined类型

   只有一个值undefined

2. Null 类型

   只有一个值null，逻辑上表示一个空对象指针。

3. Boolean 类型

   两个字面值：true 和 false。

   + Boolean()：传一个参数，把该参数转换为Boolean类型的函数

   + 不同类型与布尔值之间的转换规则：

     | 数据类型  | 转换为true的值 | 转换为false的值 |
     | --------- | -------------- | --------------- |
     | Boolean   | true           | false           |
     | String    | 非空字符串     | ""              |
     | Number    | 非零数值       | 0，NaN          |
     | Object    | 任意对象       | null            |
     | Undefined |                | undefined       |

4. Number 类型

   整数、浮点数和NaN（Not a Number）

   + NaN不等于任何数，包括自己NaN
   + isNaN()：传一个参数，函数尝试转换该参数为数值，不能转换成功的该函数返回true，否则为false。
   + Number()：传一个参数，函数转换该参数为数值或者NaN。（包含类型转换）
   + parseInt()：传一个参数，String和Number类型以外的都返回NaN；从第一个非空格字符开始转换，碰到非数值字符就结束并返回前面的数值（如果第一个就是非数值字符就返回NaN）
   + parseFloat()：和parseInt类型，但是解析到第一个小数点会有效，继续解析，第二个小数点出现就无效了

5. String 类型

   零个或多个16位Unicode字符序列。

   + 可以使用双引号（""）、单引号（''）或反引号（``）表示

   + toString()：不传参，可以把数值、布尔值、对象和字符串值转换为字符串。（null和undefined没有该方法）

   + String()：传一个参数，返回该参数的字符串类型的值

   + **模版字面量**要使用反引号（``），支持字符串插值。如

     ```js
     let name = "xiagor";
     console.log(`my name is ${name}`);
     ```

6. Symbol 类型

   > 符号？不是很懂这个类型的作用

7. Object 类型

   对象，一组数据和功能的集合。

   + 每个Object实例都有如下属性和方法：
     + constructor：指向创建当前对象的构造函数
     + hasOwnProperty(*propertyName*)：用于判断当前**对象实例**（而不是从原型上继承的）上是否存在给定的属性
     + isPrototypeof(*object*)：判断当前对象是否为另一个对象的原型
     + propertyIsEnumerable(*propertyName*)：判断给定的属性是否可以使用
     + toLocaleString()：返回对象的字符串表示。反映对象所在的本地化执行环境？？？
     + toString()：返回对象的字符串表示。
     + valueOf()：返回对象对应的字符串、数值或布尔值表示。？？？



> 第三章到操作符，不往下写了...看面筋的时候学习再会来补充笔记

