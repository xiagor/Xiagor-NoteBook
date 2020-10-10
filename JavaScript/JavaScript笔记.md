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