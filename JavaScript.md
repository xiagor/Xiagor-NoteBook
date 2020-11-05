[TOC]



## 在JavaScript中实现AOP

1. 问题场景：

   + 在方法开始的时候校验参数
   + 执行方法前检查权限
   + 删除前给出确认提示等等

   在这些问题中，不同的方法规则可能相同，每个方法前去调用显得麻烦，而且不利于统一管理，于是就有了面向切面编程（AOP）

2. 好处：

   1. 保证业务逻辑模块的纯洁和高内聚性
   2. 方便的复用日志统计模块

> **JS实现AOP，都是只把一个函数“动态织入”到另一个函数之中**

3. 代码实现：

   ```javascript
   // 主方法执行前的调用
   Function.prototype.before=function(beforefn){
       var self=this;//保存原函数的引用
       return function(){//返回包含了原函数和新函数的“代理”函数
           beforefn.apply(this,arguments);//执行新函数，修正this
           //（对下面例子的解释：就是在这里执行了需要在主方法执行前调用的beforefn函数，这里的this就是下面var ret=self.apply(this,arguments)传进来的this）
           return self.apply(this,arguments);//执行原函数（主方法）
       }
   }
   
   // 主方法执行完后的调用
   Function.prototype.after=function(afterfn){
       var self=this;//保存原函数的引用
       return function(){//返回包含了原函数和新函数的“代理”函数（返回的这个function就是下面的fn函数了！）
           var ret=self.apply(this,arguments);//执行原函数（就是在这里执行了上面before返回的funtion函数，并且让该函数的this指向改成fn的调用者即window对象）
           afterfn.apply(this,arguments);//执行新函数，修正this（window对象）
           return ret;// undefined，没啥意义
       }
   }
   
   // 下面是使用的具体例子
   // 主方法myFun
   var myFun=function(){
       console.log("myFun");
   }
   
   //myFun要调用before和after函数
   //before传入的函数参数会在myFun执行前调用
   //after传入的函数参数会在myFun执行后调用
   fn=myFun.before(function(){
       console.log("before");
   }).after(function(){
       console.log("after");
   });
   
   fn();
   ```

 

## JS判断数组的的五种方法

### 1. instanceof关键字

`arr instanceof Array`

`实例 instanceof 构造函数`



### 2. 实例arr的原型属性`__proto__`和构造函数Array的原型对象`prototype`相等

`arr.__proto__ === Array.prototype`



### 3. constructor

+ 实例对象可以通过`__proto__`访问到构造函数的原型对象`Array.prototype`（正如第二点，他们就是相等的），即也可以继承到`Array.prototype.constructor`（指回Array）

`arr.constructor === Array`

> 这里的arr.constructor实际上是`arr.__proto__.constructor`



### 4. 使用Object.prototype的tostring方法

`Object.prototype.toString() === '[object Object]'`

`Object.prototype.toString.call(arr) === '[object Array]'`

> 注意第二个的toString后面没有 () ，因为call改变前面方法的this指向的同时还会自动执行方法（bind不会）
>
> call传递的参数是实例数组arr，后面的Object就会改成Array



### 5. Array.isArray()，返回boolean值

`Array.isArray(arr) === true`



## arguments对象

### 1. 概念和定义

> 一个对应于传递给函数的参数的**类数组对象**，是所有（非箭头）函数中都可用的局部变量。

此对象包含传递给函数的每个参数（我的理解就是，**包含了调用函数时传入的实参**，不管该函数定义时有无形参）

1. 它不是一个Array，它类似Array，但除了length属性和索引元素之外没有任何Array属性。
2. `arguments.__proto__ === Object.prototype`，由此我是理解arguments的构造函数是Object
3. `Object.prototype.toString.call(arguments) === '[object Arguments]'`

> 对3里面的Object的原型对象prototype的toString方法其实我还不是很理解，是依据什么去变成字符串的呢？



### 2. 例子

#### 1）遍历参数求和

```javascript
function add() {
    var sum =0,
        len = arguments.length;
    for(var i=0; i<len; i++){
        sum += arguments[i];
    }
    return sum;
}
add()                           // 0
add(1)                          // 1
add(1,2,3,4);                   // 10
```

#### 2）定义连接字符串的函数

```javascript
function myConcat(separator) {
  var args = Array.prototype.slice.call(arguments, 1);
  return args.join(separator);
}

// returns "red, orange, blue"
myConcat(", ", "red", "orange", "blue");

// returns "elephant; giraffe; lion; cheetah"
myConcat("; ", "elephant", "giraffe", "lion", "cheetah");

// returns "sage. basil. oregano. pepper. parsley"
myConcat(". ", "sage", "basil", "oregano", "pepper", "parsley");
```

详情更多查看 [Arguments 对象 - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)



## JS数组降维（扁平化数组）

### 1. 二维数组降为一维数组

#### 1）循环降维（菜鸡）

