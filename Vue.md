[TOC]

## MVVM

+ MVVM（Mode-View-ViewModel）是一种设计思想
  + Model层代表**数据模型**，定义数据修改和操作的业务逻辑。
  + View层代表**UI组件**，负责把数据模型转换成UI
  + ViewModel，是一个同步View和Model的对象（桥梁）
+ 在MVVM架构下，View 和 Model 并没有直接的联系，而是通过 ViewModel 进行交互，Model 和 ViewModel 之间的交互是双向的。因此，**View 数据的变化会同步到 Model 中，而 Model 数据的变化也会立即反映到 View 上**。
+ ViewModel 通过**双向数据绑定**把 View 层和 Model 层连接了起来，而 View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者**只需要关注业务逻辑，不需要手动操作DOM，不需要关注数据状态的同步问题**，复杂的数据状态完全由 MVVM 来统一管理。



## vue的常见指令

1. v-if v-else-if v-else

2. v-show

   > v-if 和 v-show 的区别：
   
   + v-show只改变css的display属性
   + v-if会决定是否生成该dom节点

3. v-for：基于源数据重复渲染元素

4. v-mode：一般用于表单控件元素，创建双向**数据绑定**。（多用于 View 层输入数据，同步到 Model 层）

   > v-model修饰符：

   + number：自动将用户的输入值转换为数值类型
   + lazy：
   + trim：自动过滤用户输入的首尾空格
   
5. v-bind：动态绑定**元素属性**的

   ```html
   <!-- 完整语法 -->
   <input v-bind:type="type">
   <!-- 缩写 -->
   <input :type="type">
   
   <script>
   var app = new Vue({
       el: '#app',
       data: {
           type:"text"
       }
   })
   </script>
   ```

6. v-on：用于**绑定事件**监听器。

   ```html
   <body>
   <div id="app">
       <!-- 完整语法 -->
       <button v-on:click="consoleLog(2)"></button>
       <!-- 缩写 -->
       <button @click="consoleLog('hello world')"></button>
   </div>
   </body>
   <script>
       new Vue({
           el: '#app',
           methods:{
               consoleLog:function (event) {
                   console.log(event)
               }
           }
       })
   </script>
   ```

7. v-once：只会渲染一次

8. v-html：更新元素的innerHTML

   > 不建议使用，容易导致XSS攻击



## methods、watch和computed的区别

### 1. 作用机制上

1. watch和computed都是**以Vue的依赖追踪机制为基础**的。当某个数据（称它为依赖数据）发生变化的时候，所以依赖这个数据的相关数据“自动”发生变化，也就是**自动调用相关函数**去实现数据的变动。
2. 对`methods:methods`里面是用来定义函数的，很显然，它需要**手动调用**才能执行。而不像watch和computed那样，“自动执行”预先定义的函数。



### 2. 从性质上

1. methods里面定义的是函数，需要像`fun()`加个括号去调用。

2. computed是计算属性，事实上**使用起来**和data对象里的数据属性是一样的。

   > 根据依赖关系进行缓存的计算，并且只在需要的时候进行更新。

3. watch：类似监听机制+事件机制。

   ```js
   watch: {
   	firstName: function(value) {
   		this.fullName = val + this.lastName;
   	}
   }
   ```

   **`firstName`的改变**是这个特殊“事件”被触发的条件，而firstName对应的函数就相当于监听到事件发生后执行的方法



### 3. watch和computed的对比

+ 共同点：以Vue的依赖追踪机制为基础。在依赖数据发生变化的时候，被依赖的数据根据预先定义好的函数，发生“自动”的变化。

+ 不同点：

  + watch擅长处理的场景：一个数据影响多个数据，也就是一个数据的变化要改变其他多个的数据。

    >  比如fullName可以改变firstName和lastName

  + computed擅长处理的场景：一个数据受多个数据影响，也就是其他多个数据有发生变化，都会引起这个数据改变

    > 比如购物车的东西增删都会影响最后的总价total

  + （个人理解）watch的键可以看作触发条件（键（数据）发生变化，对应的事件就会被触发）；而computed的键和data的数据属性类似，可以直接引用。

    > ~~简单的理解就是watch的键应该要在data对象或者computed对象中存在先？~~



## watch监听一个对象的属性或者监听整个对象

+ total是监听data的一个普通属性
+ `userInfor.name`是监听一个对象的属性，用字符串的形式即可
+ `userInfo`是监听一个对象，该值也是一个对象，其中
  + handler函数是被触发的函数
  + deep属性需要设置为true（深度监听）

```js
watch: {
    total: function (val, oldVal) {
    	console.log(val + ' ' + oldVal);
    },
    'userInfo.name': function (val, oldVal) {
    	console.log(val);
    },
    userInfo: {
        handler(val, oldVal) {
        	console.log(val);
        },
        deep: true
    }
},
```









































