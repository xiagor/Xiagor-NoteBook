[TOC]



## 创建object的方法

1. 对象字面量

2. new

3. Object.create()方法（这个没答出来）

   > 用Object.create(null)可以创建出纯净的对象（即没有原型和原型链）



## HTTP状态码

> 回答的还行吧，讲到304然后跳到协商缓存去了



## 强缓存和协商缓存

> 原理可以回答出来，但是http字段没答上来。而且缓存命中的时候并不是从缓存服务器获取文件，而是在浏览器缓存获取文件。

对浏览器缓存还是不够了解



## 对ES6的了解有多少

+ let、const 

+ Array.from()

  > 讲到from的参数是传进一个类数组对象，可迭代对象，比如Set、Map之类的，又跳去Set和Map了



## Set和Map

Set的理解记住了，但是忘记Map了

而且方法也没记住....

他问到他们的使用场景，我只答了写算法的时候（卑微，所以还有啥使用场景？



## CSRF、SSE

就没怎么答上来，安全这块就是盲点，还有怎么解决

还会涉及到cookie等等等等，也是盲点



## 布局、定位等等

> 回答了float、position、flex，问到flex的时候没怎么答上来

flex布局有API的吗？？



## 事件委托

这个没啥问题



## 一道算法题

两个纯数字的数组，找出他们两个数组重复的数并存放在数据中

+ 假设他们数组里面的数是惟一的

  ```js
  var setArr = new Set(第二个数组);
  var resultArr = [];
  for(遍历第一个数组){
  	let length = setArr.length;
  	setArr = setArr.add(当前元素);
  	if(setArr.length === length){
  		resultArr.push(当前元素)
  	}
  }
  ```

+ 如果他们数组里面自身重复的话？

  > 这个没想好























