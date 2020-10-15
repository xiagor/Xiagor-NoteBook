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



## NPM与包

> 包是基于内置模块封装出来的第三方模块

[npm包官方网站](www.npmjs.com)：可查找所有第三方包的文档

+ node_modules文件夹：存放所有已安装到项目中的包。require()导入第三方包时，就是从这个目录中查找并加载包。
+ package-lock.json配置文件：记录node_modules目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等。



### 1. package.json

因为第三方包的体积过大，不方便团队成员之间共享项目源代码，所以共享时需要剔除node_modules。

在项目根目录中，创建一个叫做package.json的配置文件，即可用来记录项目中安装了哪些包。

> 注意：在今后的项目开发中，一定要把node_modules文件夹，添加到.gitignore忽略文件中



+ 快速创建package.json：`npm init -y`
  + 上述命令只能在英文的目录下成功运行（不要使用中文，不能出现空格）
  + 创建package.json后，以后执行：npm install 包，npm包管理工具会自动把包的名称和版本号，记录到package.json中。
+ 执行`npm i`时
  + npm包管理工具会先读取package.json中的 dependencies 节点，读取到记录的所有依赖包和版本号之后，npm包管理工具会把这些包一次性下载到项目中

### 2. devDependencies节点

>  如果某些包只在项目开发阶段会用到，在项目上线之后不会用到，则建议把这些包记录到devDependencies节点中。
>
> 与之相应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到dependencies节点中。

+ 把包记录到devDependencies节点：`npm i 包名 -D`



### 3. nrm

为了更方便的切换下包的镜像源，可以安装nrm小工具，利用nrm提供的终端命令，可以快速查看和切换下包的镜像源。

1. 通过npm包管理器，将nrm安装为全局可用的工具

   `npm i nrm -g`

2. 查看所有可用的镜像源

   `nrm ls`

3. 将下包的镜像源切换为taobao镜像

   `nrm use taobao`



### 4. 包的分类

+ 项目包
  + 开发依赖包：devDependencies
  + 核心依赖包：dependencies
+ 全局包
  + 只有工具性质的包，才有全局安装的必要性，因为它们提供了好用的终端命令。
  + 全局包被安装到D:\nodejs\node_global\node_modules（我的电脑，这个不用管，装包的时候终端会告诉你的）



有哪些全局包呢：

1. nrm：管理镜像的小工具
2. i5ting_toc：把md文档转为html页面的小工具



### 5. 开发属于自己的包

包的目录：

 ![image-20201015090719564](C:\Users\xia\AppData\Roaming\Typora\typora-user-images\image-20201015090719564.png)

把根据不同的功能进行模块化，用js文件存放并放在src目录下，并用`module.exports`向外暴露成员，在index中引入暴露的模块

```js
//index.js包的入口文件

const date = require('./src/dataFormat');
const escape = require('./src/htmlEscape');

//用展开符展开所有属性，向外暴露需要的成员
module.exports = {
	...date,
	...escape
}
```

## 模块的加载机制

### 1. 优先从缓存中加载

+ 模块在第一次加载后会被缓存，这也意味着多次调用`require()`不会导致模块的代码被执行多次。从而提高模块的加载效率。

### 2. 内置模块的加载机制

+ 内置模块的加载优先级最高

### 3. 自定义模块的加载机制

+ 使用require()加载自定义模块时，必须指定以./或../开头的路径标识符。在加载自定义模块时，如果没有指定./或../这样的路径标识符，则node会把它当作内置模块或第三方模块进行加载
+ 同时，在require自定义模块时，如果省略了文件的扩展名，则Node.js会按顺序分别尝试加载以下的文件：
  + 按照确切的文件名进行加载（因为有可能有没有扩展名的文件）
  + 补全.js扩展名进行加载
  + 补全.json扩展名进行加载
  + 补全.node扩展名进行加载
  + 加载失败，终端报错

### 4. 第三方模块的加载机制

+ 如果传递给require()的模块标识符不是一个内置模块，也没有以./或者../开头，则Node.js会从当前模块的父目录开始，尝试从/node_modules文件夹中加载第三方模块
+ 如果没有找到对应的第三方模块，则移动再上一层父目录中进行加载，直到文件系统的根目录。

### 5. 目录作为模块

+ 当把目录作为模块标识符，传递给require()进行加载的时候，有三种加载方式：
  1. 在被加载的目录下查找一个叫做package.json的文件，并寻找main属性，作为require()加载的入口
  2. 如果目录里咩有package.json文件，或者main入口不存在或者无法解析，则Node.js将会试图加载目录下的index.js文件
  3. 如果以上两步都失败了，则Node.js会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'



## 什么是Express

> Express是基于Node.js平台，快速、开放、极简的Web开发框架

+ 本质：就是一个npm的第三方包，提供了快速创建Web服务器的便捷方法



## Express可以做什么

对于前端程序员来说，最常见的两种服务器，分别是：

+ Web网站服务器：专门对外提供Web网页资源的服务器
+ API接口服务器：专门对外提供API接口的服务器

使用Express，我们可以方便、快速的创建Web网站的服务器或者API接口的服务器



## 使用Express

### 1. 创建基本的web服务器

首先安装第三方包：npm i express

```js
const express = require('express');

const app = express();

app.listen(80, ()=>{
	console.log('express serve running at http://127.0.0.1');
})
```



### 2. 监听GET请求

用send方法给客户端发送内容

```js
app.get('客户端请求的URL地址',(req,res)=>{
	// 用send方法向客户端发送JSON对象
	res.send({name: 'zs', age: 20});
})
```



### 3. 获取URL中携带的查询参数

通过req.query对象，可以访问到客户端通过查询字符串的形式（比如`?name=zs&age=20`），发送到服务器的参数

+ `req.query`默认是一个空对象
+ 客户端通过查询字符串的形式（比如`?name=zs&age=20`），发送到服务器的参数，可以通过`req.query.name`访问到（它会自动解析到`req.query`这个对象中）

















