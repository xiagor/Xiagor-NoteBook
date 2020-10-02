### 在JavaScript中实现AOP

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

   

