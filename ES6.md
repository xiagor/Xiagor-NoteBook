## 目录

<!-- TOC -->

- [目录](#目录)
- [export和export  default](#export和export-default)
- [箭头函数](#箭头函数)
- [数组和对象的解构赋值](#数组和对象的解构赋值)

<!-- /TOC -->



## export和export  default

export default、export、import属于es6，前两种都是导出模块，都是向外暴露成员，import是导入模块。

+ export可以向外暴露多个成员，只能使用 { } 的形式来接受（按需导出）

  + 有两种导出模块的方式

    ```js
    // 用法1，变量或者函数要用定义的方式如 var xxx 或者function f(){} ，前面才能接export
    export var firstName = 'Michael';
    export var lastName = 'Jackson';
    export var year = 1958;
    
    // 用法2，先定义变量，最后再用export { } 使用大括号指定所要输出的一组变量。
    var firstName = 'Michael';
    var lastName = 'Jackson';
    var year = 1958;
     
    export { firstName, lastName, year };
    ```

    通常情况下，export输出的变量就是本来的名字，但是可以使用as关键字重命名。

+ import命令后面不需要加大括号

  + 如果一个文件有export导出模块，就可以在另外一个文件用import导入模块（要加花括号）

    ```js
    import {firstName} from './module1';  // 假设上面文件名叫module1.js
    ```

  + 还有模块的整体加载，用星号 （*） 指定一个对象，所有的输出值都加载在这个对象上面

    ```js
    export function area(radius) {
      return Math.PI * radius * radius;
    }
     
    export function circumference(radius) {
      return 2 * Math.PI * radius;
    }
    ```

    import导入上面代码所有值方式

    ```js
    import * as circle from './circle';
     
    console.log('圆面积：' + circle.area(4));
    console.log('圆周长：' + circle.circumference(14));
    ```

+ 其中export default只允许向外暴露一次、而且可以使用任意变量来接收

  + export default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export default命令只能使用一次。所以，**import命令后面才不用加大括号**（指的是对export default文件的import），因为只可能唯一对应export default命令。

> 要区别于exports、module.exports、require（他们是Node.js的导出和导入）



## 箭头函数

1. 函数体内的 this 对象就是定义时所在的对象，而不是使用时所在的对象。

   ​		this对象的指向是可变的，但在箭头函数中它是固定的。this总是指向函数定义生效时所在的对象。箭头函数可以让this指向固定化，这种特性非常有利于封装回调函数。

   ​		this指向的固定化并不是因为箭头函数内部有绑定this的机制，实际原因是**箭头函数根本没有自己的this**，导致内部的this就是外层代码块的this。正是因为它没有this，所以不能用作构造函数。

2. 不可以当作构造函数。也就是说，**不可以使用new**命令，否则会抛出一个错误。

3. 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用rest参数代替。

4. 不可以使用yield命令（ES6的新关键字，使生成器函数执行暂停，yield关键字后面的表达式的值返回给生成器的调用者。），因此箭头函数**不能用作Generator**函数。



## 数组和对象的解构赋值

1. 解构：ES6允许按照一定模式从数组和对象中提取值，然后对变量进行赋值，这被称为解构。

2. 数组的元素是按次序排列的，变量的取值是由它的位置决定的；而对象的属性没有次序，变量必须与属性同名才能取到正确的值。

3. 对象的解构赋值的内部机制是先找到同名属性，然后再赋值给对应的变量。

   ```js
   let { foo: baz } = { foo: "aaa", bar: "bbb" };
   baz // "aaa"
   foo // error: foo is no defined
   ```

   上面的代码中，foo是匹配模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo。

   0+如果foo也要作为变量赋值，可以写成下面这样子：

   ```js
   let { foo, foo: baz }
   // 还有一种类似的
   let obj = {
       p: [
           'hello',
           { y: 'world' }
       ]
   };
   let { p, p: [x, { y }] } = obj;
   x // "hello"
   y // "world"
   p // {"hello", {y:"world"}}
   ```

   

