```javascript
let children = [1, 2, 3, [4, 5, 6], 7, 8, [9, 10]];
function simpleNormalizeChildren(children) {
  let reduce = [];
  for (let i = 0; i < children.length; i++) {
    if (Array.isArray(children[i])) {
      for (let j = 0; j < children[i].length; j++) {
        reduce.push(children[i][j]);
      }
    } else {
      reduce.push(children[i]);
    }
  }
  return reduce;
}
simpleNormalizeChildren(children) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

> 双重循环遍历再push进新数组，效率低下，菜鸡

#### 2）concat降维（还行）

```javascript
let children = [1, 2, 3, [4, 5, 6], 7, 8, [9, 10]];
function simpleNormalizeChildren(children) {
  let reduce = [];
  for (let i = 0; i < children.length; i++) {
    reduce = reduce.concat(children[i]);
  }
  return reduce;
}
simpleNormalizeChildren(children) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```

+ `concat()`如果参数是一个元素，该元素会被直接插入到新数组中；如果参数是一个数组，会自己将该数组的各个元素插入到复制的新数组的后面

> 利用concat方法，把双重循环简化为单重循环

#### 3）apply和concat降维（牛逼！）

```javascript
let children = [1, 2, 3, [4, 5, 6], 7, 8, [9, 10]];
function simpleNormalizeChildren(children) {
  return Array.prototype.concat.apply([], children);
}
simpleNormalizeChildren(children) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

+ `apply()`的**第一个参数**会作为**被调用函数的this值**，**第二个参数（一个数组，或类数组的对象arguments）**会作为**被调用对象的arguments值**，也就是说该数组的各个元素将会依次成为被调用函数的各个参数！
+ 这么理解：
  + 利用apply第二个参数是数组的特性
  + 即把children数组的7个元素：`1, 2, 3, [4, 5, 6], 7, 8, [9, 10]`，作为`concat()`的参数
  + 即`concat(1, 2, 3, [4, 5, 6], 7, 8, [9, 10])`
  + 再利用`concat`方法的特性，再次降维，参数的数组中的每一个子元素都会被独立插入进型数组。
  + 新数组就是一维数组了！



### 2. 多维数组降为一维数组

```javascript
// 多维数组
let children = [1, [2,3], [4, [5, 6, [7, 8]]], [9, 10]];
function simpleNormalizeChildren(children) {
  for (let i = 0; i < children.length; i++) {
    if (Array.isArray(children[i])) {
      children = Array.prototype.concat.apply([], children);
      for(let j =0; j<children.length; j++) {
        simpleNormalizeChildren(children)
      }
    }
  }
  return children;
}
simpleNormalizeChildren(children); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

> 我在chorme调试过代码，发现上面的方法每次递归一次都要进行一次双重循环，非常消耗资源
>
> 但是上面的递归方法是可行的，不知道还有没有别的方法，有空可以看看了解一下



## Array.from()（ES6）

> 从一个**类似数组**或**可迭代对象**创建一个新的，浅拷贝的数组实例

+ 类似数组：拥有一个 `length` 属性和若干索引属性的任意对象（应该是类数组对象arguments吧？不知道还有没有别的类似的对象）
+ 可迭代对象：可以获取对象中的元素,如 Map和 Set 等



### 1. 语法

```javascript
Array.from(arrayLike[, mapFn[, thisArg]])
```

+ 参数：

  + `arrayLike`

    想要转换成数组的伪数组对象或可迭代对象。

  + `mapFn` 可选

    如果指定了该参数，新数组中的每个元素会执行该回调函数。

  + `thisArg` 可选

    可选参数，执行回调函数 `mapFn` 时 `this` 对象。

+ 返回值

  一个新的数组实例！

> 在 ES2015 中， `Class` 语法允许我们为内置类型（比如 `Array`）和自定义类新建子类（比如叫 `SubArray`）。这些子类也会继承父类的静态方法，比如 `SubArray.from()`，调用该方法后会返回子类 `SubArray` 的一个实例，而不是 `Array` 的实例。



### 2. 示例

#### 1）从 `String` 生成数组

```javascript
Array.from('foo'); 
// [ "f", "o", "o" ]
```

#### 2）从 `Set` 生成数组

```js
const set = new Set(['foo', 'bar', 'baz', 'foo']);
Array.from(set);
// [ "foo", "bar", "baz" ]
```

#### 3）从 `Map` 生成数组

```js
const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map);
// [[1, 2], [2, 4], [4, 8]]

const mapper = new Map([['1', 'a'], ['2', 'b']]);
Array.from(mapper.values());
// ['a', 'b'];

Array.from(mapper.keys());
// ['1', '2'];
```

#### 4）从类数组对象（arguments）生成数组

```js
function f() {
  return Array.from(arguments);
}

f(1, 2, 3);

// [ 1, 2, 3 ]
```

#### 5）在 `Array.from` 中使用箭头函数

```js
// Using an arrow function as the map function to
// manipulate the elements
Array.from([1, 2, 3], x => x + x);
// [2, 4, 6]


// Generate a sequence of numbers
// Since the array is initialized with `undefined` on each position,
// the value of `v` below will be `undefined`
Array.from({length: 5}, (v, i) => i);
// [0, 1, 2, 3, 4]
```

#### 6）数组去重合并

```javascript
function combine(){ 
    let arr = Array.prototype.concat.apply([], arguments);  // 详情看JS数组降维
    return Array.from(new Set(arr));
} 

