## 金蝶前端笔试题笔记

###  一、隐式转换类型

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



![img](http://p9.pstatp.com/large/pgc-image/1538025621414c490c46b28)

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



![js面试题大坑——隐式类型转换](http://p98.pstatp.com/large/pgc-image/1538025911178e28d7c85c1)







