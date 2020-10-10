## 什么是Node.js

> Node.js是一个基于Chrome V8引擎的JavaScript运行环境

​		简单的来说就是一个运行环境，（就像js可以在浏览器中的V8引擎解析运行，这是前端的运行环境。）在该运行环境中，js就可以做后端开发。

![image-20201009211432407](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20201009211432407.png)

![image-20201009211450908](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20201009211450908.png)



## Node.js可以做什么

1. 基于Express框架（http://www.expressjs.com.cn/），可以快速构建Web应用
2. 基于Electron框架（https://electronjs.org/），可以构建跨平台的桌面应用
3. 基于restrify框架（http://restify.com/），可以快速构建API接口项目
4. 读写和操作数据库、创建实用的命令行工具辅助前端开发、etc



### 终端快捷键

1. 使用↑键，可以快速定位到上一次执行的命令
2. 使用tab键，能够快速补全路径
3. 使用esc键，能够快速清空当前已输入的命令



## Node.js模块

### 1. fs文件系统模块

> fs模块是Node.js官方提供的、用来操作文件的模块

+ `fs.readFile(path[, options], callback)`

  + 参数1：必选参数，string，表示文件的路径

  + 参数2：可选参数，表示以什么编码格式来读取文件

  + 参数3：必选参数，文件读取完成后（不管成功还是失败），通过回调函数拿到读取的结果

    ```js
    const fs = require('fs');
    
    fs.readFile('文件路径','utf8',(err, dataStr) => {
    	console.log(err); // 如果读取错误，err的值为错误对象，否则为null
    	console.log(dataStr); //如果读取成功，dataStr为文件的内容，否则为undefined
    });
    ```

  + 判断文件是否读取成功

    ```js
    const fs = require('fs');
    
    fs.readFile('文件路径','utf8',(err, result) => {
    	if (err) {
    		return console.log('文件读取失败！' + err.message);
    	}
    	
    	console.log('文件读取成功！内容是：' + result);
    });
    ```

+ `fs.writeFile(file, data[, options], callback)`

+ __dirname
  
  + `__dirname`表示当前文件所处的目录，代替文件路径的相对路径和绝对路径，移植性高



### 2. path路径模块

> path模块是Node.js官方提供的、用来处理路径的模块。

+ `path.join([...paths])`
  + ...paths <string> 路径片段的序列（多个字符串逗号分隔）
  + 返回值：<string>
  + 注意：涉及到路径拼接的操作，**都要使用path.join()方法进行处理**，不要直接使用+进行字符串的拼接
+ `path.basename([path[, ext]])`
  + path <string> 必选参数，表示一个路径的字符串
  + ext <string> 可选参数，表示文件扩展名
  + 返回：<string> 表示路径中的最后一部分（如果写了ext参数则只返回文件名字，不带扩展名）
+ `path.extname(path)`
  + 返回路径最后一部分的扩展名（包括.）



### 3. http模块

> http模块是Node.js官方提供的，用来创建web服务器的模块。通过http模块提供的`http.createServer()`方法，就能方便的把一台普通的电脑，变成一台Web服务器，从而对外提供Web资源服务。

#### 1）创建web服务器的基本步骤

1. 导入http模块

   `const http = require('http');`

2. 创建web服务器实例

   `const server = http.createServer();`

3. 为服务器实例**绑定request**事件

   ```js
   // 参数一：绑定的request事件 参数二：客户端向服务器发起请求时调用的函数
   server.on('request', (req, res) => {
       console.log('Someone visit our web server.');
   });
   ```

   + req 是请求对象，它包含了与客户端相关的数据和属性。例如：
     + req.url 是客户端请求的 URL 地址
     + req.method 是客户端的 method 请求类型
   + res 是响应对象，它包含了与服务器相关的数据和属性，例如：
     + `res.end(str)` 是向客户端发送指定的内容，并结束这次请求的处理过程
     + `res.setHeader('Content-Type', 'text/html; charest=utf-8')` 设置Content-Type，解决中文乱码问题

4. 监听客户端的请求，写好web服务的端口号和启动服务器的函数

   ```js
   // 参数一：端口号 参数二：启动服务器时调用的函数
   server.listen('8080', () => {
       console.log('serve running at http://127.0.0.1:8080');
   });
   ```




## Node.js中的模块化

### 1. 模块的三大分类

1. 内置模块
2. 用户自定义模块（js文件，需要写路径）
3. 第三方模块

### 2. `require`方法

使用`require()`方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用。

**注意**：使用`require()`方法加载其他模块时，会执行被加载模块中的代码

### 3. `module`对象

>  在每个.js自定义模块中都有一个module对象，它里面存储了和当前模块有关的信息

### 4. `module.exports`对象和`exports`对象

> 可以将模块内的成员共享出去，供外界使用

+ 默认为空对象
+ 使用`require`导入一个自定义模块的时候，得到的值就是`module.exports`
+ 默认情况下，`exports`和`module.exports`指向同一个对象，最终共享的结果，以`module.exports`为准

### 5. CommonJS模块化规范

> CommonJS规定了模块的特性和各模块之间如何相互依赖

CommonJS规定：

1. 每个模块内部，module变量代表当前模块
2. module变量是一个对象，它的exports属性是对外的接口。
3. 加载某个模块，其实是加载该模块的module.exports属性。require()方法用于加载模块。

