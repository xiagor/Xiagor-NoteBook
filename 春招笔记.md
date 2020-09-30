## HTML5的新特性

>  HTML：Hyper Text Markup Language，超文本标记语言

### 1. 语义化标签

`<header><article><footer><nav><aside><section>`

### 2. 增强型表单

+ **新的 form 属性：**
  + autocomplete
  + novalidate

+ **新的 input 属性：**
  + autocomplete
  + autofocus
  + form
  + form overrides (formaction, formenctype, formmethod, formnovalidate, formtarget)
  + height 和 width
  + list
  + min, max 和 step
  + multiple
  + pattern (regexp)
  + placeholder
  + required

### 3. 新增video和audio标签

### 4. 添加了canvas画布和svg，渲染矢量图片

+ **canvas：画线、画圆、渐变、添加图像到画布（通过js绘制2D图形）**
  + 依赖分辨率
  + 不支持事件处理器
  + 弱的文本渲染能力
  + 能够以 .png 或 .jpg 格式保存结果图像
  + 最适合图像密集型的游戏，其中的许多对象会被频繁重绘
+ **svg：可缩放矢量图形，使用XML格式定义图像**
  + 不依赖分辨率
  + 支持事件处理器
  + 最适合带有大型渲染区域的应用程序（比如谷歌地图）
  + 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
  + 不适合游戏应用

### 5. 地理定位

​	navigator对象里面有geolocation对象，其中有getCurrentPosition方法，可以获取地理的定位

### 6. 拖放API

拖（Drag）和放（drop），需要设置

+ 可拖动属性`draggable="true"`、
+ 拖放触发事件的属性`ondrop="drop(event)"`、`ondragstart="drag(event)"`、`ondragover="allowDrop(event)"`

### 7. Web Workers

当在HTML页面中执行脚本时，页面的状态时不可响应的，直到脚本已完成

Web Worker是运行在后台的JavaScript，独立于其他脚本，不会影响页面的性能。

1. 检测web worker支持

   ```javascript
   if(typeof(Worker)!=="undefined")
     {
     // Yes! Web worker support!
     // Some code.....
     }
   else
     {
     // Sorry! No Web Worker support..
     }
   ```

   

2. 创建web worker文件

   创建计数脚本，该脚本存储于“demo_workers.js”文件中

   ```javascript
   var i=0;
   
   function timedCount()
   {
       i=i+1;
       postMessage(i);	//postMessage()可以向HTML页面传回一段消息
       setTimeout("timedCount()",500);
   }
   
   timedCount();
   ```

   

3. 如果web worker支持，创建新的web worker对象，然后运行第二步中创建的js文件的代码。向web worker的实例添加一个`onmessage`事件监听器

   ```javascript
   if(typeof(w)=="undefined")
   {
   	w=new Worker("demo_workers.js");
   	w.onmessage=function(event){
       	document.getElementById("result").innerHTML=event.data;
       };
   }
   ```

   当web worker传递消息时（`postMessage()`方法可向HTML页面传回一段消息），会执行事件监听器中的代码。event.data中存有来自event.data的数据

4. 终止web worker

   当我们创建 web worker 对象后，它会继续监听消息（即使在外部脚本完成之后）直到其被终止为止。

   如需终止 web worker，并释放浏览器/计算机资源，请使用 terminate() 方法

   ```javascript
   w.terminate();
   ```

   

### 8. Web 存储

在客户端存储数据的新方法：

+ localStorage——没有时间限制的数据存储
+ sessionStorage——针对一个session的数据存储，当用户关闭浏览器窗口后，数据会被删除。



### 9. 应用程序缓存

通过创建cache manifest文件，可以轻松创建web应用的离线版本。



### 10. 服务器发送事件SSE

网页自动获取来自服务器的更新。

EventSource 对象用于接收服务器发送事件通知。

```javascript
var source=new EventSource("demo_sse.php");
source.onmessage=function(event)
{
  document.getElementById("result").innerHTML+=event.data + "<br />";
};
```

- 创建一个新的 EventSource 对象，然后规定发送更新的页面的 URL（本例中是 "demo_sse.php"）
- 每接收到一次更新，就会发生 onmessage 事件
- 当 onmessage 事件发生时，把已接收的数据推入 id 为 "result" 的元素中










