## 目录
<!-- TOC -->

- [目录](#%E7%9B%AE%E5%BD%95)
- [在JavaScript中实现AOP](#%E5%9C%A8javascript%E4%B8%AD%E5%AE%9E%E7%8E%B0aop)
- [JS判断数组的的五种方法](#js%E5%88%A4%E6%96%AD%E6%95%B0%E7%BB%84%E7%9A%84%E7%9A%84%E4%BA%94%E7%A7%8D%E6%96%B9%E6%B3%95)
    - [instanceof关键字](#instanceof%E5%85%B3%E9%94%AE%E5%AD%97)
    - [实例arr的原型属性__proto__和构造函数Array的原型对象prototype相等](#%E5%AE%9E%E4%BE%8Barr%E7%9A%84%E5%8E%9F%E5%9E%8B%E5%B1%9E%E6%80%A7__proto__%E5%92%8C%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0array%E7%9A%84%E5%8E%9F%E5%9E%8B%E5%AF%B9%E8%B1%A1prototype%E7%9B%B8%E7%AD%89)
    - [constructor](#constructor)
    - [使用Object.prototype的tostring方法](#%E4%BD%BF%E7%94%A8objectprototype%E7%9A%84tostring%E6%96%B9%E6%B3%95)
    - [Array.isArray，返回boolean值](#arrayisarray%E8%BF%94%E5%9B%9Eboolean%E5%80%BC)
- [arguments对象](#arguments%E5%AF%B9%E8%B1%A1)
    - [概念和定义](#%E6%A6%82%E5%BF%B5%E5%92%8C%E5%AE%9A%E4%B9%89)
    - [例子](#%E4%BE%8B%E5%AD%90)
        - [遍历参数求和](#%E9%81%8D%E5%8E%86%E5%8F%82%E6%95%B0%E6%B1%82%E5%92%8C)
        - [定义连接字符串的函数](#%E5%AE%9A%E4%B9%89%E8%BF%9E%E6%8E%A5%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E5%87%BD%E6%95%B0)
- [JS数组降维（扁平化数组）](#js%E6%95%B0%E7%BB%84%E9%99%8D%E7%BB%B4%E6%89%81%E5%B9%B3%E5%8C%96%E6%95%B0%E7%BB%84)
    - [二维数组降为一维数组](#%E4%BA%8C%E7%BB%B4%E6%95%B0%E7%BB%84%E9%99%8D%E4%B8%BA%E4%B8%80%E7%BB%B4%E6%95%B0%E7%BB%84)
        - [循环降维（菜鸡）](#%E5%BE%AA%E7%8E%AF%E9%99%8D%E7%BB%B4%E8%8F%9C%E9%B8%A1)
        - [concat降维（还行）](#concat%E9%99%8D%E7%BB%B4%E8%BF%98%E8%A1%8C)
        - [apply和concat降维（牛逼！）](#apply%E5%92%8Cconcat%E9%99%8D%E7%BB%B4%E7%89%9B%E9%80%BC)
    - [多维数组降为一维数组](#%E5%A4%9A%E7%BB%B4%E6%95%B0%E7%BB%84%E9%99%8D%E4%B8%BA%E4%B8%80%E7%BB%B4%E6%95%B0%E7%BB%84)
- [Array.from（ES6）](#arrayfromes6)
    - [语法](#%E8%AF%AD%E6%B3%95)
    - [示例](#%E7%A4%BA%E4%BE%8B)
        - [从 String 生成数组](#%E4%BB%8E-string-%E7%94%9F%E6%88%90%E6%95%B0%E7%BB%84)
        - [从 Set 生成数组](#%E4%BB%8E-set-%E7%94%9F%E6%88%90%E6%95%B0%E7%BB%84)
        - [从 Map 生成数组](#%E4%BB%8E-map-%E7%94%9F%E6%88%90%E6%95%B0%E7%BB%84)
        - [从类数组对象（arguments）生成数组](#%E4%BB%8E%E7%B1%BB%E6%95%B0%E7%BB%84%E5%AF%B9%E8%B1%A1arguments%E7%94%9F%E6%88%90%E6%95%B0%E7%BB%84)
        - [在 Array.from 中使用箭头函数](#%E5%9C%A8-arrayfrom-%E4%B8%AD%E4%BD%BF%E7%94%A8%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0)
        - [数组去重合并](#%E6%95%B0%E7%BB%84%E5%8E%BB%E9%87%8D%E5%90%88%E5%B9%B6)
- [回调函数](#%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0)
- [闭包](#%E9%97%AD%E5%8C%85)
- [事件](#%E4%BA%8B%E4%BB%B6)
- [隐式转换类型型](#%E9%9A%90%E5%BC%8F%E8%BD%AC%E6%8D%A2%E7%B1%BB%E5%9E%8B%E5%9E%8B)
        - [隐式转换类型规则](#%E9%9A%90%E5%BC%8F%E8%BD%AC%E6%8D%A2%E7%B1%BB%E5%9E%8B%E8%A7%84%E5%88%99)
        - [坑一：字符串连接符与算术运算符隐式转换规则混淆](#%E5%9D%91%E4%B8%80%E5%AD%97%E7%AC%A6%E4%B8%B2%E8%BF%9E%E6%8E%A5%E7%AC%A6%E4%B8%8E%E7%AE%97%E6%9C%AF%E8%BF%90%E7%AE%97%E7%AC%A6%E9%9A%90%E5%BC%8F%E8%BD%AC%E6%8D%A2%E8%A7%84%E5%88%99%E6%B7%B7%E6%B7%86)
        - [坑二：关系运算符：会把其他数据类型转换成number之后再比较关系](#%E5%9D%91%E4%BA%8C%E5%85%B3%E7%B3%BB%E8%BF%90%E7%AE%97%E7%AC%A6%E4%BC%9A%E6%8A%8A%E5%85%B6%E4%BB%96%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2%E6%88%90number%E4%B9%8B%E5%90%8E%E5%86%8D%E6%AF%94%E8%BE%83%E5%85%B3%E7%B3%BB)
        - [坑三：复杂数据类型在隐式转换时会先转成String，然后再转成Number运算](#%E5%9D%91%E4%B8%89%E5%A4%8D%E6%9D%82%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E5%9C%A8%E9%9A%90%E5%BC%8F%E8%BD%AC%E6%8D%A2%E6%97%B6%E4%BC%9A%E5%85%88%E8%BD%AC%E6%88%90string%E7%84%B6%E5%90%8E%E5%86%8D%E8%BD%AC%E6%88%90number%E8%BF%90%E7%AE%97)
        - [坑四：逻辑非隐式转换与关系运算符隐式转换搞混淆巨坑](#%E5%9D%91%E5%9B%9B%E9%80%BB%E8%BE%91%E9%9D%9E%E9%9A%90%E5%BC%8F%E8%BD%AC%E6%8D%A2%E4%B8%8E%E5%85%B3%E7%B3%BB%E8%BF%90%E7%AE%97%E7%AC%A6%E9%9A%90%E5%BC%8F%E8%BD%AC%E6%8D%A2%E6%90%9E%E6%B7%B7%E6%B7%86%E5%B7%A8%E5%9D%91)
- [String方法](#string%E6%96%B9%E6%B3%95)
    - [字符方法](#%E5%AD%97%E7%AC%A6%E6%96%B9%E6%B3%95)
        - [charAt](#charat)
        - [charCodeAt](#charcodeat)
        - [ES5访问个别字符的方法](#es5%E8%AE%BF%E9%97%AE%E4%B8%AA%E5%88%AB%E5%AD%97%E7%AC%A6%E7%9A%84%E6%96%B9%E6%B3%95)
    - [字符串操作方法](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95)
        - [concat](#concat)
        - [slice、substr、substring](#slicesubstrsubstring)
    - [字符串位置方法](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%BD%8D%E7%BD%AE%E6%96%B9%E6%B3%95)
        - [indexOf、lastIndexOf](#indexoflastindexof)
        - [查找所有出现过的字符串的方法](#%E6%9F%A5%E6%89%BE%E6%89%80%E6%9C%89%E5%87%BA%E7%8E%B0%E8%BF%87%E7%9A%84%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E6%96%B9%E6%B3%95)
    - [trim删除前后空格](#trim%E5%88%A0%E9%99%A4%E5%89%8D%E5%90%8E%E7%A9%BA%E6%A0%BC)
    - [字符串大小写转换方法](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%A4%A7%E5%B0%8F%E5%86%99%E8%BD%AC%E6%8D%A2%E6%96%B9%E6%B3%95)
    - [字符串的模式匹配方式](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E6%A8%A1%E5%BC%8F%E5%8C%B9%E9%85%8D%E6%96%B9%E5%BC%8F)
        - [match](#match)
        - [search](#search)
        - [replace](#replace)
        - [split](#split)
- [new的时候发生了什么](#new%E7%9A%84%E6%97%B6%E5%80%99%E5%8F%91%E7%94%9F%E4%BA%86%E4%BB%80%E4%B9%88)
- [防抖和节流](#%E9%98%B2%E6%8A%96%E5%92%8C%E8%8A%82%E6%B5%81)
    - [防抖debounce](#%E9%98%B2%E6%8A%96debounce)
    - [节流throttle](#%E8%8A%82%E6%B5%81throttle)
    - [应用场景举例](#%E5%BA%94%E7%94%A8%E5%9C%BA%E6%99%AF%E4%B8%BE%E4%BE%8B)
- [立即执行函数](#%E7%AB%8B%E5%8D%B3%E6%89%A7%E8%A1%8C%E5%87%BD%E6%95%B0)
- [回调地狱及解决方法](#%E5%9B%9E%E8%B0%83%E5%9C%B0%E7%8B%B1%E5%8F%8A%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95)
    - [回调地狱的缺点](#%E5%9B%9E%E8%B0%83%E5%9C%B0%E7%8B%B1%E7%9A%84%E7%BC%BA%E7%82%B9)
    - [回调地狱的解决方法](#%E5%9B%9E%E8%B0%83%E5%9C%B0%E7%8B%B1%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95)
        - [Promise解决（ES6）](#promise%E8%A7%A3%E5%86%B3es6)
        - [async/await解决（ES7）](#asyncawait%E8%A7%A3%E5%86%B3es7)
        - [generator](#generator)
- [正则表达式字符匹配](#%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%AD%97%E7%AC%A6%E5%8C%B9%E9%85%8D)
    - [两种模糊匹配](#%E4%B8%A4%E7%A7%8D%E6%A8%A1%E7%B3%8A%E5%8C%B9%E9%85%8D)
        - [横向模糊匹配](#%E6%A8%AA%E5%90%91%E6%A8%A1%E7%B3%8A%E5%8C%B9%E9%85%8D)
        - [纵向模糊匹配](#%E7%BA%B5%E5%90%91%E6%A8%A1%E7%B3%8A%E5%8C%B9%E9%85%8D)
    - [字符组](#%E5%AD%97%E7%AC%A6%E7%BB%84)
- [js数组去重的方法](#js%E6%95%B0%E7%BB%84%E5%8E%BB%E9%87%8D%E7%9A%84%E6%96%B9%E6%B3%95)
    - [测试代码：](#%E6%B5%8B%E8%AF%95%E4%BB%A3%E7%A0%81)
    - [forEach + indexOf](#foreach--indexof)
    - [filter + indexOf](#filter--indexof)
    - [forEach + includes](#foreach--includes)
    - [for + sort（sort有问题）](#for--sortsort%E6%9C%89%E9%97%AE%E9%A2%98)
    - [sort + reduce（sort有问题）](#sort--reducesort%E6%9C%89%E9%97%AE%E9%A2%98)
    - [两种for循环 + splice（耗时最长）](#%E4%B8%A4%E7%A7%8Dfor%E5%BE%AA%E7%8E%AF--splice%E8%80%97%E6%97%B6%E6%9C%80%E9%95%BF)
    - [forEach + map](#foreach--map)
    - [Set](#set)
    - [filter +  hasOwnProperty + JSON.stringify（自认为目前最好的方法！）](#filter---hasownproperty--jsonstringify%E8%87%AA%E8%AE%A4%E4%B8%BA%E7%9B%AE%E5%89%8D%E6%9C%80%E5%A5%BD%E7%9A%84%E6%96%B9%E6%B3%95)
- [JS的垃圾回收机制](#js%E7%9A%84%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6%E6%9C%BA%E5%88%B6)
- [跨域](#%E8%B7%A8%E5%9F%9F)
    - [JSONP](#jsonp)
        - [JSONP和AJAX对比](#jsonp%E5%92%8Cajax%E5%AF%B9%E6%AF%94)
        - [JSONP的优缺点](#jsonp%E7%9A%84%E4%BC%98%E7%BC%BA%E7%82%B9)
        - [JSONP的实现流程](#jsonp%E7%9A%84%E5%AE%9E%E7%8E%B0%E6%B5%81%E7%A8%8B)
        - [JSONP的简单实现](#jsonp%E7%9A%84%E7%AE%80%E5%8D%95%E5%AE%9E%E7%8E%B0)
        - [JSONP的封装](#jsonp%E7%9A%84%E5%B0%81%E8%A3%85)
        - [JQuery的jsonp形式](#jquery%E7%9A%84jsonp%E5%BD%A2%E5%BC%8F)
    - [CORS](#cors)
    - [Web Socket协议](#web-socket%E5%8D%8F%E8%AE%AE)
    - [nginx反向代理](#nginx%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86)
- [Ajax（XMLHttpRequest 对象）](#ajaxxmlhttprequest-%E5%AF%B9%E8%B1%A1)
    - [构造函数](#%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0)
    - [属性](#%E5%B1%9E%E6%80%A7)
        - [事件处理器](#%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%99%A8)
    - [方法](#%E6%96%B9%E6%B3%95)
    - [手写Promise封装ajax](#%E6%89%8B%E5%86%99promise%E5%B0%81%E8%A3%85ajax)
- [js去除字符串空格的方法](#js%E5%8E%BB%E9%99%A4%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%A9%BA%E6%A0%BC%E7%9A%84%E6%96%B9%E6%B3%95)
- [异步编程的实现方式](#%E5%BC%82%E6%AD%A5%E7%BC%96%E7%A8%8B%E7%9A%84%E5%AE%9E%E7%8E%B0%E6%96%B9%E5%BC%8F)
    - [回调函数](#%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0)
    - [Promise对象](#promise%E5%AF%B9%E8%B1%A1)
    - [Generator 函数](#generator-%E5%87%BD%E6%95%B0)
    - [async 函数](#async-%E5%87%BD%E6%95%B0)
    - [事件监听（采用时间驱动模式，取决于某个事件是否可以发生）](#%E4%BA%8B%E4%BB%B6%E7%9B%91%E5%90%AC%E9%87%87%E7%94%A8%E6%97%B6%E9%97%B4%E9%A9%B1%E5%8A%A8%E6%A8%A1%E5%BC%8F%E5%8F%96%E5%86%B3%E4%BA%8E%E6%9F%90%E4%B8%AA%E4%BA%8B%E4%BB%B6%E6%98%AF%E5%90%A6%E5%8F%AF%E4%BB%A5%E5%8F%91%E7%94%9F)
    - [发布/订阅（观察者模式）](#%E5%8F%91%E5%B8%83%E8%AE%A2%E9%98%85%E8%A7%82%E5%AF%9F%E8%80%85%E6%A8%A1%E5%BC%8F)
    - [面试答案](#%E9%9D%A2%E8%AF%95%E7%AD%94%E6%A1%88)
- [Promise动态加载图片](#promise%E5%8A%A8%E6%80%81%E5%8A%A0%E8%BD%BD%E5%9B%BE%E7%89%87)
    - [new Image](#new-image)
    - [Promise实现代码](#promise%E5%AE%9E%E7%8E%B0%E4%BB%A3%E7%A0%81)
- [动态加载一个JS，并在加载成功后执行回调函数](#%E5%8A%A8%E6%80%81%E5%8A%A0%E8%BD%BD%E4%B8%80%E4%B8%AAjs%E5%B9%B6%E5%9C%A8%E5%8A%A0%E8%BD%BD%E6%88%90%E5%8A%9F%E5%90%8E%E6%89%A7%E8%A1%8C%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0)
- [什么是假值对象](#%E4%BB%80%E4%B9%88%E6%98%AF%E5%81%87%E5%80%BC%E5%AF%B9%E8%B1%A1)
- [this对象的理解](#this%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%90%86%E8%A7%A3)
    - [this的指向](#this%E7%9A%84%E6%8C%87%E5%90%91)
    - [怎么改变this的指向](#%E6%80%8E%E4%B9%88%E6%94%B9%E5%8F%98this%E7%9A%84%E6%8C%87%E5%90%91)
        - [箭头函数](#%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0)
        - [在函数内部使用 _this = this](#%E5%9C%A8%E5%87%BD%E6%95%B0%E5%86%85%E9%83%A8%E4%BD%BF%E7%94%A8-_this--this)
        - [使用 apply、call、bind](#%E4%BD%BF%E7%94%A8-applycallbind)
        - [使用 new 实例化一个对象](#%E4%BD%BF%E7%94%A8-new-%E5%AE%9E%E4%BE%8B%E5%8C%96%E4%B8%80%E4%B8%AA%E5%AF%B9%E8%B1%A1)
    - [this 的四种调用模式](#this-%E7%9A%84%E5%9B%9B%E7%A7%8D%E8%B0%83%E7%94%A8%E6%A8%A1%E5%BC%8F)
        - [函数调用模式](#%E5%87%BD%E6%95%B0%E8%B0%83%E7%94%A8%E6%A8%A1%E5%BC%8F)
        - [方法调用模式（隐式绑定）](#%E6%96%B9%E6%B3%95%E8%B0%83%E7%94%A8%E6%A8%A1%E5%BC%8F%E9%9A%90%E5%BC%8F%E7%BB%91%E5%AE%9A)
        - [构造器调用模式](#%E6%9E%84%E9%80%A0%E5%99%A8%E8%B0%83%E7%94%A8%E6%A8%A1%E5%BC%8F)
        - [apply 、 call 和 bind 调用模式](#apply--call-%E5%92%8C-bind-%E8%B0%83%E7%94%A8%E6%A8%A1%E5%BC%8F)
        - [四种模式的优先级](#%E5%9B%9B%E7%A7%8D%E6%A8%A1%E5%BC%8F%E7%9A%84%E4%BC%98%E5%85%88%E7%BA%A7)

<!-- /TOC -->


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

### instanceof关键字

`arr instanceof Array`

`实例 instanceof 构造函数`



### 实例arr的原型属性`__proto__`和构造函数Array的原型对象`prototype`相等

`arr.__proto__ === Array.prototype`



### constructor

+ 实例对象可以通过`__proto__`访问到构造函数的原型对象`Array.prototype`（正如第二点，他们就是相等的），即也可以继承到`Array.prototype.constructor`（指回Array）

`arr.constructor === Array`

> 这里的arr.constructor实际上是`arr.__proto__.constructor`



### 使用Object.prototype的tostring方法

`Object.prototype.toString() === '[object Object]'`

`Object.prototype.toString.call(arr) === '[object Array]'`

> 注意第二个的toString后面没有 () ，因为call改变前面方法的this指向的同时还会自动执行方法（bind不会）
>
> call传递的参数是实例数组arr，后面的Object就会改成Array



### Array.isArray()，返回boolean值

`Array.isArray(arr) === true`



## arguments对象

### 概念和定义

> 一个对应于传递给函数的参数的**类数组对象**，是所有（非箭头）函数中都可用的局部变量。

此对象包含传递给函数的每个参数（我的理解就是，**包含了调用函数时传入的实参**，不管该函数定义时有无形参）

1. 它不是一个Array，它类似Array，但除了length属性和索引元素之外没有任何Array属性。
2. `arguments.__proto__ === Object.prototype`，由此我是理解arguments的构造函数是Object
3. `Object.prototype.toString.call(arguments) === '[object Arguments]'`

> 对3里面的Object的原型对象prototype的toString方法其实我还不是很理解，是依据什么去变成字符串的呢？



### 例子

#### 遍历参数求和

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

#### 定义连接字符串的函数

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

### 二维数组降为一维数组

#### 循环降维（菜鸡）

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

#### concat降维（还行）

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

#### apply和concat降维（牛逼！）

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



### 多维数组降为一维数组

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



### 语法

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



### 示例

#### 从 `String` 生成数组

```javascript
Array.from('foo'); 
// [ "f", "o", "o" ]
```

#### 从 `Set` 生成数组

```js
const set = new Set(['foo', 'bar', 'baz', 'foo']);
Array.from(set);
// [ "foo", "bar", "baz" ]
```

#### 从 `Map` 生成数组

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

#### 从类数组对象（arguments）生成数组

```js
function f() {
  return Array.from(arguments);
}

f(1, 2, 3);

// [ 1, 2, 3 ]
```

#### 在 `Array.from` 中使用箭头函数

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

#### 数组去重合并

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









## 隐式转换类型型

#### 隐式转换类型规则

1. 转成string类型： + （字符串连接符，只要有一边是string就是字符串连接符）
2. 转成number类型： ++/--(自增自减运算符) 、+-*/%(算术运算符)、><等（关系运算符）
3. 转成boolean类型：! （逻辑非运算符）

#### 坑一：字符串连接符与算术运算符隐式转换规则混淆

```javascript
console.log(1 + "true");//"1true"
console.log(1 + true);//Number(true) = 1
console.log(1 + undefined);//Number(undefined) = NaN
console.log(1 + null);//Number(null) = 0
```

#### 坑二：关系运算符：会把其他数据类型转换成number之后再比较关系

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

#### 坑三：复杂数据类型在隐式转换时会先转成String，然后再转成Number运算

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

#### 坑四：逻辑非隐式转换与关系运算符隐式转换搞混淆(巨坑)

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

### 字符方法

#### charAt()

接收一个字符位置的参数，以单字符字符串的形式返回该位置的字符。

```js
var stringValue = "hello world";
console.log(stringValue.charAt(1));		//'e'
```



#### charCodeAt()

接收一个字符位置的参数，以单字符字符串的形式返回该位置的字符**的字符编码**。

```js
var stringValue = "hello world";
console.log(stringValue.charAt(1));		//'101'
```



#### ES5访问个别字符的方法

使用方括号加数字索引访问

> IE7及更早版本不支持

```js
var stringValue = "hello world";
console.log(stringValue[1]);		//'e'
```



### 字符串操作方法

> 都是返回一个新的字符串

#### concat()

拼接字符串的，建议直接用 + 拼接。

#### slice()、substr()、substring()

| 方法        | 参数一（必需）     | 参数二（可选）                               | 参数一为负值时                      | 参数二为负值时 |
| ----------- | ------------------ | -------------------------------------------- | ----------------------------------- | -------------- |
| slice()     | 子字符串的开始位置 | 子字符串结束位置（不包括），默认到字符串末尾 | 负值+length                         | 负值+length    |
| substr()    | 子字符串的开始位置 | 字符个数，默认到字符串末尾                   | 负值+length                         | 0              |
| substring() | 子字符串的开始位置 | 子字符串结束位置（不包括），默认到字符串末尾 | 0（该方法会以较小的数作为开始位置） | 0              |



### 字符串位置方法

#### indexOf()、lastIndexOf()

+ 参数一（必需）：需要查找的子字符串
+ 参数二（可选）：从字符串哪个位置开始查找
+ 返回值：子字符串第一次出现的下标值，没有则返回-1
+ 区别：
  + indexOf：是从字符串的开头开始查找
  + lastIndexOf：是从字符串的末尾向前查找

#### 查找所有出现过的字符串的方法

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



### trim()删除前后空格

删除前置及后缀的所有空格，返回一个字符串的副本，不会改变原字符串。



### 字符串大小写转换方法

+ toLowerCase()：字符串转换为小写，无传参
+ toUpperCase()：字符串转换为大写，无传参



### 字符串的模式匹配方式

#### match()

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

#### search()

+ 参数为一个正则表达式或者一个RegExp对象
  + 当参数是一个字符串或一个数字，它会使用new RegExp(obj)来隐式转换成一个 [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp)
+ 返回正则表达式在字符串中首次匹配项的索引，否则返回-1。

#### replace()

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

#### split()

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

### 防抖debounce

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

   

### 节流throttle

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



### 应用场景举例

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

### 回调地狱的缺点

+ 上边的例子用回调地狱能解决问题，但是有缺点，或者说不优雅。
+ 如果最里面的异步没有执行结束，外面所有的程序是不是都相当于没有结束，有点递归的影子，非常消耗性能。
+ 格式非常不优雅，语义化非常差，不方便调错。

### 回调地狱的解决方法

#### Promise解决（ES6）

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

    

#### async/await解决（ES7）

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



#### generator

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

### 两种模糊匹配

#### 横向模糊匹配

> 横向模糊指的是，一个正则可匹配的字符串的长度不是固定的，可以是多种情况的。

+ 实现方式：使用量词，譬如`{m,n}`，表示连续出现最少m次，最多n次

```js
var regex = /ab{2,5}c/g;
var string = "abc abbc abbbc abbbbc abbbbbc abbbbbbc";
console.log( string.match(regex) ); 
// => ["abbc", "abbbc", "abbbbc", "abbbbbc"]
```

#### 纵向模糊匹配

> 纵向模糊指的是，一个正则匹配的字符串，具体到某一位字符时，它可以不是某个确定的字符，可以有多种可能。

+ 实现方式：使用字符组，譬如`[abc]`，表示该字符可以是"a","b","c"中的任意一个。

```js
var regex = /a[123]b/g;
var string = "a0b a1b a2b a3b a4b";
console.log( string.match(regex) ); 
// => ["a1b", "a2b", "a3b"]
```



### 字符组

> 虽然叫字符组，但只是其中一个字符，例如`[abc]`，**表示匹配一个字符**，可以是"a","b","c"中的任意一个。

1. 范围表示法

   用连字符 - 来省略和简写，如`[a-z]`

   如果要匹配连字符 - ，可以转义`\-`

2. 排除字符组

   求反，如`[^abc]`，除了a、b、c的任何一个字符

3. 常见的简写形式

   | 简写形式 | 字符组形式            | 表示                                                               | 英文写法        |
   | -------- | --------------------- | ------------------------------------------------------------------ | --------------- |
   | `\d`     | `[0-9]`               | 一位数字                                                           | **d**igit       |
   | `\D`     | `[^0-9]`              | 除了数字以外的任意字符                                             |                 |
   | `\w`     | `[0-9a-zA-Z_]`        | 数字、大小写字母和下划线                                           | **w**ord        |
   | `\W`     | `[^0-9a-zA-Z_]`       |                                                                    |                 |
   | `\s`     | `[ \t\v\r\n\f]`       | 空格、水平制表符、垂直制表符、回车符、换行符、换页符               | space character |
   | `\S`     | `[^ \t\v\r\n\f]`      |                                                                    |                 |
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



### forEach + indexOf

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



### filter + indexOf

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



### forEach + includes

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



### for + sort（sort有问题）

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



### sort + reduce（sort有问题）

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



### 两种for循环 + splice（耗时最长）

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



### forEach + map

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



### Set

```js
Array.prototype.unique = function () {
    // return Array.from(new Set(this));
    return [...new Set(this)];
}
```

+ test: 31.197021484375 ms

> 可以去掉重复的NaN，但是不能去掉重复的复杂数据类型



### filter +  hasOwnProperty + JSON.stringify（自认为目前最好的方法！）

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





## JS的垃圾回收机制

> 对于那些执行完毕的函数，如果没有外部引用（被引用的话会形成闭包），则会回收。

常见的两种垃圾回收规则是：

+ 标记清除
+ 引用计数



## 跨域

> 当协议、子域名、主域名、端口号中任意一个不相同时，都算作不同域。不同域之间相互请求资源，就算作跨域。

### JSONP

> 利用`<script>`标签没有跨域限制，网页可以得到从其他来源动态产生的JSON数据。JSONP请求一定需要对方的服务器做支持才可以。

#### JSONP和AJAX对比

JSONP和AJAX相同，都是客户端向服务器发送请求，从服务器端获取数据的方式。但AJAX属于同源策略，JSONP属于非同源策略（跨域请求）

#### JSONP的优缺点

+ 优点：简单兼容性好，可用于解决跨域数据访问的问题。
+ 缺点：仅支持get请求，不安全（可能会遭遇XSS攻击）

#### JSONP的实现流程

1. 声明一个回调函数，其函数名当作参数值，参数形参为要获取的目标数据（服务器返回的data）
2. 创建一个`<script>`标签，把那个服务器端给的数据接口地址赋值给src，还要在这个地址中传函数名（通过url的字符串拼接`?callback=show）
3. 服务器收到请求后，需要做特殊的处理：把传进来的函数名和它需要给你的data拼接成一个字符串，如`show({"name":"xiagor"})`
4. 最后服务器把准备的数据通过HTTP协议返回给客户端，客户端再调用执行之前声明的回调函数show，对返回的data进行操作

#### JSONP的简单实现

...

#### JSONP的封装

...

#### JQuery的jsonp形式

...



### CORS

> 跨域资源共享（CORS）是一种机制，它允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服了Ajax只能同源使用的限制。





### Web Socket协议

> Web Socket是HTML5的一个持久化的协议，它实现了浏览器与服务器的全双工通信，不遵循同源策略，同时也是跨域的一种解决方案。



### nginx反向代理

实现原理：同源策略是**浏览器**需要遵循的标准，而如果是**服务器向服务器**请求就无需遵循同源策略。 

代理服务器需要以下几个步骤：

1. 接受客户端请求（和客户端同源，遵循同源策略）
2. 将请求转给服务器
3. 拿到服务器的响应数据
4. 将响应转给客户端



> 正向代理和反向代理的区别：
>
> 正向代理就是，比如你指定那个人代购，要去香港买这件商品，反向代理就是你指定代购那个商品，不需要知道代购的人去哪里买





## Ajax（XMLHttpRequest 对象）

> AJAX是异步的JavaScript和XML（**A**synchronous **J**avaScript **A**nd **X**ML）。简单点说，就是使用XMLHttpRequest对象与服务器通信。[参考MDN文档的XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) 



### 构造函数

- [`XMLHttpRequest()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/XMLHttpRequest)

  该构造函数用于初始化一个 `XMLHttpRequest` 实例对象。在调用下列任何其他方法之前，必须先调用该构造函数，或通过其他方式，得到一个实例对象。



### 属性

*此接口继承了 [`XMLHttpRequestEventTarget`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequestEventTarget) 和 [`EventTarget`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget) 的属性。*

- [`XMLHttpRequest.onreadystatechange`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/onreadystatechange)

  当 `readyState` 属性发生变化时，调用的 [`EventHandler`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventHandler)。

- [`XMLHttpRequest.readyState`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState)  `只读`

  返回 一个无符号短整型（`unsigned short`）数字，代表请求的状态码。

- [`XMLHttpRequest.response`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/response) `只读`

  返回一个 [`ArrayBuffer`](https://developer.mozilla.org/zh-CN/docs/Web/API/ArrayBuffer)、[`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)、[`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document)，或 [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)，具体是哪种类型取决于 [`XMLHttpRequest.responseType`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/responseType) 的值。其中包含整个响应实体（response entity body）。

- [`XMLHttpRequest.responseText`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/responseText) `只读`

  返回一个 [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)，该 [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString) 包含对请求的响应，如果请求未成功或尚未发送，则返回 `null`。

- [`XMLHttpRequest.responseType`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/responseType)

  一个用于定义响应类型的枚举值（enumerated value）。

- [`XMLHttpRequest.responseURL`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/responseURL) `只读`

  返回经过序列化（serialized）的响应 URL，如果该 URL 为空，则返回空字符串。

- [`XMLHttpRequest.responseXML`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/responseXML) `只读`

  返回一个 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document)，其中包含该请求的响应，如果请求未成功、尚未发送或时不能被解析为 XML 或 HTML，则返回 `null`。

- [`XMLHttpRequest.status`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/status) `只读`

  返回一个无符号短整型（`unsigned short`）数字，代表请求的响应状态。

- [`XMLHttpRequest.statusText`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/statusText) `只读`

  返回一个 [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)，其中包含 HTTP 服务器返回的响应状态。与 [`XMLHTTPRequest.status`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHTTPRequest/status) 不同的是，它包含完整的响应状态文本（例如，"`200 OK`"）。

  > **注意：**根据 HTTP/2 规范（[8.1.2.4](https://http2.github.io/http2-spec/#rfc.section.8.1.2.4) [Response Pseudo-Header Fields](https://http2.github.io/http2-spec/#HttpResponse)，响应伪标头字段），HTTP/2 没有定义任何用于携带 HTTP/1.1 状态行中包含的版本（version）或者原因短语（reason phrase）的方法。

- [`XMLHttpRequest.timeout`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/timeout)

  一个无符号长整型（`unsigned long`）数字，表示该请求的最大请求时间（毫秒），若超出该时间，请求会自动终止。

- [`XMLHttpRequestEventTarget.ontimeout`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequestEventTarget/ontimeout)

  当请求超时调用的 [`EventHandler`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventHandler)。

- [`XMLHttpRequest.upload`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/upload) `只读`

  [`XMLHttpRequestUpload`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequestUpload)，代表上传进度。

- [`XMLHttpRequest.withCredentials`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/withCredentials)

  一个[`布尔值`](https://developer.mozilla.org/zh-CN/docs/Web/API/Boolean)，用来指定跨域 `Access-Control` 请求是否应当带有授权信息，如 cookie 或授权 header 头。

#### 事件处理器

作为 `XMLHttpRequest` 实例的属性之一，所有浏览器都支持 `onreadystatechange`。

后来，许多浏览器实现了一些额外的事件（`onload`、`onerror`、`onprogress` 等）。详见[Using XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)。

更多现代浏览器，包括 Firefox，除了可以设置 `on*` 属性外，也提供标准的监听器 [`addEventListener()`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener) API 来监听`XMLHttpRequest` 事件。



### 方法

- [`XMLHttpRequest.abort()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/abort)

  如果请求已被发出，则立刻中止请求。

- [`XMLHttpRequest.getAllResponseHeaders()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/getAllResponseHeaders)

  以字符串的形式返回所有用 [CRLF](https://developer.mozilla.org/zh-CN/docs/Glossary/CRLF) 分隔的响应头，如果没有收到响应，则返回 `null`。

- [`XMLHttpRequest.getResponseHeader()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/getResponseHeader)

  返回包含指定响应头的字符串，如果响应尚未收到或响应中不存在该报头，则返回 `null`。

- [`XMLHttpRequest.open()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/open)

  初始化一个请求。该方法只能在 JavaScript 代码中使用，若要在 native code 中初始化请求，请使用 [`openRequest()`](https://developer.mozilla.org/zh-CN/docs/Mozilla/Tech/XPCOM/Reference/Interface/nsIXMLHttpRequest)。

- [`XMLHttpRequest.overrideMimeType()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/overrideMimeType)

  覆写由服务器返回的 MIME 类型。

- [`XMLHttpRequest.send()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/send)

  发送请求。如果请求是异步的（默认），那么该方法将在请求发送后立即返回。

- [`XMLHttpRequest.setRequestHeader()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/setRequestHeader)

  设置 HTTP 请求头的值。必须在 `open()` 之后、`send()` 之前调用 `setRequestHeader()` 方法。



### 手写Promise封装ajax

```js
// 取JSON格式的，需要后台返回JSON格式！
function getJSON(url) {
    return new Promise((resolve, reject) => {
        let xhr = new XMLHttpRequest();
        xhr.open('get', url, true);
        xhr.onreadystatechange = function () {
            if (xhr.readyState !== 4) {
                return;
            }
            if (xhr.status == 200) {
                resolve(xhr.response);
            } else {
                reject(new Error(xhr.statusText));
            }
        }
        xhr.onerror = () => {
            reject(new Error(xhr.statusText));
        }
        xhr.responseType = 'json';
        xhr.setRequestHeader('Accept', 'application/json');
        xhr.send(null);
    });
}
getJSON('/bar')
    .then((res) => {
        console.log(res);
    })
    .catch((error) => {
        console.log(error);
    })
```



## js去除字符串空格的方法

1. `str.trim()`

   去掉字符串前后空格
   
2. `str.trimStart()`

   去掉字符串前面的空格

3. `str.trimEnd()`

   去掉字符串后面的空格

4. `str.replace(/\s/g, '')`

   去掉 字符串中所有空格



## 异步编程的实现方式

### 回调函数

优点：简单、容易理解

缺点：不利于维护、代码耦合度高（例如回调函数地狱）



### Promise对象

优点：可以利用 then 方法，进行链式写法；可以书写错误时的回调函数

缺点：多个then链式调用，可能会造成代码的语义不够明确



### Generator 函数

优点：函数体内外的数据交换、错误处理机制。

缺点：流程管理不方便。

> 使用 generator 的方式，它可以在函数的执行过程中，将函数的执行权转移出去，在函数外部我们还可以将执行权转移回来。当我们遇到异步函数执行的时候，将函数执行权转移出去，当异步函数执行完毕的时候我们再将执行权给转移回来。
>
> 因此我们在 generator 内部对于异步操作的方式，可以以同步的顺序来书写。
>
> 使用这种方式我们需要考虑的问题是何时将函数的控制权转移回来，因此我们需要有一个自动执行 generator 的机制，比如说 co 模块等方式来实现 generator 的自动执行。



### async 函数

优点：内置执行器，更好的语义，更广的适用性，返回的是Promise、结构清晰

缺点：错误处理机制

> 使用 async 函数的形式，async 函数是 generator 和 promise 实现的一个自动执行的语法糖，它内部自带执行器，当函数内部执行到一个 await 语句的时候，如果语句返回一个 promise 对象，那么函数将会等待 promise 对象的状态变为 resolve 后再继续向下执行。因此我们可以将异步逻辑，转化为同步的顺序来书写，并且这个函数可以自动执行。
>
> async函数内部**抛出的错误**会导致返回的Promise对象那个变为reject状态，抛出的错误对象会被catch方法回调函数接收到。（此时如果）
>
> 如果有多个await命令，其中一个await命令后面的异步操作失败（即Promise对象的运行结果是rejected），那后面的await语句将不再会执行。等同于整个async函数返回的Promise对象被reject。（这就是他的缺点）
>
> 解决办法可以使用try..catch结构，将可能失败的 await 命令放在 try 中并用 catch 捕捉错误，这样不管这个await是否失败，接着后面的 await 都能执行。或者直接在 await 后面的 Promise 对象后添加一个 catch 方法，处理前面可能出现的错误



### 事件监听（采用时间驱动模式，取决于某个事件是否可以发生）

优点：容易理解，可以绑定多个事件，每个事件可以指定多个回调函数

缺点：事件驱动型，流程不够清晰



### 发布/订阅（观察者模式）

类似于事件监听，但是可以通过‘消息中心’，了解现在有多少发布者，多少订阅者



### 面试答案

```
js 中的异步机制可以分为以下几种：

第一种最常见的是使用回调函数的方式，使用回调函数的方式有一个缺点是，多个回调函数嵌套的时候会造成回调函数地狱，上下两层的回调函数间的代码耦合度太高，不利于代码的可维护。

第二种是 Promise 的方式，使用 Promise 的方式可以将嵌套的回调函数作为链式调用。但是使用这种方法，有时会造成多个 then 的链式调用，可能会造成代码的语义不够明确。

第三种是使用 generator 的方式，它可以在函数的执行过程中，将函数的执行权转移出去，在函数外部我们还可以将执行权转移回来。当我们遇到异步函数执行的时候，将函数执行权转移出去，当异步函数执行完毕的时候我们再将执行权给转移回来。因此我们在 generator 内部对于异步操作的方式，可以以同步的顺序来书写。使用这种方式我们需要考虑的问题是何时将函数的控制权转移回来，因此我们需要有一个自动执行 generator 的机制，比如说 co 模块等方式来实现 generator 的自动执行。

第四种是使用 async 函数的形式，async 函数是 generator 和 promise 实现的一个自动执行的语法糖，它内部自带执行器，当函数内部执行到一个 await 语句的时候，如果语句返回一个 promise 对象，那么函数将会等待 promise 对象的状态变为 resolve 后再继续向下执行。因此我们可以将异步逻辑，转化为同步的顺序来书写，并且这个函数可以自动执行。
```



## Promise动态加载图片

### new Image()

**`Image()`**函数将会创建一个新的[`HTMLImageElement`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLImageElement)实例。

它的功能等价于 [`document.createElement('img') `](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createElement) 

> new出来的实例添加了src后就会动态加载图片了。



### Promise实现代码

```js
function loadImageAsync(url) {
    return new Promise((resolve, reject) => {
        let image = new Image();
        image.onload = function () {
            resolve(image);
        }
        image.onerror = function () {
            reject(new Error('Could not image at ' + url));
        }
        image.src = url;
    })
}
// 借一张淘宝的图嘿嘿嘿
loadImageAsync('https://img.alicdn.com/tfs/TB1VD1X1GL7gK0jSZFBXXXZZpXa-190-121.gif')
    .then((res) => {
        text.appendChild(res);
    }).catch((err) => {
        console.log(err);
    })
```



## 动态加载一个JS，并在加载成功后执行回调函数

1. 利用 `let srcipt = document.createElement('script')` 动态创建js
2. 利用 `srcipt.onload = callbank;` 将回调函数赋值给 onload 事件，js文件加载成功后就会执行该函数。

```js
function loadJS(url, callback) {
    let srcipt = document.createElement('script'),
        fn = callback || function () {};
    srcipt.type = 'text/javascript';
    srcipt.onload = fn;
    srcipt.src = url;
    console.log(srcipt);
    document.body.appendChild(srcipt);

}

loadJS('file.js', () => {
    console.log('加载完成');
})
```

> 这种封装如果请求失败就不会调用回调函数，并且会报错

+ 这个涉及到**按需加载js文件**，可以考虑一下如果多次请求，怎么让同样的文件只请求一次呢？

  > 可以利用object的特性，再利用闭包，如下：
  >
  > ```js
  > function loadJS(url, callback) {
  >     let script = document.createElement('script'),
  >         fn = callback || function () {};
  >     script.type = 'text/javascript';
  >     script.onload = fn;
  >     script.src = url;
  >     console.log(srcipt);
  >     document.body.appendChild(script);
  > 
  > }
  > // let scriptList = {};
  > let url1 = 'js/file.js',
  >     url2 = 'js/cccc.js',
  >     cb1 = () => {
  >         console.log('我是cb1');
  >     },
  >     cb2 = () => {
  >         console.log('我是cb2');
  >     };
  > 
  > // 检测加载的js是否有重复加载，如已加载过直接执行回调函数
  > function check(url, cb) {
  >     let scriptList = {};
  >     return function () {
  >         if (scriptList.hasOwnProperty(url)) {
  >             cb();
  >         } else {
  >             scriptList[url] = true;
  >             loadJS(url, cb);
  >         }
  >     }
  > }
  > 
  > let add = check(url1, cb1);
  > let add2 = check(url2, cb2);
  > ```
  >
  > 



## 什么是假值对象

+ 什么是假值

  在JavaScript中，false、null、0、”“、undefined 和 NaN被称为假值。

  规范中规定“所有的对象都是真值”，即使封装的内容是假值，这些对象依旧是真值。

+ 什么是假值对象

  在js代码中会出现对象判断为假的用法，但它实际上不属于JavaScript语言的范畴。跟浏览器有关。

  浏览器在某些特定情况下，在常规 JavaScript 语法基础上自己创建了一些外来值，这些就是“假值对象”。

  假值对象看起来和普通对象并无二致（都有属性，等等），但将它们强制类型转换为布尔值时结果为 false。

  最常见的例子是 document.all，它是一个类数组对象，包含了页面上的所有元素，由 DOM（而不是 JavaScript 引擎）提供给 JavaScript 程序使用。



## this对象的理解

### this的指向

> this永远指向最后调用它的那个对象

```js
var name = "windowsName";
var a = {
    name: "Cherry",
    fn : function () {
        console.log(this.name);      // Cherry
    }
}
a.fn();
```

+ a调用的fn，所以打印a的name

```js
var name = "windowsName";
var a = {
    name: "Cherry",
    fn : function () {
    	console.log(this.name);      // Cherry
    }
}
window.a.fn();
```

+ window调用a，a调用fn，最后调用fn的对象是a，即**this指向最后调用它的那个对象**

```js
var name = "windowsName";
var a = {
    // name: "Cherry",
    fn : function () {
    	console.log(this.name);      // undefined
    }
}
window.a.fn();
```

+ 这里为什么会打印 `undefined` 呢？这是因为正如刚刚所描述的那样，调用 fn 的是 a 对象，也就是说 fn 的内部的 this 是对象 a，而对象 a 中并没有对 name 进行定义，所以 log 的 `this.name` 的值是 `undefined`。
+ 这个例子还是说明了：**this 永远指向最后调用它的那个对象**，因为最后调用 fn 的对象是 a，所以就算 **a 中没有 name** 这个属性，也**不会**继续向上一个对象寻找 `this.name`，而是直接输出 `undefined`。

```js
var name = "windowsName";
var a = {
    name : null,
    // name: "Cherry",
    fn : function () {
    	console.log(this.name);      // windowsName
    }
}

var f = a.fn;
f();
```

+ 虽然将 a 对象的 fn 方法赋值给变量 f 了，但是**没有调用**。而**this永远执行指向最后调用它的那个对象**。最后调用 f 的是window，所以this指向window。

```js
var name = "windowsName";

function fn() {
    var name = 'Cherry';
    innerFunction();
    function innerFunction() {
    	console.log(this.name);      // windowsName
    }
}

fn()
```



### 怎么改变this的指向

有以下几种方法：

1. 使用 ES6 的箭头函数
2. 在函数内部使用 `_this = this` 
3. 使用 apply、call 、bind
4. new实例化一个对象

#### 箭头函数

> 箭头函数的 this 始终指向**函数定义时的 this**，而非执行时。

箭头函数没有 this 绑定，必须通过**查找作用域链**来决定其值，如果箭头函数被非箭头函数包含，则 this 绑定的是最近一层非箭头函数的 this ，否则，this 为 undefined。

```js
var name = "windowsName";

var a = {
    name : "Cherry",

    func1: function () {
        console.log(this.name)     
    },

    func2: function () {
        setTimeout( () => {
            this.func1()
        },100);
    }

};

a.func2()     // Cherry
```



#### 在函数内部使用 _this = this

如果不使用 ES6，那么这种方式应该是最简单的不会出错的方式了，我们是先将调用这个函数的对象保存在变量 `_this` 中，然后在函数中都使用这个 `_this`，这样 `_this` 就不会改变了。

```js
var name = "windowsName";

var a = {

    name : "Cherry",

    func1: function () {
        console.log(this.name)     
    },

    func2: function () {
        var _this = this;
        setTimeout( function() {
            _this.func1()
        },100);
    }

};

a.func2()       // Cherry
```



#### 使用 apply、call、bind

1. apply 用法：

```js
var a = {
    name : "Cherry",

    func1: function () {
        console.log(this.name)
    },

    func2: function () {
        setTimeout(  function () {
            this.func1()
        }.apply(a),100);
    }

};

a.func2()            // Cherry
```

2. call 用法：

```js
var a = {
    name : "Cherry",

    func1: function () {
        console.log(this.name)
    },

    func2: function () {
        setTimeout(  function () {
            this.func1()
        }.call(a),100);
    }

};

a.func2()            // Cherry
```

3. bind 用法

```js
var a = {
    name : "Cherry",

    func1: function () {
        console.log(this.name)
    },

    func2: function () {
        setTimeout(  function () {
            this.func1()
        }.bind(a)(),100);
    }

};

a.func2()            // Cherry
```

+ 三个的区别：
  + `fun.apply(thisArg, [argsArray])`
    + thisArg：第一个参数是fun函数运行时指定的 this 值
    + [argsArray]：一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 fun 函数
  + `fun.call(thisArg[, arg1[, arg2[, ...]]])`
    + thisArg：第一个参数是fun函数运行时指定的 this 值
    + [, arg1[, arg2[, ...]]]：传入若干个参数列表（apply 接收的是一个包含多个参数的数组）
  + `function.bind(thisArg[, arg1[, arg2[, ...]]])`
    + bind 和 call 传的参数一样，惟一不同的是 bind 是创建一个新的函数，需要手动去调用



#### 使用 new 实例化一个对象

当一个函数用作构造函数时（使用 new 关键字），它的 this 被绑定到正在构造的新对象。

> 虽然构造函数返回的默认值是 `this` 所指的那个对象，但它仍可以手动返回其他的对象（如果返回值不是一个对象，则返回 `this` 对象）。

```js
function C(){
  this.a = 37;
}

var o = new C();
console.log(o.a); // logs 37


function C2(){
  this.a = 37;
  return {a:38};
}

o = new C2();
console.log(o.a); // logs 38
```



### this 的四种调用模式

#### 函数调用模式

+ 当一个函数不是一个对象的属性时，直接作为函数来调用时，this 指向全局对象（严格模式是 undefined ）

> 默认绑定

#### 方法调用模式（隐式绑定）

+ 当一个函数作为一个对象的方法来调用时，this指向这个对象

> 隐式绑定

#### 构造器调用模式

+ 如果一个函数用 new 调用时，函数执行前会创建一个对象，this 指向这个新创建的对象
+ 涉及到另一个面试考点：[new的时候发生了什么](#new%E7%9A%84%E6%97%B6%E5%80%99%E5%8F%91%E7%94%9F%E4%BA%86%E4%BB%80%E4%B9%88) 

> new绑定

#### apply 、 call 和 bind 调用模式

+ 这三个方法都可以显式的指定调用函数的 this 指向

> 显式绑定



#### 四种模式的优先级

构造器调用模式 > apply、call 和 bind 调用模式 > 方法调用模式 > 函数调用模式





## 前端模块化AMD和requirejs、CMD和seajs

### AMD和requirejs

​		AMD规范采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。

​		这里介绍用require.js实现AMD规范的模块化：用`require.config()`指定引用路径等，用`define()`定义模块，用`require()`加载模块。

1. 首先引入requirejs文件和一个入口文件mainjs

   ```js
   /** 网页中引入require.js及main.js **/
   <script src="js/require.js" data-main="js/main"></script>
   
   /** main.js 入口文件/主模块 **/
   // 首先用config()指定各模块路径和引用名
   require.config({
     baseUrl: "js/lib",
     paths: {
       "jquery": "jquery.min",  //实际路径为js/lib/jquery.min.js
       "underscore": "underscore.min",
     }
   });
   // 执行基本操作
   require(["jquery","underscore"],function($,_){
     // some code here
   });
   
   ```

2. 引用模块的时候，我们将模块名放在`[]`中作为`reqiure()`的第一参数；如果我们定义的模块本身也依赖其他模块,那就需要将它们放在`[]`中作为`define()`的第一参数。

   ```js
   // 定义math.js模块
   define(function () {
       var basicNum = 0;
       var add = function (x, y) {
           return x + y;
       };
       return {
           add: add,
           basicNum :basicNum
       };
   });
   // 定义一个依赖underscore.js的模块
   define(['underscore'],function(_){
     var classify = function(list){
       _.countBy(list,function(num){
         return num > 30 ? 'old' : 'young';
       })
     };
     return {
       classify :classify
     };
   })
   
   // 引用模块，将模块放在[]内
   require(['jquery', 'math'],function($, math){
     var sum = math.add(10,20);
     $("#sum").html(sum);
   });
   
   ```



### CMD和seajs

​		CMD是另一种js模块化方案，它与AMD很类似，不同点在于：AMD 推崇依赖前置、提前执行，CMD推崇依赖就近、延迟执行。此规范其实是在sea.js推广过程中产生的。

```js
/** AMD写法 **/
define(["a", "b", "c", "d", "e", "f"], function(a, b, c, d, e, f) { 
     // 等于在最前面声明并初始化了要用到的所有模块
    a.doSomething();
    if (false) {
        // 即便没用到某个模块 b，但 b 还是提前执行了
        b.doSomething()
    } 
});

/** CMD写法 **/
define(function(require, exports, module) {
    var a = require('./a'); //在需要时申明
    a.doSomething();
    if (false) {
        var b = require('./b');
        b.doSomething();
    }
});

/** sea.js **/
// 定义模块 math.js
define(function(require, exports, module) {
    var $ = require('jquery.js');
    var add = function(a,b){
        return a+b;
    }
    exports.add = add;
});
// 加载模块
seajs.use(['math.js'], function(math){
    var sum = math.add(1+2);
});

```