var m = [1, 2, 2], n = [2,3,3]; 
console.log(combine(m,n));                     // [1, 2, 3]
```

+ apply第二个参数可以是数组或者类数组对象，这里传的是类数组对象（利用了apply的特性来降维）
+ 这里的类数组对象arguments为`{[1, 2, 2], [2, 3, 3]}`（好像不是这样写的，为了区分数组我姑且这样写）
+ 此时`Array.prototype.concat.apply([], arguments)`就变成了`concat([1, 2, 2], [2, 3, 3])`
+ `arr = [1, 2, 2, 2, 3, 3] `

更多详情参考MDN文档：[Array.from() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)



## 回调函数

回调函数具体的定义为：函数A作为参数(函数引用)传递到另一个函数B中，并且这个函数B执行函数A。

> 回调和同步异步应该没啥关系，感觉就是为了解耦要调用的函数，该同步的还是同步，该异步的还是要放在EventLoop，等主线程执行完再按顺序调用执行



## 闭包

> 闭包就是能够读取其他函数内部变量的函数，在本质上，闭包是将函数内部和函数外部连接起来的桥梁。

+ 创建闭包的最常见的方式就是在一个函数内创建另外一个函数，它涉及到作用域链的创建。（闭包的底层运行机制）
+ 闭包的用途：
  1. 为了读取函数内部的变量。因为在闭包函数中会引用父函数的作用域对象，可以在函数外部通过闭包函数，从而访问到函数内部的变量。
  2. 让这些变量的值始终保存在内存中。因为在闭包函数中会引用父函数的作用域对象，使得函数执行结束后，变量不会被垃圾回收机制回收。（但是这样容易造成内存泄漏，解决办法是用完的时候让变量指向null）



## 事件

> JavaScript与HTML之间的交互就是通过事件实现的。
>
> 事件，就是文档或者浏览器窗口中发生的一些特定的交互瞬间。或者说是用户或浏览器自身执行的某种动作。

常见的事件：

| 事件        | 描述                         |
| :---------- | :--------------------------- |
| onchange    | HTML 元素已被改变            |
| onclick     | 用户点击了 HTML 元素         |
| onmouseover | 用户把鼠标移动到 HTML 元素上 |
| onmouseout  | 用户把鼠标移开 HTML 元素     |
| onkeydown   | 用户按下键盘按键             |
| onload      | 浏览器已经完成页面加载       |









##  隐式转换类型

#### 1. 隐式转换类型规则

1. 转成string类型： + （字符串连接符，只要有一边是string就是字符串连接符）
2. 转成number类型： ++/--(自增自减运算符) 、+-*/%(算术运算符)、><等（关系运算符）
3. 转成boolean类型：! （逻辑非运算符）

#### 2. 坑一：字符串连接符与算术运算符隐式转换规则混淆

```javascript
console.log(1 + "true");//"1true"
console.log(1 + true);//Number(true) = 1
console.log(1 + undefined);//Number(undefined) = NaN
console.log(1 + null);//Number(null) = 0
```

#### 3. 坑二：关系运算符：会把其他数据类型转换成number之后再比较关系

```javascript
console.log("2">10);
//有一边是Number类型，另一边直接用Number("2") = 2。
//注：Number("a") = NaN

console.log("2">"10");
//两边都是String类型，不是用Number()的形式转换数字，而是用字符串对应的unicode编码来转换数字
//查看字符的unicode编码方法：string.charCodeAt(index)。index为字符下标，默认为0
//"2".charCodeAt() = 50
//"10".charCodeAt() = 49

console.log("abc">"b");//"a"的unicode比"b"的小，false
console.log("abc">"aad");//两边第一个a相等，比较第二个，从左往右依次比较
console.log(NaN == NaN);//特殊情况：NaN 永远不等于自己
console.log(undefined == null);//特殊情况：undefined == null 为 true
//undefined的类型就是undefined，null的类型是object（历史遗留问题）
```

#### 4. 坑三：复杂数据类型在隐式转换时会先转成String，然后再转成Number运算

```javascript
// 如何完善a，使其正确打印1
var a = ?
if(a == 1 && a==2 && a==3) {
	console.log(1);
}
// 如果a是数组/对象这类复杂数据类型，在隐式转换的时候：
// 1. 会先用valueOf()方法获取其原始值，如果原始值不是number类型，则使用toString()转换成string
// 2. 再将string转换成number运算

