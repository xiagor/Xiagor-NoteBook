## 自己对`JQuery`的理解

我所理解的`JQuery`，他就是一个类库，并封装成一个对象，通过`$()`获取到的是一组类似Array的对象，它的`__proto__`有`JQuery`封装的各种方法可以使用。其中的`construtor`是这样的

```js
var a = $('.notMe');
console.log(a.constructor);
//输出：
ƒ ( selector, context ) {
    // The jQuery object is actually just the init constructor 'enhanced'
    return new jQuery.fn.init( selector, context, rootjQuery );
}
```

并且`a.__proto__.__proto__ === Object.prototype`

由此可知，他就是和Array同级，类似Array的一个轻量级类库



