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




## JS判断数据的的五种方法

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
  2. 让这些变量的值始终保存在内存中。因为在闭包函数中会引用父函数的作用域对象，使得函数执行结束后，变量不会被垃圾回收机制回收。



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

### 浏览器事件机制







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