// 复杂类型数据会先自动调用valueOf()方法，然后转成number运算，而对象的valueOf()方法是可以重写的
a = {
    i: 0;
    valueOf: function(){
        return ++a.i;
    }
	//重写前:a.valueOf().toString()==="[object Object]"
	//重写后:a.valueOf().toString()==="1"
}
```



![img](Images/JavaScript%E7%AC%94%E8%AE%B0/1538025621414c490c46b28)

#### 5. 坑四：逻辑非隐式转换与关系运算符隐式转换搞混淆(巨坑)

![js面试题大坑——隐式类型转换](http://p9.pstatp.com/large/pgc-image/153802573916560e7c21b31)

1. 逻辑非"!"可以将其它数据类型使用Boolean()转成布尔类型

   + 以下八种情况转换为布尔类型会得到false：

     0、-0、NaN、undefined、null、''（空字符串）、false、document.all()

   + 除以上八种情况之外，其他所有数据都会得到true

2. 数组和对象转换类型：

   ```javascript
   [].valueOf.toString()//'' 空字符串
   {}.valueOf.toString()//"[object Object]"
   ```

3. `console.log([]==0)`为true

   + 0是number类型，所以[]要转换成number类型
   + [].valueOf.toString() 会得到空字符串（即是八种情况之一，布尔类型为false），再转换成Number类型为0

4. `console.log(![]==0)`为true

   + 0是number类型，所以![]要转换成number类型
   + ![]有逻辑非!，且[]不是八种情况之一，[]为true，![]为false
   + false转换为Number类型为0

5. `console.log(![]==[])`为true

   + 同上，![]转换为false，[]也转换为false

6. `console.log([]==[])`为false

   + 引用类型数据存在堆中，栈中存储的是地址，这两个[]空数组的地址肯定不一样，所以他们的结果为false

7. `console.log({}=={})`为false

   + 同上

8. `console.log(!{}=={})`为false

   + !{}有逻辑非!，且{}不是八种情况之一，{}为true，!{}为false
   + {}.valueOf.toString()得到字符串"[object Object]"，再转换成Number类型为NaN



![js面试题大坑——隐式类型转换](Images/JavaScript%E7%AC%94%E8%AE%B0/1538025911178e28d7c85c1)





## String方法

### 1. 字符方法

#### 1）charAt()

接收一个字符位置的参数，以单字符字符串的形式返回该位置的字符。

```js
var stringValue = "hello world";
console.log(stringValue.charAt(1));		//'e'
```



#### 2）charCodeAt()

接收一个字符位置的参数，以单字符字符串的形式返回该位置的字符**的字符编码**。

```js
var stringValue = "hello world";
console.log(stringValue.charAt(1));		//'101'
```



#### 3）ES5访问个别字符的方法

使用方括号加数字索引访问

> IE7及更早版本不支持

```js
var stringValue = "hello world";
console.log(stringValue[1]);		//'e'
```



### 2. 字符串操作方法

> 都是返回一个新的字符串

#### 1）concat()

拼接字符串的，建议直接用 + 拼接。

#### 2）slice()、substr()、substring()

| 方法        | 参数一（必需）     | 参数二（可选）                               | 参数一为负值时                      | 参数二为负值时 |
| ----------- | ------------------ | -------------------------------------------- | ----------------------------------- | -------------- |
| slice()     | 子字符串的开始位置 | 子字符串结束位置（不包括），默认到字符串末尾 | 负值+length                         | 负值+length    |
| substr()    | 子字符串的开始位置 | 字符个数，默认到字符串末尾                   | 负值+length                         | 0              |
| substring() | 子字符串的开始位置 | 子字符串结束位置（不包括），默认到字符串末尾 | 0（该方法会以较小的数作为开始位置） | 0              |



### 3. 字符串位置方法

#### 1）indexOf()、lastIndexOf()

+ 参数一（必需）：需要查找的子字符串
+ 参数二（可选）：从字符串哪个位置开始查找
+ 返回值：子字符串第一次出现的下标值，没有则返回-1
+ 区别：
  + indexOf：是从字符串的开头开始查找
  + lastIndexOf：是从字符串的末尾向前查找

#### 2）查找所有出现过的字符串的方法

```js
var stringValue = "helloworlodijjkslhkguuhghlkddfljkdjag";
var position = new Array();
var pos = stringValue.indexOf('l');

while (pos > -1) {
    position.push(pos);
    pos = stringValue.indexOf('l', pos + 1);
}

console.log(position);
```



### 4. trim()删除前后空格

删除前置及后缀的所有空格，返回一个字符串的副本，不会改变原字符串。



### 5. 字符串大小写转换方法

+ toLowerCase()：字符串转换为小写，无传参
+ toUpperCase()：字符串转换为大写，无传参



### 6. 字符串的模式匹配方式

#### 1）match()

+ 参数为一个正则表达式或者一个RegExp对象
  + 当参数是一个字符串或一个数字，它会使用new RegExp(obj)来隐式转换成一个 [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp)
+ 返回一个数组
  + 如果正则表达式是非全局，例如`/.at/`，返回的数组除了有一个匹配到的字符串，还有`index`、`input`、`groups`属性
  + 如果正则表达式是全局，例如`/.at/g`，返回一个正常的数组，从左到右存放匹配到的所有字符串。

```js
var text = "cat, bat, sat, fat";
var pattern1 = /.at/;
var pattern2 = /.at/g;

//pattern 是 RegExp对象的实例
console.log(pattern2.__proto__ === RegExp.prototype);	//true


