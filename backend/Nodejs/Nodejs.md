# Nodejs

## 浏览器中的 JavaScript

![image-20220330223733756](http://zjp.hxkj.live/MDImage/Nodejs/%e6%b5%8f%e8%a7%88%e5%99%a8%e4%b8%ad%e7%9a%84JavaScript_2022-03-30_22-37-36.png)

![image-20220330223715753](http://zjp.hxkj.live/MDImage/Nodejs/%e6%b5%8f%e8%a7%88%e5%99%a8%e4%b8%ad%e7%9a%84JavaScript_2022-03-30_22-37-18.png)

![image-20220330223757269](http://zjp.hxkj.live/MDImage/Nodejs/%e6%b5%8f%e8%a7%88%e5%99%a8%e4%b8%ad%e7%9a%84JavaScript_2022-03-30_22-37-59.png)

![image-20220330224127269](http://zjp.hxkj.live/MDImage/Nodejs/%e6%b5%8f%e8%a7%88%e5%99%a8%e4%b8%ad%e7%9a%84JavaScript_2022-03-30_22-41-29.png)



## Node.js 介绍

- Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

- Nodejs 包含两个核心部分
  1. V8 引擎：负责解析和执行 JavaScript 代码
  2. 内置 API：提供了一些能力让我们可以调用 API 去做后端的一些东西。

 ![image-20220330224944067](http://zjp.hxkj.live/MDImage/Nodejs/Nodejs%e4%b8%ad%e7%9a%84JavaScript_2022-03-30_22-49-51.png)



## 可以做什么

1. 基于 Express 框架（http://www.expressjs.com.cn/），可以快速构建 Web 应用
2. 基于 Electron 框架（https://electronjs.org/），可以构建跨平台的桌面应用
3. 基于 restify 框架（http://restify.com/），可以快速构建 API 接口项目
4. 读写和操作数据库、创建实用的命令行工具辅助前端开发
5. ……



## 环境安装

- [下载地址](https://nodejs.org/zh-cn/) 
- 一路Next

### LTS版本和Current版本

- LTS 为长期稳定版，对于追求稳定性的企业级项目来说，推荐安装 LTS 版本的 Node.js。
- Current 为新特性尝鲜版，对热衷于尝试新特性的用户来说，推荐安装 Current 版本的 Node.js。但是，Current 版本中可能存在隐藏的 Bug 或安全性漏洞，因此不推荐在企业级项目中使用 Current 版本的 Node.js。



## 查看版本号

- 打开终端，在终端输入命令 node –v 后，按下回车键，即可查看已安装的 Node.js 的版本号。

```shell
# 查看版本号
node -v
```



## 执行 js 文件

- 打开终端，在终端输入命令 node js文件路径，即可执行 JavaScript 文件。

```shell
# 执行 js 文件
node 1.js
```

![image-20220330231606389](http://zjp.hxkj.live/MDImage/Nodejs/%e6%89%a7%e8%a1%8cjs%e6%96%87%e4%bb%b6_2022-03-30_23-16-13.png)



## 终端

- 终端（英文：Terminal）是专门为开发人员设计的，用于实现人机交互的一种方式。

- 使用快捷键（Windows徽标键 + R）打开运行面板，输入 cmd 后直接回车，即可打开终端。



### 终端快捷键

1. 使用 ↑ 键，可以快速定位到上一次执行的命令
2. 使用 tab 键，能够快速补全路径
3. 使用 esc 键，能够快速清空当前已输入的命令
4. 输入 cls 命令，可以清空终端
5. 输入 cd 命令，可以切换路径



## fs 文件系统模块

- fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。



### 导入 fs 模块

- 如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：

```javascript
// 导入 fs 模块
const fs = require('fs');
```



### 读取指定的文件中的内容

- 使用 fs.readFile() 方法，可以读取指定文件中的内容，语法格式如下：

```javascript
// 读取文件中的内容
fs.readFile(path[,options],callback) 
// 参数1(必选)：读取文件的存放路径
// 参数2(可选)：读取文件的时候采用的编码格式，一般指定 utf-8
// 参数3(必选)：回调函数，拿到读取失败和成功的结果 err：失败的结果 dataStr：成功的结果
```



```javascript
// 导入 fs 模块，来操作文件
const fs = require('fs');

fs.readFile('./test.txt', 'utf-8', function(err, dataStr) {
    // 如果读取成功，则err值为null
    // 如果读取失败，则err值为错误对象，dataStr值为undefined
    if (err == null) {
        console.log('读取文件成功：' + dataStr);
    } else {
        console.log('读取文件失败：' + err);
    }
});
```

- 可以判断 err 对象是否为 null，从而知晓文件读取的结果

```javascript
// 导入 fs 模块
const fs = require('fs');

fs.readFile('./test.txt', 'utf-8', function(err, dataStr) {
    // 如果读取成功，则err值为null
    // 如果读取失败，则err值为错误对象，dataStr值为undefined
    if (err) {
        console.log('读取文件失败：' + err);
        retrun;
    }
    console.log('读取文件成功：' + dataStr);
});
```



### 向指定的文件中写入内容

- 使用 fs.writeFile() 方法，可以向指定的文件中写入内容，语法格式如下：
- 注意：
  1. 写入的内容会覆盖原始内容。
  2. 如果文件不存在，会自动创建文件，但文件夹不存在，不会创建文件夹，会报错

```javascript
// 向文件写入指定内容
fs.writeFile(file,data[,options],callback)
// 参数1(必选)：写入文件的存放路径
// 参数2(必选)：表示写入的内容
// 参数3(可选)：写入文件的时候采用的编码式，一般指定utf-8
// 参数4(必选)：回调函数，拿到写入失败的结果 err：失败的结果
```





```javascript
// 导入fs模块，来操作文件
const fs = require('fs');

fs.writeFile('./test.txt', '输入数据', 'utf-8', function(err) {
    // 如果写入成功，则err值为null
    // 如果写入失败，则err值为错误对象
    if (err == null) {
        console.log('写入文件成功');
    } else {
        console.log('写入文件失败：' + err);
    }
});
```

- 可以判断 err 对象是否为 null，从而知晓文件写入的结果

```javascript
// 导入fs模块
const fs = require('fs');

fs.writeFile('./test.txt', '输入数据', 'utf-8', function(err) {
    // 如果写入成功，则err值为null
    // 如果写入失败，则err值为错误对象
    if (err) {
        console.log('写入文件失败：' + err);
        retrun;
    }
    console.log('写入文件成功');
});
```



### 路径动态拼接

- 在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。
- 原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。而不是执行的 js 文件目录！
- 解决方案 1：直接使用完整路径。

```javascript
// 移植性非常差、不利于维护
'G:\\study\\frontend\\Nodejs\\data\\day1\\code\\files\\1.txt'
```

- 解决方案 2：使用__dirname，标识当前文件所处目录

```javascript
// 标识当前文件所处的目录
console.log(__dirname); // 返回 G:\study\frontend\Nodejs\data\day1\code\files

console.log(__dirname + '/1.txt'); // 不推荐+号拼接路径
// 推荐 path.join 拼接路径
console.log(path.join(__dirname, './1.txt')); // 返回 G:\study\frontend\Nodejs\data\day1\code\files\1.txt
```



## path 路径模块

- path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。



### 导入 path 模块

```javascript
// 导入path模块
const path = require('path');
```



### 路径拼接

- 使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下：
- 注意：不要使用+来拼接路径，应该使用path.join()来拼接路径。

```javascript
path.join([...paths]) 把多个路径片段拼接为完整的路径字符串
// 参数1：路径片段的序列 
// 返回值: 路径拼接后的路径字符串
```





```javascript
// 导入path模块
const path = require('path');

// 注意:../会返回上一层路径
const pathStr = path.join('/a', '/b/c', '../', './d', 'e');
console.log(pathStr); // 返回 \a\b\d\e

console.log(path.join(__dirname, './1.txt')); // 返回 G:\study\frontend\Nodejs\data\day1\code\files\1.txt
```



### 获取路径中的文件名

- 使用 path.basename() 方法，可以从一个文件路径中，获取到文件的名称部分：

```javascript
// 获取路径中的文件名
path.basename(path[,ext]) 获取路径中文件名
// 参数1(必选):路径字符串
// 参数2(可选):文件的拓展名，输入后，返回值会删除拓展名
// 返回值：文件名字符串
```



```javascript
// 导入path模块
const path = require('path');

const fpath = path.join(__dirname, './test.txt');

var fullName = path.basename(fpath);
console.log(fullName); // 返回 test.txt

var nameWithoutExt = path.basename(fpath, '.txt');
console.log(nameWithoutExt); // 返回 test
```



### 获取路径中文件拓展名

- 使用 path.extname() 方法，可以获取路径中的扩展名部分，语法格式如下：

```javascript
// 获取路径中文件拓展名
var fext = path.extname(fpath);
// 参数1(必选):路径字符串
// 返回值：扩展名字符串
```



```javascript
// 导入path模块
const path = require('path');

const fpath = path.join(__dirname, './test.txt');

// path.extname(path) 获取路径中文件拓展名
// 参数1(必须):路径
var fext = path.extname(fpath);
console.log(fext); // 返回 .txt
```



## http 模块

- 在网络节点中，负责消费资源的电脑，叫做客户端；负责对外提供网络资源的电脑，叫做服务器。
- http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块。通过 http 模块提供的 http.createServer() 方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

- 服务器和普通电脑的**区别**在于，服务器上安装了 web 服务器软件，例如：IIS、Apache 等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器。
- 在 Node.js 中，我们不需要使用 IIS、Apache 等这些第三方 web 服务器软件。因为我们可以基于 Node.js 提供的 http 模块，**通过几行简单的代码，就能轻松的手写一个服务器软件**，从而对外提供 web 服务。





### IP 地址

- **IP** **地址**就是互联网上每台计算机的唯一地址，因此 IP 地址具有唯一性。如果把“个人电脑”比作“一台电话”，那么“IP地址”就相当于“电话号码”，只有在知道对方 IP 地址的前提下，才能与对应的电脑之间进行数据通信。
- IP 地址的格式：通常用“点分十进制”表示成（a.b.c.d）的形式，其中，a,b,c,d 都是 0~255 之间的十进制整数。例如：用点分十进表示的 IP地址（192.168.1.1）
- 注意
  - **互联网中每台 Web 服务器，都有自己的 IP地址**，例如：大家可以在 Windows 的终端中运行 ping www.baidu.com 命令，即可查看到百度服务器的 IP 地址。
  - 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入 127.0.0.1 这个 IP 地址，就能把自己的电脑当做一台服务器进行访问了。



### 域名和域名服务器

- 尽管 IP 地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套字符型的地址方案，即所谓的**域名（Domain Name）地址**。
- IP地址和域名是一一对应的关系，这份对应关系存放在一种叫做**域名服务器**(DNS，Domain name server)的电脑中。使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，**域名服务器就是提供 IP 地址和域名之间的转换服务的服务器**。
- 注意
  - 单纯使用 IP 地址，互联网中的电脑也能够正常工作。但是有了域名的加持，能让互联网的世界变得更加方便。
  - 在开发测试期间， 127.0.0.1 对应的域名是 localhost，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。



### 端口号

- 在一台电脑中，可以运行成百上千个 web 服务。每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的 web 服务进行处理。
- 注意
  - 每个端口号不能同时被多个 web 服务占用。
  - 在实际应用中，URL 中的 80 端口可以被省略。

![image-20220331215554069](http://zjp.hxkj.live/MDImage/Nodejs/%e7%ab%af%e5%8f%a3%e5%8f%b7_2022-03-31_21-56-04.png)



### 创建 web 服务器

- 步骤
  1. 导入 http 模块
  2. 创建 web 服务器实例
  3. 为服务器实例绑定 request 事件，监听客户端的请求
  4. 启动服务器

### 导入 http 模块

- 如果希望在自己的电脑上创建一个 web 服务器，从而对外提供 web 服务，则需要导入 http 模块

```javascript
// 导入http模块
const http = require('http');
```



### 创建 web 服务器实例

- 调用 http.createServer() 方法，即可快速创建一个 web 服务器实例：

```javascript
// 创建 web 服务器实例
const server = http.createServer();
```



### 为服务器实例绑定 request 事件

- 为服务器实例绑定 request 事件，即可监听客户端发送过来的网络请求

```javascript
// 使用服务器实例的 .on() 方法，为服务器绑定一个 request 事件
server.on('request',(req, res) =>{
    // 只要有客户端来请求我们自己的服务器，就会触发 request 事件，从而调用这个事件处理函数
    console.log('Someone visit our web server.')  
});
```



### 启动服务器

- 调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例

```javascript
// 调用 server.ten(端口号，成功后的回调函数) 方法，即可启动 web 服务器
server.listen(80, () =>{
    console.log('server running at http://127.0.0.1:8080')
});
```



### 创建 web 服务器（基本架构）

```javascript
// 1. 导入 http 模块
const http = require('http')
// 2. 创建 web 服务器实例
const server = http.createServer()
// 3. 为服务器实例绑定 request 事件，监听客户端的请求
server.on('request', function (req, res) {
  console.log('Someone visit our web server.')
})
// 4. 启动服务器
server.listen(80, function () {  
  console.log('server running at http://127.0.0.1:8080')
})
```



### requset 请求对象

- 只要服务器接收到了客户端的请求，就会调用通过 server.on() 为服务器绑定的 request 事件处理函数。
- 如果想在事件处理函数中，访问与**客户端**相关的**数据**或**属性**，可以使用如下的方式
- 注意：request.url 请求的 url 地址是从端口号后开始

```javascript
const http = require('http')
const server = http.createServer()


// 为服务器实例绑定 requset 事件，监听客户端的请求,只要有人通过客户端浏览器请求服务器，就会触发 requset 事件，从而执行回调函数
server.on('request', (request, response) => {
    // request.url 是客户端请求的 URL 地址
    const url = request.url;
    // request.method 是客户端请求的 method 类型，比如 GET / POST 请求
    const method = request.method;
    const str = `Your request url is ${url},and request method is ${method}`;
    console.log(str); // 如果地址是 http://127.0.0.1/ 返回 Your request url is /,and request method is GET
    //console.log(str); // 如果地址是 http://127.0.0.1/index.html 返回 Your request url is /index.html,and request method is GET
});


server.listen(80, () => {
  console.log('server running at http://127.0.0.1')
})
```





### response 响应对象

- 在服务器的 request 事件处理函数中，如果想访问与**服务器**相关的**数据**或**属性**，可以使用如下的方式



```javascript
const http = require('http')
const server = http.createServer()


// 为服务器实例绑定requset事件，监听客户端的请求,只要有人通过客户端浏览器请求服务器，就会触发requset事件，从而执行回调函数
server.on('request', (request, response) => {
    // request.url 是客户端请求的URL地址
    const url = request.url;
    // request.method 是客户端请求的method类型
    const method = request.method;
    const str = `您请求的url地址是 ${url},请求的method类型是 ${method}`;

    // 设置响应头，防止客户端响应内容为中文显示乱码的问题
    response.setHeader('Content-Type', 'text/html;charset=utf-8');
    // 向客户端响应内容，并且结束这次请求的处理过程
    response.end(str);
});


server.listen(80, () => {
  console.log('server running at http://127.0.0.1')
})
```



## web 服务器标准架构

- 步骤
  1. 导入需要的模块
  2. 创建基本的 web 服务器
  3. 将资源的请求 url 地址映射为文件的存放路径
  4. 读取文件内容并响应给客户端
  5. 优化资源的请求路径

```javascript
// 导入 http 模块
const http = require('http');
// 导入 fs 模块
const fs = require('fs');
// 导入 path 模块
const path = require('path');

// 创建web服务器实例
const server = http.createServer();

// 为服务器实例绑定requset事件，监听客户端的请求,只要有人通过客户端浏览器请求服务器，就会触发requset事件，从而执行回调函数
server.on('request', (request, response) => {
    // request.url 是客户端请求的URL地址
    const url = request.url;
    let fpath = '';
    if (url === '/') {
        fpath = path.join(__dirname, '/index.html');
    } else {
        fpath = path.join(__dirname, url);
    }

    // 根据“映射”过来的文件路径读取文件的内容
    fs.readFile(fpath, 'utf-8', (err, dataStr) => {
        if (err) {
            // 读取文件失败后，向客户端响应固定的"错误信息"
            response.end('404 Not found.');
        } 
        // 读取文件成功后，将“读取成功的内容”响应给客户端
        response.end(dataStr);

    });
});

// 启动服务器，设置端口
server.listen(80, function() {
    console.log('server running at http://127.0.0.1');
});
```



## 模块化

- **模块化**是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

- 编程领域中的模块化，就是**遵守固定的规则**，把一个大文件拆成独立并互相依赖的多个小模块。

- 好处：
  1. 提高了代码的复用性。
  2. 提高了代码的可维护性。
  3. 可以实现按需加载。



### 模块化规范

- **模块化规范**就是对代码进行模块化的拆分与组合时，需要遵守的那些规则。
- 例如
  - 使用什么样的语法格式来引用模块
  - 在模块中使用什么样的语法格式向外暴露成员
- 好处
  - 大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己。



### 模块的分类

- Node.js 中根据模块来源的不同，将模块分为了 3 大类，分别是
  1. 内置模块（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）
  2. 自定义模块（用户创建的每个 .js 文件，都是自定义模块）
  3. 第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）



### 加载模块

- 使用强大的 require() 方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用。例如：
- 加载用户自定义模块，需要指定路径，而加载内置模块和第三方模块不需要指定路径，只需要指定名称即可。
- 注意：使用 require() 方法加载其它模块时，会执行被加载模块中的代码。

```javascript
// 导入内置 http 模块
const http = require('http');

// 加载用户的自定义模块
const custom = require('./custom.js');
// 或者省略js后缀名
const custom = require('./custom');

// 加载第三方模块
const moment = require('moment');
```



### 模块作用域

- 和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做**模块作用域**。
- 好处：防止全局变量污染的问题。



### 向外共享模块作用域的成员

#### module 对象

- 在每个 .js 自定义模块中都有一个 module 对象，它里面**存储了和当前模块有关的信息**，打印如下：

![image-20220401004244346](http://zjp.hxkj.live/MDImage/Nodejs/module%e5%af%b9%e8%b1%a1_2022-04-01_00-42-51.png)



#### module.exports 对象

- 在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。
- 外界用 require() 方法导入自定义模块时，得到的就是 module.exports 所指向的对象。
- 在一个自定义模块中，默认情况下， module.exports = {}

```javascript
// 自定义模块.js
// 向module.exports对象上挂载username属性
module.exports.username = "hx";
// 向module.exports对象上挂载sayHello方法
module.exports.sayHello = function () {
    console.log('Hello');
}

// 或者

module.exports = {
    nickname: '小黑',
    sayHi() {
        console.log('Hi!')
    }
}
```

- 通过module.exports 对象向外共享模块作用域的成员

```javascript
// app.js
const m = require('./自定义模块');
console.log(m);
// 返回 { username: 'hx', sayHello: [Function (anonymous)] }

// 或者

// 返回 { nickname: '小黑', sayHi: [Function: sayHi] }
```



- 注意：
  - 使用 require() 方法导入模块时，导入的结果，**永远以** **module.exports** **指向的对象为准**。新指向会覆盖旧指向。
  - 在自定义模块中 module.exports 和 exports 代表的意思相同。如果同时出现，以 module.exports 指向的对象为准。
  - 使用时候避免同时使用 module.exports 和 exports。



#### exports 对象

- 由于 module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了 exports 对象。
- 默认情况下，exports 和 module.exports 指向同一个对象。最终共享的结果，还是以 module.exports 指向的对象为准。



### 模块化规范

- Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。
- CommonJS 规定：
  1. 每个模块内部，module 变量代表当前模块。
  2. module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口。
  3. 加载某个模块，其实是加载该模块的 module.exports 属性。require() 方法用于加载模块。



## npm 和包

### 包

- npm第三方模块又叫做包。就像电脑和计算机指的是相同的东西，第三方模块和包指的是同一个概念，只不过叫法不同。
- 不同于 Node.js 中的内置模块与自定义模块，包是由第三方个人或团队开发出来的，免费供所有人使用。
- 注意：Node.js 中的包都是免费且开源的，不需要付费即可免费下载使用。
- 由于 Node.js 的内置模块仅提供了一些底层的 API，导致在基于内置模块进行项目开发的时，效率很低。
- 包是基于内置模块封装出来的，提供了更高级、更方便的 API，极大的提高了开发效率。
- 包和内置模块之间的关系，类似于 jQuery 和 浏览器内置 API 之间的关系。
- [npm包搜索网站](https://www.npmjs.com/)
- [npm包下载服务器](https://registry.npmjs.org/)



### 下载包

- **npm, Inc.** **公司**提供了一个包管理工具，我们可以使用这个包管理工具，从 https://registry.npmjs.org/ 服务器把需要的包下载到本地使用。
- 这个包管理工具的名字叫做 Node Package Manager（简称 npm 包管理工具），这个包管理工具随着 Node.js 的安装包一起被安装到了用户的电脑上。
- 大家可以在终端中执行 **npm -v** 命令，来查看自己电脑上所安装的 npm 包管理工具的版本号：



### npm 包体验

#### 格式化时间

- 步骤
  1. 使用 npm 包管理工具，在项目中安装格式化时间的包 moment
  2. 使用 require() 导入格式化时间的包
  3. 参考 moment 的官方 API 文档对时间进行格式化

```javascript
// 1. 导入需要的包
// 注意：导入的名称，就是装包时候的名称
const moment = require('moment')

// 参考 momnet 官方 API 文档，调用对应的方法，对时间进行格式化
// 调用 moment() 方法，得到当前的时间
// 针对当前的时间，调用 format() 方法，按照指定的格式进行时间的格式化
const dt = moment().format('YYYY-MM-DD HH:mm:ss')
console.log(dt)
// 输出 2022-04-01 22::12:30
```



### 在项目中安装包的命令

- 如果想在项目中安装指定名称的包，需要运行如下的命令：

```shell
# 在项目中安装包的命令
npm install 包的完整名称
# 简写
npm i 包的完整名称
```



### 初次安装多了哪些文件

- 初次装包完成后，在项目文件夹下多一个叫做 node_modules 的文件夹和 package-lock.json 的配置文件。
- node_modules 文件夹用来存放所有已安装到项目中的包。require() 导入第三方包时，就是从这个目录中查找并加载包。
- package-lock.json 配置文件用来记录 node_modules 目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等。
- 注意：程序员不要手动修改 node_modules 或 package-lock.json 文件中的任何代码，npm 包管理工具会自动维护它们。



### 安装指定版本的包

- 默认情况下，使用 npm install 命令安装包的时候，会自动安装最新版本的包。如果需要安装指定版本的包，可以在包名之后，通过 @ 符号指定具体的版本，例如：

```shell
# 安装指定版本的包
npm i moment@2.22.2
```



### 包的语义化版本规范

- 包的版本号是以“点分十进制”形式进行定义的，总共有三位数字，例如 **2.24.0**
- 其中每一位数字所代表的的含义如下：
  - 第1位数字：大版本
  - 第2位数字：功能版本
  - 第3位数字：Bug修复版本

- 版本号提升的规则：只要前面的版本号增长了，则后面的版本号归零。



### 包管理配置文件

- npm 规定，在项目根目录中，**必须**提供一个叫做 package.json 的包管理配置文件。用来记录与项目有关的一些配置信息。例如：
  - 项目的名称、版本号、描述等
  - 项目中都用到了哪些包
  - 哪些包只在开发期间会用到
  - 那些包在开发和部署时都需要用到

![image-20220401222538448](http://zjp.hxkj.live/MDImage/Nodejs/%e5%8c%85%e7%ae%a1%e7%90%86%e9%85%8d%e7%bd%ae%e6%96%87%e4%bb%b6_2022-04-01_22-25-46.png)

#### 记录项目中安装了哪些包

- 在项目根目录中，创建一个叫做 package.json 的配置文件，即可用来记录项目中安装了哪些包。从而方便剔除 node_modules 目录之后，在团队成员之间共享项目的源代码。
- 注意：今后在项目开发中，一定要把 node_modules 文件夹，添加到 .gitignore 忽略文件中。



#### 快速创建 package.json

- npm 包管理工具提供了一个快捷命令，可以在执行命令时所处的目录中，快速创建 package.json 这个包管理配置文件：
- **在新建了项目文件夹以后，还没有写代码，就需要执行该命令，且只需要执行一次**

```shell
# 作用：在执行命令所处的目录中，快速新建 package.json 文件
npm init -y
```

- 注意：
  - 上述命令只能在英文的目录下成功运行！所以，项目文件夹的名称一定要使用英文命名，不要使用中文，不能出现空格。
  - 运行 npm install 命令安装包的时候，npm 包管理工具会自动把包的名称和版本号，记录到 package.json 中。

#### dependencies 节点

- package.json 文件中，有一个 dependencies 节点，专门用来记录您使用 npm install 命令安装了哪些包。

![image-20220401223331409](http://zjp.hxkj.live/MDImage/Nodejs/dependencies%e8%8a%82%e7%82%b9_2022-04-01_22-33-35.png)



#### 一次性安装所有的包

- 当我们拿到一个剔除了 node_modules 的项目之后，需要先把所有的包下载到项目中，才能将项目运行起来。
- 否则会报类似于下面的错误：

![image-20220401223500380](http://zjp.hxkj.live/MDImage/Nodejs/%e5%8c%85%e4%b8%a2%e5%a4%b1%e6%8a%a5%e9%94%99_2022-04-01_22-35-14.png)

- 可以运行 npm install 命令（或 npm i）一次性安装所有的依赖包，主要依靠 package.json 包管理配置文件。

```shell
# 执行 npm install 命令时，npm 包管理工具会先读取 package.json 中的 dependencies 节点
# 读取到记录的所有依赖包名称和版本号后，npm 包管理工具会把这些包一次性下载到项目中
npm install
# 或
npm i
```



#### devDependencies 节点

- 如果某些包**只在项目开发阶段**会用到，在**项目上线之后不会用到**，则建议把这些包记录到 devDependencies 节点中。
- 与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。

- 您可以使用如下的命令，将包记录到 devDependencies 节点中：

```shell
# 安装指定的包，并记录到 devDependencies 节点中
npm i 包名 -D

# 注意：上述命令是简写形式，完整写法为
npm install 包名 --save-dev
```



### 卸载包

- 可以运行 npm uninstall 命令，来卸载指定的包：

```shell
# 卸载包
npm uninstall 具体的包名

# 示例
npm uninstall moment
```

- 注意：npm uninstall 命令执行成功后，会把卸载的包，自动从 package.json 的 dependencies 中移除掉。



### 解决下包速度慢问题

#### 为什么会下载慢

- 在使用 npm 下包的时候，默认从国外的 https://registry.npmjs.org/ 服务器进行下载，此时，网络数据的传输需要经过漫长的海底光缆，因此下包速度会很慢。

#### 淘宝 npm 镜像服务器

- 淘宝在国内搭建了一个服务器，专门把国外官方服务器上的包同步到国内的服务器，然后在国内提供下包的服务。从而极大的提高了下包的速度。
- **镜像**（Mirroring）是一种文件存储形式，一个磁盘上的数据在另一个磁盘上存在一个完全相同的副本即为镜像。



#### 切换 npm 的下包镜像源

```shell
# 查看当前下包镜像源
npm config get registry
# 返回 https://registry.npmjs.org/

# 将下包的镜像源切换为淘宝镜像源
npm config set registry=https://registry.npmmirror.com/
npm config set registry=https://registry.npmjs.org/
# 检查镜像源是否下载成功
npm config get registry
```



#### nrm

- 为了更方便的切换下包的镜像源，我们可以安装 **nrm** 这个小工具，利用 nrm 提供的终端命令，可以快速查看和切换下包的镜像源。

```shell
# 通过npm包管理器，将 nrm 安装为全局可用的工具
npm i nrm -g

# 查看所有可用的镜像源
nrm ls

# 将下包的镜像源改为 taobao 镜像
nrm use taobao
# 将下包的镜像源改为官方服务器镜像
nrm use npm
```

![image-20220401225245417](http://zjp.hxkj.live/MDImage/Nodejs/nrm%e9%95%9c%e5%83%8f%e6%ba%90_2022-04-01_22-52-55.png)



### 包的分类

- 使用 npm 包管理工具下载的包，共分为两大类，分别是：
  1. 项目包
  2. 全局包

#### 项目包

- 那些被安装到项目的 node_modules 目录中的包，都是项目包。
- 项目包又分为两类，分别是：
  1. 开发依赖包（被记录到 devDependencies 节点中的包，只在开发期间会用到）
  2. 核心依赖包（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）

```shell
# 安装项目核心依赖包
npm i 包名
# 安装项目开发依赖包
npm i 包名 -D

# 卸载项目安装的包
npm uninstall 包名
```



#### 全局包

- 在执行 npm install 命令时，如果提供了 -g 参数，则会把包安装为全局包。
- 全局包会被安装到 C:\Users\用户目录\AppData\Roaming\npm\node_modules 目录下。
- 注意：
  - 只有工具性质的包，才有全局安装的必要性。因为它们提供了好用的终端命令。
  - 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可。

```shell
# 安装全局指定的包
npm i 包名 -g
# 卸载全局安装的包
npm uninstall 包名 -g
```



### i5ting_toc包

- i5ting_toc 是一个可以把 md 文档转为 html 页面的小工具，使用步骤如下：

```shell
# 将 i5ting_toc 安装为全局包
npm install -g i5ting_toc
# 调用 i5ting_toc ,实现 md 转 html 的功能
i5ting_toc -f 要转换的md文件路径 -o
```



### 规范的包结构

- 一个规范的包，它的组成结构，必须符合以下 3 点要求：
  1. 包必须以单独的目录而存在
  2. 包的顶级目录下要必须包含 package.json 这个包管理配置文件
  3. package.json 中必须包含 name，version，main 这三个属性，分别代表包的名字、版本号、包的入口。



## 开发属于自己的包

###  需要实现的功能

![image-20220401231415022](http://zjp.hxkj.live/MDImage/Nodejs/%e5%bc%80%e5%8f%91%e5%b1%9e%e4%ba%8e%e8%87%aa%e5%b7%b1%e7%9a%84%e5%8c%85_2022-04-01_23-14-21.png)

![image-20220401231429355](http://zjp.hxkj.live/MDImage/Nodejs/%e5%bc%80%e5%8f%91%e5%b1%9e%e4%ba%8e%e8%87%aa%e5%b7%b1%e7%9a%84%e5%8c%85_2022-04-01_23-14-31.png)

![image-20220401231436844](http://zjp.hxkj.live/MDImage/Nodejs/%e5%bc%80%e5%8f%91%e5%b1%9e%e4%ba%8e%e8%87%aa%e5%b7%b1%e7%9a%84%e5%8c%85_2022-04-01_23-14-39.png)

### 初始化包的基本结构

1. 新建 itheima-tools 文件夹，作为包的根目录
2. 在 itheima-tools 文件夹中，新建三个文件：
   1. package.json（包管理配置文件）
   2. index.js（包的入口文件）
   3. README.md（包的说明文档）



### 初始化 package.json

- name：包的名称（包的名称不能与 npm 上已有的包名称重复）
- version：版本号，默认从 1.0.0 开始
- main：指定包的入口
- description：包的简短描述信息
- keywords：数组，为 npm 官网包搜索的关键字
- licnese：开源许可协议，默认 ISC

![image-20220401231703003](http://zjp.hxkj.live/MDImage/Nodejs/%e5%88%9d%e5%a7%8b%e5%8c%96package.json_2022-04-01_23-17-15.png)

### 在 index.js 中定义格式化时间的方法

```javascript
// 定义格式化时间的函数
function dateFormat(dateStr) {
  const dt = new Date(dateStr)

  const y = dt.getFullYear()
  const m = padZero(dt.getMonth() + 1)
  const d = padZero(dt.getDate())

  const hh = padZero(dt.getHours())
  const mm = padZero(dt.getMinutes())
  const ss = padZero(dt.getSeconds())

  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}

// 定义一个补零的函数
function padZero(n) {
  return n > 9 ? n : '0' + n
}

module.exports = {
  dateFormat
}

```



### 在 index.js 中定义转义 HTML 和还原 HTML 的方法

```javascript
// 定义转义 HTML 字符的函数
function htmlEscape(htmlstr) {
  return htmlstr.replace(/<|>|"|&/g, match => {
    switch (match) {
      case '<':
        return '&lt;'
      case '>':
        return '&gt;'
      case '"':
        return '&quot;'
      case '&':
        return '&amp;'
    }
  })
}

// 定义还原 HTML 字符串的函数
function htmlUnEscape(str) {
  return str.replace(/&lt;|&gt;|&quot;|&amp;/g, match => {
    switch (match) {
      case '&lt;':
        return '<'
      case '&gt;':
        return '>'
      case '&quot;':
        return '"'
      case '&amp;':
        return '&'
    }
  })
}

module.exports = {
  htmlEscape,
  htmlUnEscape
}
```



### 将不同的功能进行模块化拆分

1. 将格式化时间的功能，拆分到 src -> dateFormat.js 中
2. 将处理 HTML 字符串的功能，拆分到 src -> htmlEscape.js 中
3. 在 index.js 中，导入两个模块，得到需要向外共享的方法
4. 在 index.js 中，使用 module.exports 把对应的方法共享出去

```javascript
// index.js
// 这是包的入口文件

const date = require('./src/dateFormat')
const escape = require('./src/htmlEscape')

// 向外暴露需要的成员
module.exports = {
  // ... 展开运算符，展开对象中的内容
  ...date,
  ...escape
}
```



```javascript
// 测试，require 会自动到路径下的 package.json 中找到 main 对应的文件名，作为导入文件
const itheima = require('./itheima-tools')

// 格式化时间的功能
const dtStr = itheima.dateFormat(new Date())
console.log(dtStr)
console.log('-----------')

const htmlStr = '<h1 title="abc">这是h1标签<span>123&nbsp;</span></h1>'
const str = itheima.htmlEscape(htmlStr)
console.log(str)
console.log('-----------')

const str2 = itheima.htmlUnEscape(str)
console.log(str2)
```



### 编写包的说明文档

- 包根目录中的 README.md 文件，是包的使用说明文档。通过它，我们可以事先把包的使用说明，以 markdown 的格式写出来，方便用户参考。
- README 文件中具体写什么内容，没有强制性的要求；只要能够清晰地把包的作用、用法、注意事项等描述清楚即可。
- 我们所创建的这个包的 README.md 文档中，会包含以下 6 项内容：
- 安装方式、导入方式、格式化时间、转义 HTML 中的特殊字符、还原 HTML 中的特殊字符、开源协议。

````markdown
## 安装
```shell
npm install itheima-tools
```

## 导入
```javascript
const itheima = require('itheima-tools')
```

## 格式化时间
```javascript
// 调用 dateFormat 对时间进行格式化
const dtStr = itheima.dateFormat(new Date())
// 结果  2020-04-03 17:20:58
console.log(dtStr)
```

## 转义 HTML 中的特殊字符
```javascript
// 带转换的 HTML 字符串
const htmlStr = '<h1 title="abc">这是h1标签<span>123&nbsp;</span></h1>'
// 调用 htmlEscape 方法进行转换
const str = itheima.htmlEscape(htmlStr)
// 转换的结果 &lt;h1 title=&quot;abc&quot;&gt;这是h1标签&lt;span&gt;123&amp;nbsp;&lt;/span&gt;&lt;/h1&gt;
console.log(str)
```

## 还原 HTML 中的特殊字符
```javascript
// 待还原的 HTML 字符串
const str2 = itheima.htmlUnEscape(str)
// 输出的结果 <h1 title="abc">这是h1标签<span>123&nbsp;</span></h1>
console.log(str2)
```

## 开源协议
ISC
````



### 发布 npm 包

#### 注册 npm 包

1. 访问 https://www.npmjs.com/ 网站，点击 sign up 按钮，进入注册用户界面
2. 填写账号相关的信息：Full Name、Public Email、Username、Password
3. 点击 Create an Account 按钮，注册账号
4. 登录邮箱，点击验证链接，进行账号的验证



#### 登录 npm 账号

- npm 账号注册完成后，可以在终端中执行 npm login 命令，依次输入用户名、密码、邮箱后，即可登录成功。
- 注意：在运行 npm login 命令之前，必须先把下包的服务器地址切换为 npm 的官方服务器。否则会导致发布包失败！

![image-20220401235426969](http://zjp.hxkj.live/MDImage/Nodejs/%e7%99%bb%e5%bd%95npm%e8%b4%a6%e6%88%b7_2022-04-01_23-54-35.png)

#### 把包发布到 npm 上

- 将终端切换到包的根目录之后，运行 npm publish 命令，即可将包发布到 npm 上（注意：包名不能雷同）。

![image-20220401235413444](http://zjp.hxkj.live/MDImage/Nodejs/%e6%8a%8a%e5%8c%85%e5%8f%91%e5%b8%83%e5%88%b0npm%e4%b8%8a_2022-04-01_23-54-22.png)

#### 删除已发布的包

- 运行 npm unpublish 包名 --force 命令，即可从 npm 删除已发布的包。
- 注意
  - npm unpublish 命令只能删除 72 小时以内发布的包
  - npm unpublish 删除的包，在 24 小时内不允许重复发布
  - 发布包的时候要慎重，尽量不要往 npm 上发布没有意义的包！

![image-20220401235727280](http://zjp.hxkj.live/MDImage/Nodejs/%e5%88%a0%e9%99%a4%e5%b7%b2%e5%8f%91%e5%b8%83%e7%9a%84%e5%8c%85_2022-04-01_23-57-38.png)



## 模块的加载机制

### 优先从缓存中加载

- **模块在第一次加载后会被缓存**。 这也意味着多次调用 require() 不会导致模块的代码被执行多次。
- 注意：不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率。

### 内置模块的加载机制

- 内置模块是由 Node.js 官方提供的模块，内置模块的加载优先级最高。
- 例如，require('fs') 始终返回内置的 fs 模块，即使在 node_modules 目录下有名字相同的包也叫做 fs。

### 自定义模块的加载机制

- 使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。在加载自定义模块时，如果没有指定 ./ 或 ../ 这样的路径标识符，则 node 会把它当作内置模块或第三方模块进行加载。
- 同时，在使用 require() 导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：
  1. 按照确切的文件名进行加载
  2. 补全 .js 扩展名进行加载
  3. 补全 .json 扩展名进行加载
  4. 补全 .node 扩展名进行加载
  5. 加载失败，终端报错

### 第三方模块的加载机制

- 如果传递给 require() 的模块标识符不是一个内置模块，也没有以 ‘./’ 或 ‘../’ 开头，则 Node.js 会从当前模块的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块。

- 如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。
- 例如，假设在 'C:\Users\itheima\project\foo.js' 文件里调用了 require('tools')，则 Node.js 会按以下顺序查找：
  - C:\Users\itheima\project\node_modules\tools
  - C:\Users\itheima\node_modules\tools
  - C:\Users\node_modules\tools
  - C:\node_modules\tools

### 目录作为模块

- 当把目录作为模块标识符，传递给 require() 进行加载的时候，有三种加载方式
  1. 在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口
  2. 如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件
  3. 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'



## Express

- 官方给出的概念：Express 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架。
- Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。
- **Express** **的本质**：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。
- 类似于浏览器中 Web API 和 jQuery 的关系。Express 是基于 http 模块进一步封装出来的。



### 作用

- 对于前端程序员来说，最常见的两种服务器，分别是：
  1. Web 网站服务器：专门对外提供 Web 网页资源的服务器。
  2. API 接口服务器：专门对外提供 API 接口的服务器。
- 使用 Express，我们可以方便、快速的创建 Web 网站的服务器或 API 接口的服务器。



### 安装

- 在项目所处的目录中，运行如下的终端命令，即可将 express 安装到项目中使用：

```shell
npm i express@4.17.1
```



### 创建基本的 web 服务器

```javascript
// 导入 express
const express = require('express');
// 创建 web 服务器
const app = express();

// 调用 app.listen (端口号，启动成功后的回调函数)，启动服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
})
```



### 监听 GET 请求

- 通过 app.get() 方法，可以监听客户端的 GET 请求，具体的语法格式如下：

```javascript
// 参数1:客户端请求的 URL 地址
// 参数2:请求对应的处理函数
//		requset:请求对象（包含了与请求相关的属性和方法）
//      response:响应对象（包含了与对应相关的属性和方法）
app.get('请求 URL',(requset, response) =>{
    /* 处理函数 */
});
```



### 监听 POST 请求

- 通过 app.post() 方法，可以监听客户端的 POST 请求，具体的语法格式如下：

```javascript
// 参数1:客户端请求的 URL 地址
// 参数2:请求对应的处理函数
//		requset:请求对象（包含了与请求相关的属性和方法）
//      response:响应对象（包含了与对应相关的属性和方法）
app.post('请求 URL',(requset, response) =>{
    /* 处理函数 */
});
```



### 把内容响应给客户端

- 通过 requset.send() 方法，可以把处理好的内容，发送给客户端：

```javascript
app.get('/user', (request, response) => {
    // 向客户端发送 JSON 对象
    response.send({ name: 'zs', age: 20, gender: '男' });
});

app.post('/user', (request, response) => {
    // 向客户端发送文本内容
    response.send('请求成功');
});
```



### 获取 URL 中携带的查询参数

- 通过 req.query 对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数：

```javascript
app.get('/', (request, response) => {
    // 通过 request.query 可以获取到客户端发送过来的查询参数
    // 注意：默认情况下，request.query 是一个空对象 {}
    console.log(request.query);
    res.send(request.query);
    // 客户端使用 ?name=zs&age=20 这种查询字符串的形式，发送到服务器的参数
    // 可以通过 request.query 对象访问到
    // request.query.name
    // request.query.age

})
```



![image-20220403182923858](http://zjp.hxkj.live/MDImage/Nodejs/%e8%8e%b7%e5%8f%96URL%e4%b8%ad%e6%90%ba%e5%b8%a6%e7%9a%84%e6%9f%a5%e8%af%a2%e5%8f%82%e6%95%b0_2022-04-03_18-29-34.png)



### 获取 URL 中的动态参数

- 通过 req.params 对象，可以访问到 URL 中，通过 **:** 匹配到的动态参数：
- : 后面的动态参数名可根据需求修改
- 可以有多个动态参数

```javascript
// 注意：这里的 :id 是一个动态的参数
app.get('/user/:ids/:username', (req, res) => {
    // req.params 是动态匹配到的 URL 参数，默认也是一个空对象
    console.log(req.params)
    res.send(req.params)
})
```



![image-20220403183713505](http://zjp.hxkj.live/MDImage/Nodejs/%e8%8e%b7%e5%8f%96URL%e4%b8%ad%e7%9a%84%e5%8a%a8%e6%80%81%e5%8f%82%e6%95%b0_2022-04-03_18-37-25.png)





### 托管静态资源

- express 提供了一个非常好用的函数，叫做 express.static()，通过它，我们可以非常方便地创建一个静态资源服务器，
- 例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

```javascript
// 托管静态资源
app.use(express.static('public'));
```

- 现在，你就可以访问 public 目录中的所有文件了：
  - http://127.0.0.1/index.html
  - http://127.0.0.1/index.css
  - http://127.0.0.1/index.js

- **注意：**Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在 URL 中。

  



```javascript
const express = require('express')
const app = express()

// 在这里，调用 express.static() 方法，快速的对外提供静态资源
app.use(express.static('./clock'))

app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
}) 
```



#### 托管多个静态资源目录

- 如果要托管多个静态资源目录，请多次调用 express.static() 函数
- 访问静态资源文件时，express.static() 函数会根据目录的添加顺序查找所需的文件，查找文件有先后顺序，先托管的先找。

```javascript
app.use(express.static('./files'))
app.use(express.static('./clock'))
```



#### 挂载路径前缀

- 如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式：
- 使用该方法，可以避免文件重名。

```javascript
app.use('/files', express.static('./files'))
```



### nodemon

- 在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐。
- 现在，我们可以使用 nodemon（https://www.npmjs.com/package/nodemon） 这个工具，它能够监听项目文件的变动，当代码被修改后，nodemon 会自动帮我们重启项目，极大方便了开发和调试。

#### 安装

- 在终端中，运行如下命令，即可将 nodemon 安装为全局可用的工具：

```shell
npm i -g nodemon
```



#### 使用 nodemon

- 当基于 Node.js 编写了一个网站应用的时候，传统的方式，是运行 node app.js 命令，来启动项目。这样做的坏处是：代码被修改之后，需要手动重启项目。
- 现在，我们可以将 node 命令替换为 nodemon 命令，使用 nodemon app.js 来启动项目。这样做的好处是：代码被修改之后，会被 nodemon 监听到，从而实现自动重启项目的效果。

```shell
node app.js
# 将上面的终端命令，替换为下面的终端命令，即可实现自动重启项目的效果
nodemon app.js
```



## 路由

- 路由就是映射关系。

![image-20220403234948160](http://zjp.hxkj.live/MDImage/Nodejs/%e8%b7%af%e7%94%b1%e7%9a%84%e6%a6%82%e5%bf%b5_2022-04-03_23-49-57.png)

### Express 中的路由

- 在 Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系。
- Express 中的路由分 3 部分组成，分别是请求的类型、请求的 URL 地址、处理函数，格式如下：

```javascript
app.METHOD(PATH,HANDLER)
```

- 例如：

```javascript
// 挂载路由
app.get('/', (req, res) => {
  res.send('hello world.')
})
app.post('/', (req, res) => {
  res.send('Post Request.')
})
```



### 路由的匹配过程

- 每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。
- 在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的 URL 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

![image-20220403235528098](http://zjp.hxkj.live/MDImage/Nodejs/%e8%b7%af%e7%94%b1%e7%9a%84%e5%8c%b9%e9%85%8d%e8%bf%87%e7%a8%8b_2022-04-03_23-55-30.png)

- 注意：
  1. 按照定义的先后顺序进行匹配
  2. 请求类型和请求的URL同时匹配成功，才会调用对应的处理函数



### 最简单用法

- 在 Express 中使用路由最简单的方式，就是把路由挂载到 app 上，示例代码如下：

```javascript
const express = require('express')
const app = express()

// 挂载路由
app.get('/', (req, res) => {
  res.send('hello world.')
})
app.post('/', (req, res) => {
  res.send('Post Request.')
})

app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```



### 模块化路由

- 为了方便对路由进行模块化的管理，Express **不建议**将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。

- 将路由抽离为单独模块的步骤如下：
  1. 创建路由模块对应的 .js 文件
  2. 调用 express.Router() 函数创建路由对象
  3. 向路由对象上挂载具体的路由
  4. 使用 module.exports 向外共享路由对象
  5. 使用 app.use() 函数注册路由模块



#### 创建路由模块

```javascript
// 这是路由模块
// 导入 express
const express = require('express')
// 创建路由对象
const router = express.Router()

// 挂载获取用户列表的路由
router.get('/user/list', (req, res) => {
    res.send('Get user list.')
})
// 挂载添加用户的路由
router.post('/user/add', (req, res) => {
    res.send('Add new user.')
})

// 向外导出路由对象
module.exports = router
```



#### 注册路由模块

- 导入路由模块

```javascript
// 导入路由模块
const userRouter = require('./router/user.js');
// 使用 app.use() 注册路由模块
app.use(userRouter)
```



#### 为路由模块添加前缀

- 类似于托管静态资源时，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也非常简单：

```javascript
// 导入路由模块
const userRouter = require('./router/user.js');

// 使用 app.use() 注册路由模块，并添加统一的访问前缀 /api
app.use('/api', userRouter)
```

```javascript
// 这是服务器模块
const express = require('express')
const app = express()

// app.use('/files', express.static('./files'))

// 1. 导入路由模块
const router = require('./03.router')
// 2. 注册路由模块
app.use('/api', router)

// 注意： app.use() 函数的作用，就是来注册全局中间件

app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```



## 中间件

- 中间件（Middleware ），特指业务流程的中间处理环节。

![image-20220404003527604](http://zjp.hxkj.live/MDImage/Nodejs/%e4%b8%ad%e9%97%b4%e4%bb%b6_2022-04-04_00-35-35.png)



### Express 中间件的调用流程

- 当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

![image-20220404003623181](http://zjp.hxkj.live/MDImage/Nodejs/Express%e4%b8%ad%e9%97%b4%e4%bb%b6_2022-04-04_00-36-29.png)

### Express 中间件的格式

- Express 的中间件，本质上就是一个 function 处理函数，Express 中间件的格式如下：

![image-20220404003815711](http://zjp.hxkj.live/MDImage/Nodejs/Express%e4%b8%ad%e9%97%b4%e4%bb%b6%e7%9a%84%e6%a0%bc%e5%bc%8f_2022-04-04_00-38-22.png)

- 注意：中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res。



### next 函数的作用

- next 函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

![image-20220404004145059](http://zjp.hxkj.live/MDImage/Nodejs/%e4%b8%ad%e9%97%b4%e4%bb%b6next%e5%87%bd%e6%95%b0_2022-04-04_00-41-53.png)



### 定义中间件函数

- 可以通过如下的方式，定义一个最简单的中间件函数：

```javascript
// 常量 mw 所指向的，就是一个中间件函数
const mw = function(req, res, next){
    console.log('这是一个最简单的中间件函数');
    // 注意：在当前中间件的业务处理完毕后，必须调用 next() 函数
    // 表示把流转关系交给下一个中间件或路由
    next();
}
```



### 全局生效的中间件

- 客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。
- 通过调用 app.use(中间件函数)，即可定义一个全局生效的中间件，示例代码如下：

```javascript
// 常量 mw 所指向的，就是一个中间件函数
const mw = function(req, res, next){
    console.log('这是一个简单的中间件函数');
    next();
}

// 全局生效的中间件
app.use(mw);
```



```javascript
// 简化版
// 全局生效的中间件
app.use((req, res, next) => {
    console.log('这是一个简单的中间件函数');
    next();
})
```



### 中间件的作用

- 多个中间件之间，**共享同一份 req 和 res**。基于这样的特性，我们可以在上游的中间件中，**统一为 req 或 res 对象添加自定义的属性或方法**，供下游的中间件或路由进行使用。

![image-20220404142604898](http://zjp.hxkj.live/MDImage/Nodejs/%e4%b8%ad%e9%97%b4%e4%bb%b6%e7%9a%84%e4%bd%9c%e7%94%a8_2022-04-04_14-26-10.png)

```javascript
const express = require('express')
const app = express()

// 这是定义全局中间件的简化形式
app.use((req, res, next) => {
    // 获取到请求到达服务器的时间
    const time = Date.now()
        // 为 req 对象，挂载自定义属性，从而把时间共享给后面的所有路由
    req.startTime = time
    next()
})

app.get('/', (req, res) => {
    res.send('Home page.' + req.startTime)
})
app.get('/user', (req, res) => {
    res.send('User page.' + req.startTime)
})

app.listen(80, () => {
    console.log('http://127.0.0.1')
})
```



### 定义多个全局中间件

- 可以使用 app.use() 连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行调用，示例代码如下：

```javascript
const express = require('express')
const app = express()

// 定义第一个全局中间件
app.use((req, res, next) => {
  console.log('调用了第1个全局中间件')
  next()
})
// 定义第二个全局中间件
app.use((req, res, next) => {
  console.log('调用了第2个全局中间件')
  next()
})

// 定义一个路由
app.get('/user', (req, res) => {
  res.send('User page.')
})

app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```



### 局部生效的中间件

- 不使用 app.use() 定义的中间件，叫做局部生效的中间件，示例代码如下：

```javascript
// 定义中间件函数 mw1
const mw1 = function(req, res, next){
    console.log('这是中间件函数');
    next();
}
// mw1 这个中间件只在"当前路由中生效"，这种用法属于"局部生效的中间件"
// 先执行局部生效的中间件，再执行回调函数
app.get('/', mw1, function(req, res)){
	res.send('Home page');        
}
```



### 定义多个局部中间件

- 可以在路由中，通过如下两种等价的方式，使用多个局部中间件：

```javascript
// 以下两种写法是"完全等价"的，可根据自己的喜好，选择任意一种方式进行使用
app.get('/', mw1, mw2, (req, res) => {
    res.send('Home page.');
});

app.get('/', [mw1, mw2], (req, res) => {
    res.send('Home page.');
})
```



### 使用事项

1. 一定要在路由之前注册中间件
2. 客户端发送过来的请求，可以连续调用多个中间件进行处理
3. 执行完中间件的业务代码之后，不要忘记调用 next() 函数
4. 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码
5. 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象



### 中间件的分类

- 为了方便大家理解和记忆中间件的使用，Express 官方把常见的中间件用法，分成了 5 大类，分别是：
  1. 应用级别的中间件
  2. 路由级别的中间件
  3. 错误级别的中间件
  4. Express 内置的中间件
  5. 第三方的中间件

#### 应用级别的中间件

- 通过 app.use() 或 app.get() 或 app.post() ，绑定到 app 实例上的中间件，叫做应用级别的中间件，代码示例如下：

```javascript
// 应用级别的中间件（全局中间件）
app.use((req, res, next) => {
    next();
})

// 应用级别的中间件（局部中间件）
app.get('/', mw1, (req, res) => {
    res.send('Home page.');
});
```



#### 路由级别的中间件

- 绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过，应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上，代码示例如下：

```javascript
const app = express()
const router = express.Router()

// 路由级别的中间件
router.use((req, res, next){
	console.log('Time:', Date.now());
	next();
});

app.use('/', router);
```



#### 错误级别的中间件

- 错误级别中间件的作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。
- 格式：错误级别中间件的 function 处理函数中，必须有 4 个形参，形参顺序从前到后，分别是 (err, req, res, next)。
- 注意：错误级别的中间件，必须注册在所有路由之后

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 1. 定义路由
app.get('/', (req, res) => {
    // 人为的制造错误
    // 抛出一个自定义的错误
    throw new Error('服务器内部发生了错误！')
    res.send('Home page.')
})

// 2. 定义错误级别的中间件，捕获整个项目的异常错误，从而防止程序的崩溃
app.use((err, req, res, next) => {
	// 在服务器打印错误消息
    console.log('发生了错误！' + err.message)
    // 向客户端响应错误相关的内容
    res.send('Error：' + err.message)
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
    console.log('Express server running at http://127.0.0.1')
})
```



#### Express 内置的中间件

- 自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验：
  1.  express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）
  2. express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
  3. express.urlencoded 解析 URL-encoded 格式（键值对）的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

```javascript
// 配置解析 application/json 格式数据的内置中间件
app.use(express.json());
// 配置解析 application/x-www-form-urlencoded 格式数据的内置中间件
app.use(express.urlencoded({ extended: fasle }))
```

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置
// 通过 express.json() 这个中间件，解析表单中的 JSON 格式的数据
app.use(express.json())
// 通过 express.urlencoded() 这个中间件，来解析 表单中的 url-encoded 格式的数据
app.use(express.urlencoded({ extended: false }))

app.post('/user', (req, res) => {
  // 在服务器，可以使用 req.body 这个属性，来接收客户端发送过来的请求体数据
  // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认等于 undefined
  console.log(req.body)
  res.send('ok')
})

app.post('/book', (req, res) => {
  // 在服务器端，可以通过 req.body 来获取 JSON 格式的表单数据和 url-encoded 格式的数据
  console.log(req.body)
  res.send('ok')
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})

```

![image-20220404160101507](http://zjp.hxkj.live/MDImage/Nodejs/POST%e5%8f%91%e9%80%81json_2022-04-04_16-01-14.png)

![image-20220404160235906](http://zjp.hxkj.live/MDImage/Nodejs/POST%e5%8f%91%e9%80%81json_2022-04-04_16-02-38.png)

![image-20220404160808555](http://zjp.hxkj.live/MDImage/Nodejs/POST%e5%8f%91%e9%80%81urlencoded_2022-04-04_16-08-45.png)

![image-20220404160911490](http://zjp.hxkj.live/MDImage/Nodejs/POST%e5%8f%91%e9%80%81urlencoded_2022-04-04_16-09-13.png)



#### 第三方的中间件

- 非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率。
- 例如：在 express@4.16.0 之前的版本中，经常使用 body-parser 这个第三方中间件，来解析请求体数据。使用步骤如下：
  1. 运行 npm install body-parser 安装中间件
  2. 使用 require 导入中间件
  3. 调用 app.use() 注册并使用中间件
- 注意：Express 内置的 express.urlencoded 中间件，就是基于 body-parser 这个第三方中间件进一步封装出来的。

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 1. 导入解析表单数据的中间件 body-parser
const parser = require('body-parser')
// 2. 使用 app.use() 注册中间件
app.use(parser.urlencoded({ extended: false }))
// app.use(express.urlencoded({ extended: false }))

app.post('/user', (req, res) => {
  // 如果没有配置任何解析表单数据的中间件，则 req.body 默认等于 undefined
  console.log(req.body)
  res.send('ok')
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```



### 自定义中间件

- 自己手动模拟一个类似于 express.urlencoded 这样的中间件，来解析 POST 提交到服务器的表单数据。
- 步骤
  1. 定义中间件
  2. 监听 req 的 data 事件
  3. 监听 req 的 end 事件
  4. 使用 querystring 模块解析请求体数据
  5. 将解析出来的数据对象挂载为 req.body
  6. 将自定义中间件封装为模块

#### 定义中间件

- 使用 app.use() 来定义全局生效的中间件，代码如下

```javascript
app.use((req, res, next) => {
    // 中间件的业务逻辑
})
```



#### 监听 req 的 data 事件

- 在中间件中，需要监听 req 对象的 data 事件，来获取客户端发送到服务器的数据。
- 如果数据量比较大，无法一次性发送完毕，则客户端会把数据切割后，分批发送到服务器。所以 data 事件可能会触发多次，每一次触发 data 事件时，获取到数据只是完整数据的一部分，需要手动对接收到的数据进行拼接。

```javascript
// 定义变量，用来存储客户端发送过来的请求数据
let str = '';
// 监听 req 对象的 data 事件 (客户端发送过来的新的请求体数据)
req.on('data', (chunk) => {
    // 拼接请求体数据，隐式转换为字符串
    str += chunk;
})
```



#### 监听 req 的 end 事件

- 当请求体数据接收完毕之后，会自动触发 req 的 end 事件。
- 因此，我们可以在 req 的 end 事件中，拿到并处理完整的请求体数据。示例代码如下：

```javascript
// 监听 req 事件的 end 事件（请求体发送完毕后自动触发）
req.on('end', () => {
    // 在 str 中存放的是完整的请求体数据
    console.log(str)
    // TODO: 把字符串格式的请求体数据，解析成对象格式
  })
```



#### 使用 querystring 模块解析请求体数据

- Node.js 内置了一个 querystring 模块，专门用来处理查询字符串。通过这个模块提供的 parse() 函数，可以轻松把查询字符串，解析成对象的格式。示例代码如下：

```javascript
// 导入处理 querystring 的 Node.js 内置模块
const qs = require('querystring');

// 调用 qs.parse() 方法，把查询字符解析为对象
const body = qs.parse(str);
```



#### 将解析出来的数据对象挂载为 req.body

- 上游的中间件和下游的中间件及路由之间，**共享同一份 req 和 res**。因此，我们可以将解析出来的数据，挂载为 req 的自定义属性，命名为 req.body，供下游使用。示例代码如下：

```javascript
req.on('end', () => {
    // 调用 qs.parse() 方法，把查询字符串解析为对象
    const body = qs.parse(str);
    // 将解析出来的请求对象，挂载为 req.body 属性
    req.body = body;
    // 调用 next() 函数，执行后续的业务逻辑
    next();
})
```



#### 将自定义中间件封装为模块

- 为了优化代码的结构，我们可以把自定义的中间件函数，封装为独立的模块，示例代码如下：

```javascript
// custom-body-parser.js 模块中的代码
const qs = require('querystring');
function bodyParser(req, res, next){ /* 省略其他代码 */ }
// 向外导出解析请求体数据的中间件函数
module.exports = bodyParser;
```



```javascript
// 主程序中的代码
// 导入自定义的中间件模块
const myBodyParser = require('custom-body-parser');
// 注册自定义的中间件模块
app.use(myBodyParser);
```



## 接口

- 步骤
  1. 创建基本的服务器
  2. 创建 API 路由模块
  3. 编写 GET 接口
  4. 编写 POST 接口



### 创建基本的服务器

```javascript
// 主程序 app.js
// 导入 express 模块
const express = require('express');
// 创建 express 的服务器实例
const app = express();


// write your code here...

// 调用 app.listen 方法，指定接口号并启动 web 服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1')
});
```



### 创建 API 路由模块

```javascript
// 路由模块 apiRouter.js
// 导入 express 模块
const express = require('express');
// 创建 express 路由实例
const router = express.Router();

// bind your couter here...
```



```javascript
// 主程序 app.js
const apiRouter = require('./apiRouter.js');
app.use('/api', apiRouter);
```



### 编写 GET 接口

```javascript
// 路由模块 apiRouter.js
// 在这里挂载对应的路由
router.get('/get', (req, res) => {
    // 通过 req.query 获取客户端通过查询字符串，发送到服务器的数据
    const query = req.query
    // 调用 res.send() 方法，向客户端响应处理的结果
    res.send({
        status: 0, // 0 表示处理成功，1 表示处理失败
        msg: 'GET 请求成功！', // 状态的描述
        data: query, // 需要响应给客户端的数据
    })
})
```



### 编写 POST 接口

- 注意：如果要获取 URL-encoded 格式的请求体数据，必须配置中间件 app.use(express.urlencoded({ extended: false }))

```javascript
// 路由模块 apiRouter.js
// 定义 POST 接口
router.post('/post', (req, res) => {
    // 通过 req.body 获取请求体中包含的 url-encoded 格式的数据
    const body = req.body
    // 调用 res.send() 方法，向客户端响应结果
    res.send({
        status: 0,
        msg: 'POST 请求成功！',
        data: body,
    })
})
```



```javascript
// 主程序 app.js
// 配置解析表单数据的中间件
app.use(express.urlencoded({ extended: false }));
```



### 接口的跨域问题

- 刚才编写的 GET 和 POST接口，存在一个很严重的问题：不支持跨域请求。
- 解决接口跨域问题的方案主要有两种：
  1. CORS（主流的解决方案，推荐使用）
  2. JSONP（有缺陷的解决方案：只支持 GET 请求）



#### 使用 CORS 中间件解决跨域问题

- CORS 是 Express 的一个第三方中间件。通过安装和配置 CORS 中间件，可以很方便地解决跨域问题。
- 步骤
  1. 运行 npm install cors 安装中间件
  2. 使用 const cors = require('cors') 导入中间件
  3. **在路由之前调用** app.use(cors()) 配置中间件



```shell
# 安装 CORS
npm i cors
```



```javascript
// 主程序 app.js
const cors = require('cors');
// 一定要在路由之前，配置 cors 这个中间件，从而解决接口跨域的问题
app.use(cors());
```



#### 什么是 CORS

- CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，**这些** **HTTP** **响应头决定浏览器是否阻止前端** **JS** **代码跨域获取资源**。
- 浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制。

![image-20220405023836446](http://zjp.hxkj.live/MDImage/Nodejs/%e4%bb%80%e4%b9%88%e6%98%afcors_2022-04-05_02-38-49.png)

- 注意：
  - CORS 主要在服务器端进行配置。客户端浏览器**无须做任何额外的配置**，即可请求开启了 CORS 的接口。
  - CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。



#### CORS 响应头部 - Access-Control-Allow-Origin 

- 响应头部中可以携带一个 Access-Control-Allow-Origin 字段，其语法如下:

```javascript
Access-Control-Allow-Origin: <origin> | *
```

- 其中，origin 参数的值指定了允许访问该资源的外域 URL。
- 例如，下面的字段值将**只允许**来自 http://itcast.cn 的请求：

```javascript
res.setHeader('Access-Control-Allow-Origin', 'http://itcast.cn');
```

- 如果指定了 Access-Control-Allow-Origin 字段的值为通配符 *****，表示允许来自任何域的请求，示例代码如下：

```javascript
res.setHeader('Access-Control-Allow-Origin', '*');
```



#### CORS 响应头部 - Access-Control-Allow-Headers

- 默认情况下，CORS 仅支持客户端向服务器发送如下的 9 个请求头：
- Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）
- 如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

```javascript
// 允许客户端额外向服务器发送 Content-Type 请求头和 X-Custom-Header 请求头
// 注意：多个请求头之间使用英文的逗号进行分隔
res.setHeader('Access-Control-Allow-Headers', 'Content-Type', 'X-Custom-Header');
```



#### CORS 响应头部 - Access-Control-Allow-Methods

- 默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。
- 如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来指明实际请求所允许使用的 HTTP 方法。

```javascript
// 只允许 POST、GET、DELETE、HEAD 请求方式
res.setHeader('Access-Control-Allow-Methods', 'POST, GET, DELETE, HEAD');
// 允许所有的 HTTP 请求方法
res.setHeader('Access-Control-Allow-Methods', '*');
```



#### CORS 请求的分类

- 客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类，分别是：
  1. 简单请求
  2. 预检请求



##### 简单请求

- 同时满足以下两大条件的请求，就属于简单请求：
  1. 请求方式：GET、POST、HEAD 三者之一
  2. HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain）



##### 预检请求

- 只要符合以下任何一个条件的请求，都需要进行预检请求：
  1. 请求方式为 GET、POST、HEAD 之外的请求 Method 类型
  2. 请求头中包含自定义头部字段
  3. 向服务器发送了 application/json 格式的数据
- 在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。



##### 简单请求和预检请求的区别

- **简单请求的特点**：客户端与服务器之间只会发生一次请求
- **预检请求的特点**：客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求。



#### JSONP

- 概念：浏览器端通过 < script > 标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。
- 特点：
  1. JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象。
  2. JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求。



#### 创建 JSONP 接口的注意事项

- 如果项目中已经配置了 CORS 跨域资源共享，为了**防止冲突**，必须在配置 CORS 中间件之前声明 JSONP 的接口。否则 JSONP 接口会被处理成开启了 CORS 的接口。示例代码如下：

```javascript
// 优先创建 JSONP 接口，这个接口不会被处理成 CORS 接口
app.get('/api/jsonp', (req, res) => { });

// 再配置 CORS 中间件，后续的所有接口，都会被处理成 CORS 接口
app.use(cors());

// 这是一个开启了 CORS 的接口
app.get('/api/get', (req, res) => { });
```



#### 实现 JSONP 接口的步骤

1. 获取客户端发送过来的回调函数的名字
2. 得到要通过 JSONP 形式发送给客户端的数据
3. 根据前两步得到的数据，拼接出一个函数调用的字符串
4. 把上一步拼接得到的字符串，响应给客户端的 < script > 标签进行解析执行

```javascript
// 必须在配置 cors 中间件之前，配置 JSONP 的接口
app.get('/api/jsonp', (req, res) => {
    // TODO: 定义 JSONP 接口具体的实现过程
    // 1. 得到函数的名称
    const funcName = req.query.callback
    // 2. 定义要发送到客户端的数据对象
    const data = { name: 'zs', age: 22 }
    // 3. 拼接出一个函数调用的字符串
    const scriptStr = `${funcName}(${JSON.stringify(data)})`
    // 4. 把拼接的字符串，响应给客户端
    res.send(scriptStr)
})
```



#### 在网页中使用 jQuery 发起 JSONP 请求

- 调用 $.ajax() 函数，提供 JSONP 的配置选项，从而发起 JSONP 请求，示例代码如下：

```javascript
// 为 JSONP 按钮绑定点击事件处理函数
$('#btnJSONP').on('click', function () {
    $.ajax({
        type: 'GET',
        url: 'http://127.0.0.1/api/jsonp',
        dataType: 'jsonp',
        success: function (res) {
            console.log(res)
        },
    })
})
```



## 数据库

- 数据库（database）是用来组织、存储和管理数据的仓库。
- 当今世界是一个充满着数据的互联网世界，充斥着大量的数据。数据的来源有很多，比如出行记录、消费记录、浏览的网页、发送的消息等等。除了文本类型的数据，图像、音乐、声音都是数据。
- 为了方便管理互联网世界中的数据，就有了数据库管理系统的概念（简称：数据库）。用户可以对数据库中的数据进行新增、查询、更新、删除等操作。



### 常见的数据库和分类

- 市面上的数据库有很多种，最常见的数据库有如下几个：
  - MySQL 数据库（目前使用最广泛、流行度最高的开源免费数据库；Community + Enterprise）
  - Oracle 数据库（收费）
  - SQL Server 数据库（收费）
  - Mongodb 数据库（Community + Enterprise）
- 其中，MySQL、Oracle、SQL Server 属于**传统型数据库**（又叫做：关系型数据库 或 SQL 数据库），这三者的设计理念相同，用法比较类似。
- 而 Mongodb 属于**新型数据库**（又叫做：非关系型数据库 或 NoSQL 数据库），它在一定程度上弥补了传统型数据库的缺陷。



### 传统型数据库的数据组织结构

- 传统型数据库的数据组织结构，与 Excel 中数据的组织结构比较类似。
- 因此，我们可以对比着 Excel 来了解和学习传统型数据库的数据组织结构。



#### Excel 的数据组织结构

- 每个 Excel 中，数据的组织结构分别为工作簿、工作表、数据行、列这 4 大部分组成。

![image-20220405184617553](http://zjp.hxkj.live/MDImage/Nodejs/Excel%e7%9a%84%e6%95%b0%e6%8d%ae%e7%bb%84%e7%bb%87%e7%bb%93%e6%9e%84_2022-04-05_18-46-35.png)



#### 传统型数据库的数据组织结构

- 在传统型数据库中，数据的组织结构分为数据库(database)、数据表(table)、数据行(row)、字段(field)这 4 大部分组成。

![image-20220405185135262](http://zjp.hxkj.live/MDImage/Nodejs/%e4%bc%a0%e7%bb%9f%e5%9e%8b%e6%95%b0%e6%8d%ae%e5%ba%93%e7%9a%84%e6%95%b0%e6%8d%ae%e7%bb%84%e7%bb%87%e7%bb%93%e6%9e%84_2022-04-05_18-51-46.png)



#### 实际开发中库、表、行、字段的关系

- 在实际项目开发中，一般情况下，每个项目都对应独立的数据库。
- 不同的数据，要存储到数据库的不同表中，例如：用户数据存储到 users 表中，图书数据存储到 books 表中。
- 每个表中具体存储哪些信息，由字段来决定，例如：我们可以为 users 表设计 id、username、password 这 3 个字段。
- 表中的行，代表每一条具体的数据。



### 安装

- 对于开发人员来说，只需要安装 MySQL Server 和 Navicat Premium 这两个软件，就能满足开发的需要了。

- [MySQL Server](https://downloads.mysql.com/archives/community/)：专门用来提供数据存储和服务的软件。（看 JavaWeb.md 文档）

- Navicat Premium：可视化的 MySQL 管理工具，通过它，可以方便的操作存储在 MySQL Server 中的数据。

  - 网盘下载地址：

    链接: https://pan.baidu.com/s/11PH7oGOaegG00e8x-bx_aQ

    提取码: 3y6d

    操作教程：

    https://www.jb51.net/article/199525.htm




### 创建数据库

- 数据库名不要有中文以及空格，空格可以用下划线代替

```sql
-- 创建数据库
-- 创建一个名为 my_db_01 的数据库
CREATE DATABASE `my_db_01`;
```



### 创建数据表

1. 右键数据库，新建表

![image-20220405194527995](http://zjp.hxkj.live/MDImage/Nodejs/%e5%88%9b%e5%bb%ba%e6%95%b0%e6%8d%ae%e8%a1%a8_2022-04-05_19-45-42.png)

2. 添加表注释，描述表的用处

![image-20220405194655529](http://zjp.hxkj.live/MDImage/Nodejs/%e6%95%b0%e6%8d%ae%e8%a1%a8%e6%b7%bb%e5%8a%a0%e6%b3%a8%e9%87%8a_2022-04-05_19-47-02.png)

3. 创建字段，每个表必须要有 id 字段，设置好，字段名，字段数据类型，字段注释

   - DataType 数据类型：
     1. int 整数
     2. varchar(len) 字符串
     3. tinyint(1) 布尔值

   ![image-20220405195256920](http://zjp.hxkj.live/MDImage/Nodejs/%e6%95%b0%e6%8d%ae%e8%a1%a8%e5%88%9b%e5%bb%ba%e5%ad%97%e6%ae%b5_2022-04-05_19-53-05.png)

4. 设置字段的特殊标识，其中 id 需要设置键，不是 null，自动增长，其他字段名根据需要进行设置
   1. PK (Primary Key)：主键、唯一标识
   2. NN (Not Null)：值不允许为空
   3. UQ (Unique)：值唯一
   4. AI (Auto Increment)：值自动增长

![image-20220405195826098](http://zjp.hxkj.live/MDImage/Nodejs/%e6%95%b0%e6%8d%ae%e8%a1%a8%e8%ae%be%e7%bd%ae%e5%ad%97%e6%ae%b5%e7%9a%84%e7%89%b9%e6%ae%8a%e6%a0%87%e8%af%86_2022-04-05_19-58-34.png)

![image-20220405200027874](http://zjp.hxkj.live/MDImage/Nodejs/%e6%95%b0%e6%8d%ae%e8%a1%a8%e8%ae%be%e7%bd%ae%e5%ad%97%e6%ae%b5%e7%9a%84%e7%89%b9%e6%ae%8a%e6%a0%87%e8%af%86_2022-04-05_20-00-30.png)

5. 保存，设置表名

![image-20220405200216679](http://zjp.hxkj.live/MDImage/Nodejs/%e6%95%b0%e6%8d%ae%e8%a1%a8%e7%9a%84%e4%bf%9d%e5%ad%98_2022-04-05_20-02-25.png)



### 填写数据表

1. 根据数据表表头，填写对应数据内容，其中自增字段和有默认值的字段不需要填写，（id 和 status）

![image-20220405200533058](http://zjp.hxkj.live/MDImage/Nodejs/%e6%95%b0%e6%8d%ae%e8%a1%a8%e7%9a%84%e6%95%b0%e6%8d%ae%e5%a1%ab%e5%86%99_2022-04-05_20-05-48.png)



## SQL

- SQL（英文全称：Structured Query Language）是结构化查询语言，专门用来访问和处理数据库的编程语言。能够让我们**以编程的形式**，**操作数据库里面的数据**。
- 关键点
  - SQL 是一门数据库编程语言
  - 使用 SQL 语言编写出来的代码，叫做 SQL 语句
  - SQL 语言只能在关系型数据库中使用（例如 MySQL、Oracle、SQL Server）。非关系型数据库（例如 Mongodb）不支持 SQL 语言



### 功能

1. 从数据库中查询数据
2. 向数据库中插入新的数据
3. 更新数据库中的数据
4. 从数据库删除数据
5. 可以创建新数据库
6. 可在数据库中创建新表
7. 可在数据库中创建存储过程、视图



### 查询数据 

- SELECT 语句用于从表中查询数据。执行的结果被存储在一个结果表中（称为结果集）。语法格式如下：
- 注意：SQL 语句中的关键字对大小写不敏感。SELECT 等效于 select,FROM 等效于 from

```sql
-- 这是注释
-- 从 FROM 指定的表中，查询出所有的数据。 * 表示所有列
SELECT * FROM 表名称;
-- 示例
SELECT * FROM `users`;


-- 从 FROM 指定的表中，查询出指定 列名称(字段) 的数据。
SELECT 列名称 FROM 表名称;
-- 示例
SELECT `id` FROM `users`;
-- 多个列名用英文逗号分隔
SELECT `id`,`username` FROM `users`;
```



### 插入数据

- INSERT INTO 语句用于向数据表中插入新的数据行，语法格式如下：

```sql
-- 语句解读：向指定的表中，插入如下几列数据，列的值通过 values 指定
-- 注意：列和值要一一对应，多个列和多个值之间使用英文的逗号分隔
INSERT INTO table_name(列1， 列2， …) VALUES(值1, 值2, …);
-- 示例
INSERT INTO users(`username`,`password`) VALUES ('tony stark','098123');
```



### 修改数据

- Update 语句用于修改表中的数据。语法格式如下：
- **注意：必须加 WHERE ，否则整张表对应列值都会统一修改**

```sql
-- 语句解读:
-- 1. 用 UPDATE 指定要更新哪个表中的数据
-- 2. 用 SET 指定列对应的新值
-- 3. 用 WHERE 指定更新的条件
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值;
-- 示例
UPDATE `users` SET `password` = "8888" WHERE `id` = 2;
-- 更新多个值
UPDATE `users` SET `password` = "8888", `status` = 1 WHERE `id` = 1;
```



### 删除数据

- DELETE 语句用于删除表中的行。语法格式如下：
- **注意：必须加 WHERE，否则会删除整个表**

```sql
-- 语句解读：
-- 从指定的表中，根据 WHERE 条件，删除对应的数据行
DELETE FROM 表名称 WHERE 列名称 = 值;
-- 示例
DELETE FROM `users` WHERE `id` = 3;
```



### WHERE 子句

- WHERE 子句用于限定选择的标准。在 SELECT、UPDATE、DELETE 语句中，皆可使用 WHERE 子句来限定选择的标准。

```sql
-- 查询语句中的 WHERE 条件
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值;
-- 更新语句中的 WHERE 条件
UPDATE 表名称 SET 列 = 新值 WHERE 列 运算符 值;
-- 删除语句中的 WHERE 条件
DELETE FROM 表名称 WHERE 列 运算符 值;
```

- 下面的运算符可在 WHERE 子句中使用，用来限定选择的标准：
- 注意：在某些版本的 SQL 中，操作符 <> 可以写为 !=，mysql 可以使用 != 运算符

![image-20220405235859651](http://zjp.hxkj.live/MDImage/Nodejs/WHERE%e4%b8%ad%e7%9a%84%e8%bf%90%e7%ae%97%e7%ac%a6_2022-04-05_23-59-15.png)

#### AND 和 OR 运算符

- AND 和 OR 可在 WHERE 子语句中把两个或多个条件结合起来。
- AND 表示必须同时满足多个条件，相当于 JavaScript 中的 && 运算符，例如 if (a !== 10 && a !== 20)
- OR 表示只要满足任意一个条件即可，相当于 JavaScript 中的 || 运算符，例如 if(a !== 10 || a !== 20)



#### AND 运算符

```sql
-- 示例
SELECT * FROM `users` WHERE `status` = 0 AND id < 3;
```



#### OR 运算符

```sql
-- 示例
SELECT * FROM `users` WHERE `status` = 0 OR id < 3;
```



### ORDER BY 子句

- ORDER BY 语句用于根据指定的列对结果集进行排序。
- ORDER BY 语句**默认**按照升序对记录进行排序。
- 如果您希望按照**降序**对记录进行排序，可以使用 **DESC** 关键字。

```sql
-- 升序排序，默认是 ASC 升序排序
SELECT * FROM `users` ORDER BY `id`;
-- 升序排序
SELECT * FROM `users` ORDER BY `id` ASC;
-- 降序排序
SELECT * FROM `users` ORDER BY `id` DESC ;
```



#### 多重排序

- 多个排序规则使用英文逗号分隔。

```sql
-- 对 users 表中的数据，先按照 id 字段进行降序排序，再按照 username 的字母顺序，进行升序排序
SELECT * FROM `users` ORDER BY `id` DESC, username ASC;
```



### COUNT(*) 函数

- COUNT(*) 函数用于返回查询结果的总数据条数，语法格式如下：

```sql
SELECT COUNT(*) FROM 表名称
-- 示例
SELECT COUNT(*) FROM `users` WHERE `status` = 0;
```



### AS 为列设置别名

- 如果希望给查询出来的列名称设置别名，可以使用 AS 关键字，示例如下：

```sql
SELECT COUNT(*) AS `total` FROM `users` WHERE `status` = 0;
```

![image-20220406002920003](http://zjp.hxkj.live/MDImage/Nodejs/AS%e4%b8%ba%e5%88%97%e8%ae%be%e7%bd%ae%e5%88%ab%e5%90%8d_2022-04-06_00-29-23.png)

- 给其他列起别名

```sql
SELECT `id` AS `total` FROM `users`
```



![image-20220406002833685](http://zjp.hxkj.live/MDImage/Nodejs/AS%e4%b8%ba%e5%88%97%e8%ae%be%e7%bd%ae%e5%88%ab%e5%90%8d_2022-04-06_00-28-42.png)



## 项目中操作数据库

- 步骤：
  1. 安装操作 MySQL 数据库的第三方模块（mysql）
  2. 通过 mysql 模块连接到 MySQL 数据库
  3. 通过 mysql 模块执行 SQL 语句

![image-20220406003604157](http://zjp.hxkj.live/MDImage/Nodejs/%e9%a1%b9%e7%9b%ae%e4%b8%ad%e6%93%8d%e4%bd%9c%e6%95%b0%e6%8d%ae%e5%ba%93_2022-04-06_00-36-14.png)

### 安装 mysql 模块

- mysql 模块是托管于 npm 上的第三方模块。它提供了在 Node.js 项目中连接和操作 MySQL 数据库的能力。
- 想要在项目中使用它，需要先运行如下命令，将 mysql 安装为项目的依赖包：

```shell
npm install mysql
```



### 配置 mysql 模块

- 在使用 mysql 模块操作 MySQL 数据库之前，必须先对 mysql 模块进行必要的配置，主要的配置步骤如下：

```javascript
// 1. 导入 mysql 模块
const mysql = require('mysql')
// 2. 建立与 MySQL 数据库的连接关系
const db = mysql.createPool({
  host: '127.0.0.1', // 数据库的 IP 地址
  user: 'root', // 登录数据库的账号
  password: '1234', // 登录数据库的密码
  database: 'my_db_01', // 指定要操作哪个数据库
})
```



### 测试 mysql 模块能否正常工作

- 调用 db.query() 函数，指定要执行的 SQL 语句，通过回调函数拿到执行的结果：

```javascript
// 测试 mysql 模块能否正常工作
db.query('select 1', (err, results) => {
    // mysql 模块工作期间报错了
    if (err) return console.log(err.message);
    // 能够成功的执行 SQL 语句
    // 只要能打印出 [ RowDataPacket { '1': 1 } ] 的结果，就证明数据库连接正常
    console.log(results);
})
```

![image-20220406005220683](http://zjp.hxkj.live/MDImage/Nodejs/%e9%a1%b9%e7%9b%ae%e4%b8%ad%e6%b5%8b%e8%af%95%e6%95%b0%e6%8d%ae%e5%ba%93%e7%9a%84%e8%bf%9e%e6%8e%a5_2022-04-06_00-52-28.png)

### 查询数据

```javascript
// 查询 users 表中的所有数据
const sqlStr = 'SELECT * FROM `users`'
db.query(sqlStr, (err, results) => {
    // 查询数据失败
    if (err) return console.log(err.message);
    // 查询数据成功
    // 注意：如果执行的是 select 查询语句，则执行的结果是数组
    console.log(results);
})
```

![image-20220406005202344](http://zjp.hxkj.live/MDImage/Nodejs/%e9%a1%b9%e7%9b%ae%e4%b8%ad%e6%9f%a5%e8%af%a2%e6%95%b0%e6%8d%ae_2022-04-06_00-52-10.png)

### 插入数据

```javascript
// 向 users 表中，新增一条数据，其中 username 的值为 Spider-Man，password 的值为 pcc123
const user = { username: 'Spider-Man', password: 'pcc123' };
// 定义待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'insert into users(username, password) values (?, ?)';
// 使用数组的形式，依次为 ? 占位符指定具体的值
// 执行 SQL 语句
db.query(sqlStr, [user.username, user.password], (err, results) => {
    // 执行 SQL 语句失败了
    if (err) return console.log(err.message);
    // 成功了
    // 注意：如果执行的是 insert into 插入语句，则 results 是一个对象
    // 可以通过 affectedRows 属性，来判断是否插入数据成功
    if (results.affectedRows === 1) {
        console.log('插入数据成功!');
    }
})
```

- 快捷方式
- 向表中新增数据时，如果数据对象的每个属性和数据表的字段**一一对应**，则可以通过如下方式快速插入数据：

```javascript
// 演示插入数据的便捷方式
const user = { username: 'Spider-Man2', password: 'pcc4321' };
// 定义待执行的 SQL 语句
const sqlStr = 'insert into users set ?';
// 执行 SQL 语句
db.query(sqlStr, user, (err, results) => {
    if (err) return console.log(err.message);
    if (results.affectedRows === 1) {
        console.log('插入数据成功');
    }
})
```



### 更新数据

```javascript
// 演示如何更新用户的信息
const user = { id: 6, username: 'aaa', password: '000' };
// 定义 SQL 语句
const sqlStr = 'update users set username=?, password=? where id=?';
// 执行 SQL 语句
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
    if (err) return console.log(err.message);
    // 注意：执行了 update 语句之后，执行的结果，也是一个对象，可以通过 affectedRows 判断是否更新成功
    if (results.affectedRows === 1) {
        console.log('更新成功');
    }
});
```

- 快捷方式
- 更新表数据时，如果数据对象的每个属性和数据表的字段**一一对应**，则可以通过如下方式快速更新表数据：

```javascript
// 演示更新数据的便捷方式
const user = { id: 6, username: 'aaaa', password: '0000' };
// 定义 SQL 语句
const sqlStr = 'update users set ? where id=?';
// 执行 SQL 语句
db.query(sqlStr, [user, user.id], (err, results) => {
    if (err) return console.log(err.message);
    if (results.affectedRows === 1) {
        console.log('更新数据成功');
    }
});
```



### 删除数据

- 在删除数据时，推荐根据 id 这样的唯一标识，来删除对应的数据。示例如下：

```javascript
// 删除 id 为 5 的用户
const sqlStr = 'delete from users where id=?';
// 调用 db.query() 执行 SQL 语句的时候，为占位符指定具体的值
// 注意：如果 SQL 语句汇总有多个占位符，则必须使用数组为每个占位符指定具体的值
//      如果 SQL 语句中只有一个占位符，则可以省略数组
db.query(sqlStr, 5, (err, results) => {
    if (err) return console.log(err.message);
    // 注意：执行 delete 语句之后，结果也是一个对象，也会包含 affectedRows 属性
    if (results.affectedRows === 1) {
        console.log('删除数据成功');
    }
})
```



### 标记删除

- 使用 DELETE 语句，会把真正的把数据从表中删除掉。为了保险起见，**推荐使用**标记删除的形式，来**模拟删除的动作**。
- 所谓的标记删除，就是在表中设置类似于 **status** 这样的**状态字段**，来**标记**当前这条数据是否被删除。
- 当用户执行了删除的动作时，我们并没有执行 DELETE 语句把数据删除掉，而是执行了 UPDATE 语句，将这条数据对应的 status 字段标记为删除即可。

```javascript
// 标记删除
const sqlStr = 'update users set status=? where id=?'
db.query(sqlStr, [1, 6], (err, results) => {
    if (err) return console.log(err.message);
    if (results.affectedRows === 1) {
        console.log('标记删除成功');
    }
})
```



## 前后端的身份认证

### Web 开发模式

- 目前主流的 Web 开发模式有两种，分别是：
  1. 基于服务端渲染的传统 Web 开发模式
  2. 基于前后端分离的新型 Web 开发模式

#### 服务端渲染的 Web 开发模式

- 服务端渲染的概念：服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不需要使用 Ajax 这样的技术额外请求页面的数据。代码示例如下：

![image-20220406011909279](http://zjp.hxkj.live/MDImage/Nodejs/%e6%9c%8d%e5%8a%a1%e5%99%a8%e6%b8%b2%e6%9f%93%e7%9a%84Web%e5%bc%80%e5%8f%91%e6%a8%a1%e5%9d%97_2022-04-06_01-19-24.png)

- 优点
  1. 前端耗时少。因为服务器端负责动态生成 HTML 内容，浏览器只需要直接渲染页面即可。尤其是移动端，更省电。
  2. 有利于 SEO。因为服务器端响应的是完整的 HTML 页面内容，所以爬虫更容易爬取获得信息，更有利于 SEO。

- 缺点
  1. 占用服务器端资源。即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力。
  2. 不利于前后端分离，开发效率低。使用服务器端渲染，则无法进行分工合作，尤其对于前端复杂度高的项目，不利于项目高效开发。



#### 前后端分离的 Web 开发模式

- 前后端分离的概念：前后端分离的开发模式，依赖于 Ajax 技术的广泛应用。简而言之，前后端分离的 Web 开发模式，就是后端只负责提供 API 接口，前端使用 Ajax 调用接口的开发模式。
- 优点
  1. 开发体验好。前端专注于 UI 页面的开发，后端专注于 api 的开发，且前端有更多的选择性。
  2. 用户体验好。Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。
  3. 减轻了服务器端的渲染压力。因为页面最终是在每个用户的浏览器中生成的。
- 缺点
  1. 不利于 SEO。因为完整的 HTML 页面需要在客户端动态拼接完成，所以爬虫对无法爬取页面的有效信息。（解决方案：利用 Vue、React 等前端框架的 SSR （server side render）技术能够很好的解决 SEO 问题！）



### 如何选择 Web 开发模式

- 不谈业务场景而盲目选择使用何种开发模式都是耍流氓。
- 比如企业级网站，主要功能是展示而没有复杂的交互，并且需要良好的 SEO，则这时我们就需要使用服务器端渲染；
- 而类似后台管理项目，交互性比较强，不需要考虑 SEO，那么就可以使用前后端分离的开发模式。
- 另外，具体使用何种开发模式并不是绝对的，为了**同时兼顾了首页的渲染速度和前后端分离的开发效率**，一些网站采用了首屏服务器端渲染 + 其他页面前后端分离的开发模式。



### 身份认证

- 身份认证（Authentication）又称“身份验证”、“鉴权”，是指通过一定的手段，完成对用户身份的确认。
- 日常生活中的身份认证随处可见，例如：高铁的验票乘车，手机的密码或指纹解锁，支付宝或微信的支付密码等。
- 在 Web 开发中，也涉及到用户身份的认证，例如：各大网站的**手机验证码登录**、**邮箱密码登录**、**二维码登录**等。
- 身份认证的目的，是为了**确认当前所声称为某种身份的用户，确实是所声称的用户**。例如，你去找快递员取快递，你要怎么证明这份快递是你的。
- 在互联网项目开发中，如何对用户的身份进行认证，是一个值得深入探讨的问题。例如，如何才能保证网站不会错误的将 “马云的存款数额” 显示到 “马化腾的账户” 上。



### 不同模式下的身份认证

- 对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案：
  - 服务端渲染推荐使用 Session 认证机制
  - 前后端分离推荐使用 JWT 认证机制



### Session 认证机制

#### HTTP 协议的无状态性

- 了解 HTTP 协议的无状态性是进一步学习 Session 认证机制的必要前提。

- HTTP 协议的无状态性，指的是客户端的每次 HTTP 请求都是独立的，连续多个请求之间没有直接的关系，服务器不会主动保留每次 HTTP 请求的状态。

![image-20220406013308455](http://zjp.hxkj.live/MDImage/Nodejs/HTTP%e5%8d%8f%e8%ae%ae%e7%9a%84%e6%97%a0%e7%8a%b6%e6%80%81%e6%80%a7_2022-04-06_01-33-17.png)



#### 打破 HTTP 无状态性的限制

- 对于超市来说，为了方便收银员在进行结算时给 VIP 用户打折，超市可以为每个 VIP 用户发放会员卡。
- 注意：现实生活中的会员卡身份认证方式，在 Web 开发中的专业术语叫做 Cookie。

![image-20220406013454303](http://zjp.hxkj.live/MDImage/Nodejs/%e6%89%93%e7%a0%b4HTTP%e5%8d%8f%e8%ae%ae%e7%9a%84%e6%97%a0%e7%8a%b6%e6%80%81%e6%80%a7%e7%9a%84%e9%99%90%e5%88%b6_2022-04-06_01-35-12.png)



#### Cookie

- Cookie 是存储在用户浏览器中的一段不超过 4 KB 的字符串。它由一个名称（Name）、一个值（Value）和其它几个用于控制 Cookie 有效期、安全性、使用范围的可选属性组成。
- 不同域名下的 Cookie 各自独立，每当客户端发起请求时，会自动把当前域名下所有未过期的 Cookie 一同发送到服务器。
- Cookie 的特性
  - 自动发送
  - 域名独立
  - 过期时限
  - 4KB 的限制



#### Cookie 在身份认证中的作用

- 客户端第一次请求服务器的时候，服务器**通过响应头的形式**，向客户端发送一个身份认证的 Cookie，客户端会自动将 Cookie 保存在浏览器中。
- 随后，当客户端浏览器每次请求服务器的时候，浏览器会**自动**将身份认证相关的 Cookie，**通过请求头的形式**发送给服务器，服务器即可验明客户端的身份。

![image-20220406014134935](http://zjp.hxkj.live/MDImage/Nodejs/Cookie%e5%9c%a8%e8%ba%ab%e4%bb%bd%e8%ae%a4%e8%af%81%e4%b8%ad%e7%9a%84%e4%bd%9c%e7%94%a8_2022-04-06_01-41-46.png)



#### Cookie 不具有安全性

- 由于 Cookie 是存储在浏览器中的，而且**浏览器也提供了读写 Cookie 的 API**，因此 **Cookie 很容易被伪造**，不具有安全性。因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送给浏览器。
- **注意：千万不要使用 Cookie 存储重要且隐私的数据**！比如用户的身份信息、密码等。

![image-20220406014708063](http://zjp.hxkj.live/MDImage/Nodejs/Cookie%e4%b8%8d%e5%85%b7%e6%9c%89%e5%ae%89%e5%85%a8%e6%80%a7_2022-04-06_01-47-10.png)

#### 提高身份认证的安全性

- 为了防止客户伪造会员卡，收银员在拿到客户出示的会员卡之后，可以**在收银机上进行刷卡认证**。只有收银机确认存在的会员卡，才能被正常使用。
- 这种“**会员卡 + 刷卡认证**”的设计理念，就是 Session 认证机制的精髓。

![image-20220406014901056](http://zjp.hxkj.live/MDImage/Nodejs/%e6%8f%90%e9%ab%98%e8%ba%ab%e4%bb%bd%e8%ae%a4%e8%af%81%e7%9a%84%e5%ae%89%e5%85%a8%e6%80%a7_2022-04-06_01-49-08.png)



#### Session 的工作原理

![image-20220406015043243](http://zjp.hxkj.live/MDImage/Nodejs/Session%e7%9a%84%e5%b7%a5%e4%bd%9c%e5%8e%9f%e7%90%86_2022-04-06_01-50-52.png)



### 安装 express-session

- 在 Express 项目中，只需要安装 express-session 中间件，即可在项目中使用 Session 认证。

```shell
npm i express-session
```

### 配置 express-session

- express-session 中间件安装成功后，需要通过 app.use() 来注册 session 中间件，示例代码如下：

```javascript
// 导入 session 中间件
const session = require('express-session');

// 配置 session 中间件
app.use(session({
    secret: 'keyboard cat',  // secret 属性值可以为任意字符串，用于加密的 key
    resave: false,  // 固定写法
    saveUninitialized: true  // 固定写法
}))
```



### 向 session 中存数据

- 当 express-session 中间件配置成功后，即可通过 **req.session** 来访问和使用 session 对象，从而存储用户的关键信息：

```javascript
// 登陆的 API 接口
app.post('/api/login', (req, res) => {
    // 判断用户提交的登陆信息是否正确
    if (req.body.username !== 'admin' || req.body.password !== '000000') {
        return res.send({ status: 1, msg: '登陆失败' });
    }

    // 注意：只有成功配置了 express-session 这个中间件之后，才能通过 req 点出来 session 这个属性
    req.session.user = req.body;  // 将用户的信息，存储到 session 中
    req.session.islogin = true;  // 将用户的登陆状态，存储到 session 中

    res.send({ status: 0, msg: '登陆成功' });
});
```



### 从 session 中取数据

- 可以直接从 req.session 对象上获取之前存储的数据，示例代码如下：

```javascript
// 获取用户姓名的接口
app.get('/api/username', (req, res) => {
    // 判断用户是否登陆
    if (!req.session.islogin) {
        return res.send({ status: 1, msg: 'fail' });
    }
    res.send({ status: 0, msg: 'success', username: req.session.user.username });
});
```



### 清空 session

- 调用 req.session.destroy() 函数，即可清空服务器保存的 session 信息。

```javascript
// 退出登陆的接口
app.post('/api/logout', (req, res) => {
    // 清空当前客户端对应的 session 信息
    req.session.destroy();
    res.send({
        status: 0,
        mes: '退出登陆成功'
    })
});
```



### JWT 认证机制

- Session 认证机制需要配合 Cookie 才能实现。由于 Cookie 默认不支持跨域访问，所以，当涉及到前端跨域请求后端接口的时候，**需要做很多额外的配置**，才能实现跨域 Session 认证。
- 注意：
  - 当前端请求后端接口**不存在跨域问题**的时候，**推荐使用** **Session** 身份认证机制。
  - 当前端需要跨域请求后端接口的时候，不推荐使用 Session 身份认证机制，推荐使用 JWT 认证机制。



#### JWT

- JWT（英文全称：JSON Web Token）是目前**最流行**的**跨域认证解决方案**。



#### JWT 工作原理

- 用户的信息通过 Token 字符串的形式，保存在客户端浏览器中。服务器通过还原 Token 字符串的形式来认证用户的身份。

![image-20220406141652441](http://zjp.hxkj.live/MDImage/Nodejs/JWT%e5%b7%a5%e4%bd%9c%e5%8e%9f%e7%90%86_2022-04-06_14-17-04.png)

#### JWT 组成部分

- JWT 通常由三部分组成，分别是 Header（头部）、Payload（有效荷载）、Signature（签名）。
- 三者之间使用英文的“.”分隔，格式如下：
- Payload 部分才是真正的用户信息，它是用户信息经过加密之后生成的字符串。
- Header 和 Signature 是安全性相关的部分，只是为了保证 Token 的安全性。

![image-20220406142152460](http://zjp.hxkj.live/MDImage/Nodejs/JWT%e7%bb%84%e6%88%90%e9%83%a8%e5%88%86_2022-04-06_14-21-57.png)



![image-20220406142246898](http://zjp.hxkj.live/MDImage/Nodejs/JWT%e7%bb%84%e6%88%90%e9%83%a8%e5%88%86_2022-04-06_14-22-49.png)



#### JWT 的使用方式

- 客户端收到服务器返回的 JWT 之后，通常会将它储存在 localStorage 或 sessionStorage 中。
- 此后，客户端每次与服务器通信，都要带上这个 JWT 的字符串，从而进行身份认证。推荐的做法是**把** **JWT** **放在** **HTTP** **请求头的** **Authorization** **字段中**，格式如下：

![image-20220406142738286](http://zjp.hxkj.live/MDImage/Nodejs/JWT%e7%9a%84%e4%bd%bf%e7%94%a8%e6%96%b9%e5%bc%8f_2022-04-06_14-27-44.png)



### 安装 JWT 相关包

```shell
npm install jsonwebtoken express-jwt
```

- jsonwebtoken 用于生成 JWT 字符串
- express-jwt 用于将 JWT 字符串解析还原成 JSON 对象



### 导入 JWT 相关包

```javascript
// 导入用于生成 JWT 字符串的包
const jwt = require('jsonwebtoken');
// 导入用于将客户端发送过来的 JWT 字符串，解析还原成 JSON 对象的包
const expressJWT = require('express-jwt');
```



### 定义 secret 密钥

- 为了保证 JWT 字符串的安全性，防止 JWT 字符串在网络传输过程中被别人破解，我们需要专门定义一个用于**加密**和**解密**的 secret 密钥：
  - 当生成 JWT 字符串的时候，需要使用 secret 密钥对用户的信息进行加密，最终得到加密好的 JWT 字符串
  - 当把 JWT 字符串解析还原成 JSON 对象的时候，需要使用 secret 密钥进行解密

```javascript
// secret 密钥的本质：就是一个字符串
const secretKey = 'itheima No1 ^_^';
```



### 在登陆成功后生成 JWT 字符串

- 调用 **jsonwebtoken** 包提供的 **sign()** 方法，将用户的信息加密成 JWT 字符串，响应给客户端：

```javascript
// 登录成功
// TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
// 参数1：用户的信息对象
// 参数2：加密的秘钥
// 参数3：配置对象，可以配置当前 token 的有效期,30s 过期
// 记住：千万不要把密码加密到 token 字符中
const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' })
res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
})
```

![image-20220407101454686](http://zjp.hxkj.live/MDImage/Nodejs/%e7%99%bb%e9%99%86%e6%88%90%e5%90%8e%e7%94%9f%e6%88%90JWT%e5%ad%97%e7%ac%a6%e4%b8%b2_2022-04-07_10-15-09.png)

### 将 JWT 字符串还原成 JSON 对象

- 客户端每次在访问那些有权限接口的时候，都需要主动通过**请求头中的 Authorization 字段**，将 Token 字符串发送到服务器进行身份认证。
- 此时，服务器可以通过 express-jwt 这个中间件，自动将客户端发送过来的 Token 解析还原成 JSON 对象：
- 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上

```javascript
// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
// .unless({ path: [/^\/api\//] }) 用来指定哪些接口不需要访问权限
app.use(expressJWT({ secret: secretKey, algorithms: ['HS256'] }).unless({ path: [/^\/api\//] }))
```



### 使用 req.user 获取用户信息

- 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
- req.user 对象的内容取决于自定义的用户信息对象 jwt.sign({ username: userinfo.username } 中的内容。

- 当 express-jwt 这个中间件配置成功之后，即可在那些有权限的接口中，使用 req.user 对象，来访问从 JWT 字符串中解析出来的用户信息了，示例代码如下：

```javascript
// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
    // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
    console.log(req.user)
    res.send({
        status: 200,
        message: '获取用户信息成功！',
        data: req.user, // 要发送给客户端的用户信息
    })
})
```

![image-20220407102153082](http://zjp.hxkj.live/MDImage/Nodejs/%e4%bd%bf%e7%94%a8req.user%e8%8e%b7%e5%8f%96%e7%94%a8%e6%88%b7%e4%bf%a1%e6%81%af_2022-04-07_10-22-06.png)



### 捕获解析 JWT 失败后产生的错误

- 当使用 express-jwt 解析 Token 字符串时，如果客户端发送过来的 Token 字符串**过期**或**不合法**，会产生一个**解析失败**的错误，影响项目的正常运行。我们可以通过 **Express** **的错误中间件**，捕获这个错误并进行相关的处理，示例代码如下：

```javascript
// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
    // 这次错误是由 token 解析失败导致的
    if (err.name === 'UnauthorizedError') {
        return res.send({
            status: 401,
            message: '无效的token',
        })
    }
    res.send({
        status: 500,
        message: '未知的错误',
    })
})
```