var matches1 = text.match(pattern1);
var matches2 = text.match(pattern2);
console.log(matches1);
// ["cat", index: 0, input: "cat, bat, sat, fat", groups: undefined]
console.log(matches2);
// ["cat", "bat", "sat", "fat"]
```

#### 2）search()

+ 参数为一个正则表达式或者一个RegExp对象
  + 当参数是一个字符串或一个数字，它会使用new RegExp(obj)来隐式转换成一个 [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp)
+ 返回正则表达式在字符串中首次匹配项的索引，否则返回-1。

#### 3）replace()

> ```js
> str.replace(regexp|substr, newSubStr|function)
> ```

+ 第一个参数
  + regexp：一个正则表达式或者RegExp对象，该正则所匹配的内容会被第二个参数的返回值（指函数的返回值）替换掉
  + substr：一个字符串，其被视为一整个字符串，而不是一个正则表达式，仅第一个匹配项会被替换掉
+ 第二个参数
  + newSubStr：用于替换掉第一个参数匹配部分的字符串。（该字符串可以**内插一些特殊的变量名**）
  + function：该函数的返回值将替换掉第一个参数匹配到的结果。
+ 返回值
  + 一个替换好的新的字符串

#### 4）split()

```js
str.split([separator[, limit]])
```

+ separator：指定表示每个拆分应发生的点的字符串。`separator` 可以是一个字符串或[正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)。

  如果在str中省略或不出现分隔符，则返回的数组包含一个由整个字符串组成的元素。

  如果分隔符为空字符串，则将str原字符串中**每个字符**的数组形式返回。（就是每个字符都被分开了）

+ limit：一个整数，限定返回的分割片段数量。



## new的时候发生了什么

> new表达式是配合构造函数使用，用来创建对象。（还有一个创建对象的方式是对象字面量）

```js
function O(name){
	this.name = name;
}
var o = new O('虾哥');
```

在使用new操作符来调用一个构造函数的时候，发生了四件事：

```js
var obj = {};
obj.__proto__ = O.prototype;
O.call(obj);
return obj;
```

1. 创建一个空对象obj
2. 将这个空对象的`__proto__`成员指向了构造函数对象的prototype成员对象，这是最关键的一步
3. 将构造函数的作用域赋给新对象，因此O函数中的this指向新对象obj，然后再调用O函数。于是我们就给obj对象赋值了一个成员变量name，这个成员变量的值是"虾哥"。（其实这里应该还有arguments的解构赋值的，具体参考[点击该文章](https://www.jianshu.com/p/9bf81eea03b2)）
4. **返回新对象obj**。但如果构造函数包含返回值：
   + 返回值必须是this对象、或者是其他非对象类型的值
   + 如果返回值是引用类型（如对象、数组、函数等），则new出来的对象就会被返回的引用类型值给替换了。



## 防抖和节流

### 1. 防抖debounce

> 通俗理解：函数防抖就是法师发技能的时候要读条，技能读条没完再按技能就会重新读条。

1. 思路：**在第一次触发事件时，不立即执行函数，而是给出一个期限值比如200ms**，然后：

   + 如果在200ms内没有再次触发滚动事件，那么就执行函数
   + 如果在200ms内再次触发滚动事件，那么当前的计时取消，重新开始计时

2. 效果：如果短时间内大量触发同一事件，只会执行一次函数。

3. 实现：既然前面都提到了计时，那实现的关键就在于`setTimeout`这个函数，由于还需要一个变量来保存计时，考虑维护全局纯净，可以借助闭包来实现：

   ```js
   // 防抖：触发不会立马执行，delay时间内不触发的话，到时间就执行，否则重新计时
   function debounce(fn, delay) {
       let timer = null;
   
       return function () {
           if (timer) {
               // 如果当前正在计时中，要把原来的计时器关掉，再重新计时，以防重复触发计时器
               clearTimeout(timer);
           }
           timer = setTimeout(fn, delay);
       }
   }
   
   let trigger = () => {
       console.log('trigger');
   }
   
   window.addEventListener('resize', debounce(trigger, 1000));
   ```

   

### 2. 节流throttle

> 通俗理解：函数节流就是fps游戏的射速，就算一直按着鼠标射击，也只会在规定射速内射出子弹。

1. 思路：**在第一次触发事件时，不立即执行函数，而是给出一个期限值比如200ms开始计时，并且给标志位设置为false**，然后：

   + 如果在200ms内再次触发滚动事件，标志位为false，不做任何反应。
   + 200ms事件到了以后标志位就随同函数的执行变为true。
   + 如果在200ms以后再次触发滚动时间，给标志位设置为false并开始计时。

2. 效果：如果短时间内大量触发同一事件，那么**在函数执行一次之后，该函数在指定的时间期限内不再工作**，直至过了这段时间才重新生效。

3. 这里借助`setTimeout`来做一个简单的实现，加上一个状态位`valid`来表示当前函数是否处于工作状态：

   ```js
   // 节流：触发就开始计时，计时delay的时候触发不会重复执行，时间到了就执行函数并开放可触发
   function throttle(fn, delay) {
       let valid = true;
       return function () {
           if (!valid) {
               // 当还没计时，此时valid为true，不会走进来，就会走到下面的valid = false并触发计时
               // 在计时过程中，valid一直为false，如果又被触发，就会走进来这里
               return false;
           }
           // 能走到这里说明 没有计时或者计时已经完成并把valid设置为true了
           valid = false;
           setTimeout(() => {
               fn();
               valid = true; // 时间到了，又可以被触发了
           }, delay);
       }
   }
   
   window.addEventListener('resize', throttle(trigger, 2000));
   ```



### 3. 应用场景举例

1. 搜索框input事件，例如要支持输入实时搜索可以使用**节流**方案（间隔一段时间就必须查询相关内容），或者实现输入间隔大于某个值（如500ms），就当做用户输入完成，然后开始搜索，具体使用哪种方案要看业务需求。
2. 页面resize事件，常见于需要做页面适配的时候。需要根据最终呈现的页面情况进行dom渲染（这种情形一般是**使用防抖**，因为只需要判断最后一次的变化情况）



## 立即执行函数

> 在红宝书中的定义：**立即调用的匿名函数**又被称做立即调用的函数表达式（IIFE）。
>
> 它类似于函数声明，但由于被包含在括号中，所以会被解释为函数表达式。紧跟在第一组括号后面的第二组括号会立即调用前面的函数表达式。

+ 在ECMAScript5.1及以前，为了防止变量定义外泄，IIFE是个非常有效的方法，在ES6以后，IIFE就没那么必要了，因为let就可以实现同样的隔离。给一个例子：
    ```js
    let divs = document.querySelectorAll('div');
    
    //达不到目的！每次点击都是输出divs.length的值而不是对应的i
    for(var i = 0; i < divs.length; ++i){
        divs[i].addEventListener('click', function(){
            console.log(i);
        });
    }
    ```

+ IIFE的写法：

    ```js
    let divs = document.querySelectorAll('div');
    
    for (var i = 0; i < divs.length; ++i) {
        // 里面的方法放入一个匿名函数中并且立即调用，这样相当于for循环的每个匿名函数都对应一个i（给匿名函数传参传进去的），类似块级作用域
        (function (i) {
            divs[i].addEventListener('click', function () {
                console.log(i);
            });
        })(i);
    }
    ```

+ ES6的let写法 ：（很简单）
    ```js
    let divs = document.querySelectorAll('div');

    for (let i = 0; i < divs.length; ++i) {
        divs[i].addEventListener('click', function () {
            console.log(i);
        });
    }
    ```

所以总的来看：

1. 立即执行函数一般都是匿名函数的立即调用，具体使用方法可以看上面的例子。

2. 立即执行函数是ES6的let之前的实现方法，但是很麻烦。

3. 立即执行函数和闭包没有半毛钱关系，要说有关系的话，那就是立即执行函数用的是匿名函数，而闭包一般返回的函数也是匿名函数

   ```js
   // 匿名函数的形式
   function (){
   	//....上面没有函数名
   } 
   ```

   

## 回调地狱及解决方法

> 前端的ajax和jsonp内部充斥着大量的异步，为了能够拿到异步的数据，使用了大量的回调函数，来获取将来异步执行成功之后的数据。如果请求不多时还好，一旦请求的数量达到一定程度，并且复杂度提升以后，会造成一些问题，这就是回调地狱。

```js
//开启三个异步的程序，要求能同时拿到所有异步的结果，下边就是用回调地狱方式解决的例子
 ajax({
     url:"http://localhost/promise/data/d1.php",
     success:function(res1){
         console.log(res1);
         ajax({
             url:"http://localhost/promise/data/d2.php",
             success:function(res2){
                 console.log(res2);
                 ajax({
                   url:"http://localhost/promise/data/d3.php",
                    success:function(res3){
                       console.log(res3);
                       console.log(res1, res2, res3);
                     }
                 })
             }
         })
     }
 })

```

### 1. 回调地狱的缺点

+ 上边的例子用回调地狱能解决问题，但是有缺点，或者说不优雅。
+ 如果最里面的异步没有执行结束，外面所有的程序是不是都相当于没有结束，有点递归的影子，非常消耗性能。
+ 格式非常不优雅，语义化非常差，不方便调错。

### 2. 回调地狱的解决方法

#### 1）Promise解决（ES6）

```js
// Promise的格式
var p = new Promise(function(a,b){
	// 正在执行....
	// 此处放置异步的程序
	// a就是在then中的第一个回调函数，表示成功要做的事情
	// b就是在catch中的第一个回调函数，表示失败要做的事情
});
p.then(function(){
	// 成功的预置函数
});
p.catch(function(){
	// 失败的预置函数
});
```

+ 用Promise和ajax解决回调地狱：

    ```js
     var p1 = new Promise(function(resolve){
         ajax({
             url:"http://localhost/promise/data/d1.php",
             success:function(res1){
                 resolve(res1);
             }
         })
     })
     var p2 = new Promise(function(resolve){
         ajax({
             url:"http://localhost/promise/data/d2.php",
             success:function(res2){
                 resolve(res2);
             }
         })
     })
     var p3 = new Promise(function(resolve){
         ajax({
             url:"http://localhost/promise/data/d3.php",
             success:function(res3){
                 resolve(res3);
             }
         })
     })

     p1.then(function(r1){
         console.log(r1);
         return p2;
     }).then(function(r2){
         console.log(r2);
         return p3;
     }).then(function(r3){
         console.log(r3);
     }
    ```
    
+ promise的封装

    ```js
    // ajax函数自身执行的时候不再接收成功和失败的处理函数了
    // 交给ajax内部封装的promise处理
    function ajax(ops){
        ops.type = ops.type || "get";
        ops.data = ops.data || {};
        var str = "";
        for(var key in ops.data){
            str += `${key}=${ops.data[key]}&`;
        }
        if(ops.type=="get"){
            let t = new Date().getTime();
            ops.url = ops.url + "?" + str + "__qft="+ t;
        }
        var xhr = new XMLHttpRequest();
        xhr.open(ops.type, ops.url);
        if(ops.type == "get"){
            xhr.send();
        }else{
            xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
            xhr.send(ops.data);
        }
        return new Promise(function(resolve,reject){
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4 && xhr.status === 200){
                    resolve(xhr.responseText);
                }else if(xhr.readyState === 4 && xhr.status !== 200){
                    reject("当前请求失败了，失败的原因是：" + xhr.status);
                }
            }
        })
    }
    ```

+ 当前ajax封装完成之后的调用方式

    ```js
    // 当前ajax封装完成之后的调用方式：
     var p1 = ajax({
         type:"get",
         url:"",
         data:{
             user:"admin",
             pass:123
         }
     })
     p1.then(function(res){
         console.log(res)
     })
     p1.catch(function(res){
         console.log(res)
     })
    ```

    

#### 2）async/await解决（ES7）

+ 在Promise的基础上，再使用async/await

  ```js
  //语法
  async function fn(){
    var res1 = await new Promise(....)
  
    var res2 = await new Promise(....)
  
    var res3 = await new Promise(....)
  
    var res4 = await new Promise(....)
  
    console.log(res1,res2,res3,res4);
   }
  ```

+ async/await解决地狱回调

  ```js
      async function fn(abc){
          var p1 = await ajax({
              url:"http://localhost/async-await/data/d1.php"
          });
          
          var p2 = await ajax({
              url:"http://localhost/async-await/data/d12312.php"
          });
  
          var p3 = await ajax({
              url:"http://localhost/async-await/data/d3.php"
          });
          
          var p3 = await ajax({
              url:"http://localhost/async-await/data/d3.php"
          });
          
          var p3 = await ajax({
              url:"http://localhost/async-await/data/d3.php"
          });
  
          console.log(p1, p2, p3);
  
          console.log(abc);
      }
  
      document.onclick = function(){
          fn("hello world");
      }
  ```



#### 3）generator

+ generator是es6中的一个新的语法。在function关键字后添加*即可将函数变为generator。

+ generator函数有一个最大的特点，可以在内部执行的过程中交出程序的控制权，yield相当于起到了一个暂停的作用；而当一定情况下，外部又将控制权再移交回来。

+ 用generator来封装代码，在异步任务处使用yield关键词，此时generator会将程序执行权交给其他代码，而在异步任务完成后，调用next方法来恢复yield下方代码的执行。

+ 以readFile为例，大致流程如下：

  ```js
  // 我们的主任务——显示关键字// 使用yield暂时中断下方代码执行// yield后面为promise对象
  const showKeyword = function* (filepath) {
      console.log('开始读取');
      let keyword = yield readFile(filepath);
      console.log(`关键字为${filepath}`);
  }
  // generator的流程控制
  let gen = showKeyword();
  let res = gen.next();
  res.value.then(res => gen.next(res));
  ```




## 正则表达式字符匹配

> 正则表达式是匹配模式，要么匹配字符、要么匹配位置。

### 1. 两种模糊匹配

#### 1）横向模糊匹配

> 横向模糊指的是，一个正则可匹配的字符串的长度不是固定的，可以是多种情况的。

+ 实现方式：使用量词，譬如`{m,n}`，表示连续出现最少m次，最多n次

```js
var regex = /ab{2,5}c/g;
var string = "abc abbc abbbc abbbbc abbbbbc abbbbbbc";
console.log( string.match(regex) ); 
// => ["abbc", "abbbc", "abbbbc", "abbbbbc"]
```

#### 2）纵向模糊匹配

> 纵向模糊指的是，一个正则匹配的字符串，具体到某一位字符时，它可以不是某个确定的字符，可以有多种可能。

+ 实现方式：使用字符组，譬如`[abc]`，表示该字符可以是"a","b","c"中的任意一个。

```js
var regex = /a[123]b/g;
var string = "a0b a1b a2b a3b a4b";
console.log( string.match(regex) ); 
// => ["a1b", "a2b", "a3b"]
```



### 2. 字符组

> 虽然叫字符组，但只是其中一个字符，例如`[abc]`，**表示匹配一个字符**，可以是"a","b","c"中的任意一个。

1. 范围表示法

   用连字符 - 来省略和简写，如`[a-z]`

   如果要匹配连字符 - ，可以转义`\-`

2. 排除字符组

   求反，如`[^abc]`，除了a、b、c的任何一个字符

3. 常见的简写形式

   | 简写形式 | 字符组形式            | 表示                                                         | 英文写法        |
   | -------- | --------------------- | ------------------------------------------------------------ | --------------- |
   | `\d`     | `[0-9]`               | 一位数字                                                     | **d**igit       |
   | `\D`     | `[^0-9]`              | 除了数字以外的任意字符                                       |                 |
   | `\w`     | `[0-9a-zA-Z_]`        | 数字、大小写字母和下划线                                     | **w**ord        |
   | `\W`     | `[^0-9a-zA-Z_]`       |                                                              |                 |
   | `\s`     | `[ \t\v\r\n\f]`       | 空格、水平制表符、垂直制表符、回车符、换行符、换页符         | space character |
   | `\S`     | `[^ \t\v\r\n\f]`      |                                                              |                 |
   | `.`      | `[^\n\r\u2028\u2029]` | 通配符，表示几乎任意字符。换行符、回车符、行分隔符和段分隔符除外。 |                 |





## js数组去重的方法

### 测试代码：

```js
let arr1 = [3, 1, [1], 1, [1], true, true, {}, '1', NaN, undefined, NaN, undefined, {}, null, null];	
let arr2 = [];
for (let i = 0; i < 100000; i++) {
    arr2.push(0 + Math.floor((100000 - 0 + 1) * Math.random()));
}

//function unique(arr) {
//    //...
//}
// 封装在Array的原型对象会更好，this就是指向调用该方法的数组
Array.prototype.unique = function () {
    //...
}

console.log(arr1.unique());	// 测试去重效果
console.time('test');
console.log(arr2.unique());	// 测试去重时间
console.timeEnd('test');
```



### 1. forEach + indexOf

```js
Array.prototype.unique = function () {
    let newArr = [];
    this.forEach((item) => {
        if (newArr.indexOf(item) === -1) {
            newArr.push(item);
        }
    })
    return newArr;
}
```

+ test: 4104.52294921875 ms

> 不能去除重复的NaN和复杂数据类型（比如 Object 和 Array ）
>
> + 原因：indexOf 认为 NaN 不等于 NaN 



### 2. filter + indexOf

```js
Array.prototype.unique = function () {
    return this.filter((item, index) => {
        // 利用indexOf检测元素在数组中第一次出现的位置是否和元素现在的位置相等，如果不等则说明该元素是重复元素
        return this.indexOf(item) === index;
    })
}
```

+ test: 5682.358154296875 ms

> 不能去掉重复的复杂数据类型，同时还会去掉所有的NaN
>
> + 原因：indexOf 认为 NaN 不等于 NaN 



### 3. forEach + includes

```js
Array.prototype.unique = function () {
    let newArr = [];
    this.forEach((item) => {
        if (!newArr.includes(item)) {
            newArr.push(item);
        }
    })
    return newArr;
}
```

+ 4181.393798828125 ms

> 可以去掉重复的NaN，但是不能去掉重复的复杂数据类型
>
> + includes 认为 NaN === NaN 为 true



### 4. for + sort（sort有问题）

```
Array.prototype.unique = function () {
    let newArr = [];
    this.sort();
    for (let i = 0; i < this.length; i++) {
        if (this[i] !== this[i + 1]) {
            newArr.push(this[i]);
        }
    }
    return newArr;
}
```

+ test: 61.96484375 ms

> 带 sort 方法的只对**纯number或者纯string类型**有效，它无法区分1和'1'，因为它是在将元素转换为字符串，然后比较它们的UTF-16代码单元值序列时构建的。
>
> 这时候如果有一段这样的排序[1, '1', 1]，再用前后比较的方法去重就会出现问题

> 同样它不能去重NaN和复杂数据类型



### 5. sort + reduce（sort有问题）

```js
Array.prototype.unique = function () {
    return this.sort().reduce((init, cur) => {
        if (init.length === 0 || init[init.length - 1] !== cur) {
            init.push(cur);
        }
        return init;
    }, []);
}
```

+ test: 66.679931640625 ms

> 同样他也是用sort排序再前后比较，也是傻逼玩意

> 同样也不能去重NaN和复杂数组类型



### 6. 两种for循环 + splice（耗时最长）

```js
Array.prototype.unique = function () {
    for (let i = 0; i < this.length; i++) {
        for (let j = i + 1; j < this.length; j++) {
            if (this[i] === this[j]) {
                this.splice(j, 1);
                j--;
            }
        }
    }
    return this;
}
```

+ test: 21208.31396484375 ms

> 不能去重NaN和复杂数组类型



### 7. forEach + map

```js
Array.prototype.unique = function () {
    let map = new Map();
    let newArr = new Array();
    this.forEach((item) => {
        if (!map.has(item)) {
            map.set(item, 1);
            newArr.push(item);
        }
    });
    return newArr;
}
```

+ test: 27.030029296875 ms

> 可以去NaN，不能去重复杂数组类型



### 8. Set

```js
Array.prototype.unique = function () {
    // return Array.from(new Set(this));
    return [...new Set(this)];
}
```

+ test: 31.197021484375 ms

> 可以去掉重复的NaN，但是不能去掉重复的复杂数据类型



### 9. filter +  hasOwnProperty + JSON.stringify（自认为目前最好的方法！）

```js
Array.prototype.unique = function () {
    let obj = {};
    return this.filter(function (item, index, arr) {
        return obj.hasOwnProperty(typeof item + JSON.stringify(item)) ? false : (obj[typeof item + JSON.stringify(item)] = true);
    });
}
```

+ test: 126.3359375 ms

> 可以去掉**重复的NaN和重复的复杂数据类型**
>
> 在object中，key如果是number类型，它会自动转换成string类型，所以{1:1}和{"1":1}是相等的，这不是这个方法的缺陷，这是obj的缺陷

+ 该方法的核心：以`typeof item`元素类型+`item`的字符串作为key
+ 考虑到obj的字符串都为'[object Object]'，这里使用JSON.stringify(item)，就可以**保存不同的obj字符串**























