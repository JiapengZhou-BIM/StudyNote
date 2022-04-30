# Vue

## ES6 模块化与异步编程高级用法

### ES6 模块化

- node.js 遵循了 CommonJS 的模块化规范。其中：
  - 导入其它模块使用 require() 方法
  - 模块对外共享成员使用 module.exports 对象
- 模块化的好处：
  - 大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己。



#### 前端模块化规范的分类

- 在 ES6 模块化规范诞生之前，JavaScript 社区已经尝试并提出了 AMD、CMD、CommonJS 等模块化规范。
- 但是，这些由社区提出的模块化标准，还是存在一定的差异性与局限性、并不是浏览器与服务器通用的模块化标准，例如：
  - AMD 和 CMD 适用于浏览器端的 Javascript 模块化
  - CommonJS 适用于服务器端的 Javascript 模块化
- 太多的模块化规范给开发者增加了学习的难度与开发的成本。因此，大一统的ES6 模块化规范诞生了！
- ES6 模块化规范是浏览器端与服务器端通用的模块化开发规范。它的出现极大的降低了前端开发者的模块化学习成本，开发者不需再额外学习 AMD、CMD 或 CommonJS 等模块化规范。
- ES6 模块化规范中定义：
  - 每个 js 文件都是一个独立的模块
  - 导入其它模块成员使用 import 关键字
  - 向外共享模块成员使用 export 关键字



#### 在 node.js 中体验 ES6 模块化

- node.js 中默认仅支持 CommonJS 模块化规范，若想基于 node.js 体验与学习 ES6 的模块化语法，可以按照如下两个步骤进行配置：
  - 确保安装了 v14.15.1 或更高版本的 node.js

```bash
node -v
```

- 在 package.json 的根节点中添加 "type": "module" 节点
  - 创建 package.json 文件
  - 在头部区域添加  `"type": "module",`

```bash
npm init -y
```

![image-20220414064639582](http://zjp.hxkj.live/MDImage/Vue/nodejs%e4%b8%ad%e4%bd%93%e9%aa%8cES6%e6%a8%a1%e5%9d%97%e5%8c%96_2022-04-14_06-46-54.png)



#### ES6 模块化的基本语法

- ES6 的模块化主要包含如下 3 种用法：
  - 默认导出与默认导入
  - 按需导出与按需导入
  - 直接导入并执行模块中的代码



##### 默认导出

- 默认导出的语法： export default 默认导出的成员

```javascript
let n1 = 10  // 定义模块私有成员 n1
let n2 = 20  // 定义模块私有成员 n2（外界访问不到 n2，因为它没有被共享出去）
function show() {}  // 定义模块私有方法 show

// 使用 export default 默认导出语法，向外共享 n1 和 show 两个成员
export default {
  n1,
  show
}
```

##### 默认导出注意事项

- 每个模块中，只允许使用唯一的一次 export default，否则会报错！

![image-20220414065646016](http://zjp.hxkj.live/MDImage/Vue/%e6%a8%a1%e5%9d%97%e5%a4%9a%e6%ac%a1%e5%af%bc%e5%87%ba%e6%8a%a5%e9%94%99_2022-04-14_06-56-55.png)







##### 默认导入

- 默认导入的语法： import 接收名称 from '模块标识符'

```javascript
// 从 01_m1.js 模块中导入 export default 向外共享的成员
// 并使用 m1 成员进行接收
import m1 from './01_m1.js'

// 打印输出的结果为：
// { n1: 10, show: [Function: show] }
console.log(m1)
```



##### 默认导入注意事项

- 默认导入时的接收名称可以任意名称，只要是合法的成员名称即可：

![image-20220414070029906](http://zjp.hxkj.live/MDImage/Vue/%e9%bb%98%e8%ae%a4%e5%af%bc%e5%85%a5%e6%8a%a5%e9%94%99_2022-04-14_07-00-40.png)



##### 按需导出

- 按需导出的语法： export 按需导出的成员

```javascript
// 当前模块为 03_m2.js

// 向外按需导出变量 s1
export let s1 = 'aaa'
// 向外按需导出变量 s2
export let s2 = 'ccc'
// 向外按需导出变量 say
export function say() {}

// 每个模块中可以使用多次按需导出，默认导出只能一次。
export default {
  a: 20
}
```





##### 按需导入

- 按需导入的语法： import { s1 } from '模块标识符'

```javascript
// 导入模块成员
// 按需导入的成员名称必须和按需导出的名称保持一致
import {s1, s2, say} from './03_m2.js'

console.log(s1)  // 打印输出 aaa
console.log(s2)  // 打印输出 ccc
console.log(say)  // 打印输出 [Function: say]
```



##### 按需导出与按需导入的注意事项

1. 每个模块中可以使用多次按需导出，默认导出只能一次。
2. 按需导入的成员名称必须和按需导出的名称保持一致
3. 按需导入时，可以使用 as 关键字进行重命名
4. 按需导入可以和默认导入一起使用

```javascript
import info, { s1, s2 as str2, say } from './03_m2.js'

console.log(s1)  // 打印输出 aaa
console.log(str2)  // 打印输出 ccc
console.log(say)  // 打印输出 [Function: say]
console.log(info)  // 打印输出 { a: 20}
```



##### 直接导入并执行模块中的代码

- 如果只想单纯地执行某个模块中的代码，并不需要得到模块中向外共享的成员。此时，可以直接导入并执行模块代码，示例代码如下：

```javascript
// 当前文件模块为 05_m3.js
// 在当前模块中执行一个 for 循环操作
for (let i = 0; i < 3; i++) {
  console.log(i)
}
```



```javascript
// 直接导入并执行模块代码，不需要得到模块向外共享的成员
import './05_m3.js'
```





### Promise

#### 回调地狱

- 多层回调函数的相互嵌套，就形成了回调地狱。示例代码如下：

```javascript
// 第 1 层回调地狱
setTimeout(() => {
    console.log('延时 1 秒后输出');
	// // 第 2 层回调地狱
    setTimeout(() => {
        console.log('再延时 2 秒后输出');
        // 第 3 层回调地狱
        setTimeout(() => {
            console.log('再延时 3 秒后输出');
        }, 3000);
    }, 2000);
}, 1000);
```

- 代码耦合性太强，牵一发而动全身，难以维护
- 大量冗余的代码相互嵌套，代码的可读性变差



- 为了解决回调地狱的问题，ES6（ECMAScript 2015）中新增了 Promise 的概念。



#### Promise

- Promise 是一个构造函数
  - 我们可以创建 Promise 的实例 `const p = new Promise()`
  - new 出来的 Promise 实例对象，代表一个异步操作

- `Promise.prototype` 上包含一个 `.then()` 方法
  - 每一次 new Promise() 构造函数得到的实例对象
  - 都可以通过原型链的方式访问到 `.then()` 方法，例如 `p.then()`
- `.then()` 方法用来预先指定成功和失败的回调函数
  - `p.then`(成功的回调函数，失败的回调函数)
  - `p.then(result => { }, error => { })`
  - 调用 .then() 方法时，成功的回调函数是必选的、失败的回调函数是可选的



#### .then() 方法的特性

- 如果上一个 .then() 方法中返回了一个新的Promise 实例对象，则可以通过下一个 .then() 继续进行处理。通过 .then() 方法的链式调用，就解决了回调地狱的问题。





#### 基于 then-fs 读取文件内容

- 由于 node.js 官方提供的 fs 模块仅支持以回调函数的方式读取文件，不支持Promise 的调用方式。因此，需要先运行如下的命令，安装 then-fs 这个第三方包，从而支持我们基于 Promise 的方式读取文件的内容：

```bash
npm i then-fs
```

- 调用 then-fs 提供的 readFile() 方法，可以异步地读取文件的内容，它的返回值是 Promise 的实例对象。因此可以调用 .then() 方法为每个 Promise 异步操作指定成功和失败之后的回调函数。示例代码如下：

```javascript
// 基于 Promise 的方式读取文件
import thenFs from 'then-fs'
// 注意：.then() 中的失败回调是可选的，可以被省略
thenFs.readFile('./files/1.txt', 'utf8').then(r1 => { console.log(r1) }, err1 => { console.log(err1) })
thenFs.readFile('./files/2.txt', 'utf8').then(r2 => { console.log(r2) }, err2 => { console.log(err2) })
thenFs.readFile('./files/3.txt', 'utf8').then(r3 => { console.log(r3) }, err3 => { console.log(err3) })
```

- **注意：上述的代码无法保证文件的读取顺序！！**

#### 按顺序读取文件

- Promise 支持链式调用，从而来解决回调地狱的问题。示例代码如下：

```javascript
import thenFs from 'then-fs'


thenFs.readFile('./files/1.txt', 'utf8') // 返回值是 Promise 的实例对象
    .then((r1) => { // 通过 .then 为第一个 Promise 实例指定成功之后的回调函数
        console.log(r1)
        return thenFs.readFile('./files/2.txt', 'utf8') // 在第一个 .then 中返回一个新的 Promise 实例对象
    })
    .then((r2) => { // 继续调用 .then，为上一个 .then 的返回值（新的 Promise 实例）指定成功之后的回调函数
        console.log(r2)
        return thenFs.readFile('./files/3.txt', 'utf8') // 在第二个 .then 中返回一个新的 Promise 实例对象
    })
    .then((r3) => { // 继续调用 .then，为上一个 .then 的返回值（新的 Promise 实例）指定成功之后的回调函数
        console.log(r3)
    })
```

##### 通过 .catch 捕获错误

- 在 Promise 的链式操作中如果发生了错误，可以使用 `Promise.prototype.catch` 方法进行捕获和处理：

```javascript
import thenFs from 'then-fs'

thenFs.readFile('./files/11.txt', 'utf8') // 文件不存在导致读取失败，后面的 3 个.then 都不执行
    .then((r1) => {
        console.log(r1)
        return thenFs.readFile('./files/2.txt', 'utf8')
    })
    .then((r2) => {
        console.log(r2)
        return thenFs.readFile('./files/3.txt', 'utf8')
    })
    .then((r3) => {
        console.log(r3)
    })
    .catch((err) => { // 捕获第 1 行发生的错误，并输出错误的消息 ENOENT: no such file or directory, open 'C:\Users\dell\Desktop\Vue\day 01\code\code1\files\11.txt'
        console.log(err.message)
    })
```

- 如果不希望前面的错误导致后续的 .then 无法正常执行，则可以将.catch 的调用提前，示例代码如下：

```javascript
import thenFs from 'then-fs'

thenFs.readFile('./files/11.txt', 'utf8')
    .catch((err) => { // 捕获第 1 行发生的错误，并输出错误的消息 ENOENT: no such file or directory, open 'C:\Users\dell\Desktop\Vue\day 01\code\code1\files\11.txt'
        console.log(err.message) // 由于错误已被及时处理，不影响后续 .then 的正常执行
    })
    .then((r1) => {
        console.log(r1) // 输出 undefined
        return thenFs.readFile('./files/2.txt', 'utf8')
    })
    .then((r2) => {
        console.log(r2) // 输出 222
        return thenFs.readFile('./files/3.txt', 'utf8')
    })
    .then((r3) => {
        console.log(r3) // 输出 333
    })
```



#### Promise.all() 方法

- Promise.all() 方法会发起并行的 Promise 异步操作，等所有的异步操作全部结束后才会执行下一步的 .then操作（等待机制）。示例代码如下

```javascript
import thenFs from 'then-fs'

// 定义一个数组，存放 3 个读文件的异步操作
const promiseArr = [
    thenFs.readFile('./files/3.txt', 'utf8'),
    thenFs.readFile('./files/2.txt', 'utf8'),
    thenFs.readFile('./files/1.txt', 'utf8'),
]

// 将 Promise 的数组，作为 Promise.all() 的参数
Promise.all(promiseArr).then(result => { // 所有文件读取成功（等待机制）
        console.log(result); // 输出 [ '333', '222', '111' ]
    })
    .catch(err => {
        console.log(err.message);
    })
Promise.all(promiseArr)
    .then(([r1, r2, r3]) => { // 所有文件读取成功（等待机制）
        console.log(r1); // 输出 333
        console.log(r2); // 输出 222
        console.log(r3); // 输出 111
    })
    .catch(err => {
        console.log(err.message);
    })
```



#### Promise.race() 方法

- Promise.race() 方法会发起并行的 Promise 异步操作，只要任何一个异步操作完成，就立即执行下一步的.then 操作（赛跑机制）。示例代码如下：

```javascript
import thenFs from 'then-fs'

// 定义一个数组，存放 3 个读文件的异步操作
const promiseArr = [
    thenFs.readFile('./files/3.txt', 'utf8'),
    thenFs.readFile('./files/2.txt', 'utf8'),
    thenFs.readFile('./files/1.txt', 'utf8'),
]

// 将 Promise 的数组，作为 Promise.race() 的参数
Promise.race(promiseArr).then(result => { // 只要任何一个异步操作完成，就立即执行成功的回调函数（赛跑机制）
        console.log(result); // 输出 333 也可能是 111
    })
    .catch(err => { // 捕获 Promise 异步操作中的错误
        console.log(err.message);
    })
```



#### 基于 Promise 封装读文件的方法

- 方法的封装要求：
  1. 方法的名称要定义为 getFile
  2. 方法接收一个形参 fpath，表示要读取的文件的路径
  3. 方法的返回值为 Promise 实例对象

##### getFile 方法的基本定义

- 代码示例：
- 注意：第 5 行代码中的 new Promise() 只是创建了一个形式上的异步操作。

```javascript
// 方法的名称为 getFile
// 方法接收一个形参 fpath，表示要读取的文件的路径
function getFile(fpath) {
    // 方法的返回值为 Promise 的实例对象
    return new Promise()
}
```

##### 创建具体的异步操作

- 如果想要创建具体的异步操作，则需要在new Promise() 构造函数期间，传递一个function 函数，将具体的异步操作定义到 function 函数内部。示例代码如下：

```javascript
import fs from 'fs'
// 方法的名称为 getFile
// 方法接收一个形参 fpath，表示要读取的文件的路径
function getFile(fpath) {
    // 方法的返回值为 Promise 的实例对象
    return new Promise(() => {
        // 下面这行代码，表示这是一个具体的、读文件的异步操作
        fs.readFile(fpath, 'utf8', (err, dataStr) => {

        })
    })
}
```

##### 获取 .then 的两个实参

- 通过 .then() 指定的成功和失败的回调函数，可以在 function 的形参中进行接收，示例代码如下：

```javascript
import fs from 'fs'
function getFile(fpath) {
    // resolve 形参是：调用 getFiles() 方法时，通过 .then 指定的"成功的"回调函数
    // reject 形参是：调用 getFiles() 方法时，通过 .then 指定的"失败的"回调函数
    return new Promise((resolve, reject) => {
        fs.readFile(fpath, 'utf8', (err, dataStr) => {

        })
    })
}
```

##### 调用 resolve 和 reject 回调函数

- Promise 异步操作的结果，可以调用 resolve 或 reject 回调函数进行处理。示例代码如下：

```javascript
import fs from 'fs'
function getFile(fpath) {
    return new Promise((resolve, reject) => {
        // 下面这行代码，表示这是一个具体的、读文件的异步操作
        fs.readFile(fpath, 'utf8', (err, dataStr) => {
            if (err) return reject(err) // 如果读取失败，则调用"失败的回调函数"
            resolve(dataStr) // 如果读取成功，则调用"成功的回调函数"
        })
    })
}
```

##### 调用封装好的方法

```javascript
getFile('./files/11.txt')
    .then((r1) => {
        console.log(r1)
    })
    .catch((err) => {
        console.log(err.message)
    })
```



###  async/await

- async/await 是 ES8（ECMAScript 2017）引入的新语法，用来简化 Promise 异步操作。在 async/await 出现之前，开发者只能通过链式.then() 的方式处理 Promise 异步操作。示例代码如下：

```javascript
thenFs.readFile('./files/1.txt', 'utf8')
    .then((r1) => {
        console.log(r1)
        return thenFs.readFile('./files/2.txt', 'utf8')
    })
    .then((r2) => {
        console.log(r2)
        return thenFs.readFile('./files/3.txt', 'utf8')
    })
    .then((r3) => {
        console.log(r3)
    })
```

- .then 链式调用的优点：解决了回调地狱的问题
- .then 链式调用的缺点：代码冗余、阅读性差、不易理解



- 使用 async/await 简化 Promise 异步操作的示例代码如下：

```javascript
import thenFs from 'then-fs'

// 按照顺序读取文件 1, 2, 3 的内容
async function getAllFile() {
    const r1 = await thenFs.readFile('./files/1.txt', 'utf8')
    console.log(r1)
    const r2 = await thenFs.readFile('./files/2.txt', 'utf8')
    console.log(r2)
    const r3 = await thenFs.readFile('./files/3.txt', 'utf8')
    console.log(r3)
}

getAllFile()
// 输出
// 111
// 222
// 333
```



#### 注意事项

1. 如果在 function 中使用了 await，则 function 必须被 async 修饰
2. 在 async 方法中，第一个 await 之前的代码会同步执行，await 之后的代码会异步执行

```javascript
import thenFs from 'then-fs'

console.log('A')
async function getAllFile() {
    console.log('B')
    // 遇到 await 后，后面的代码异步执行
    const r1 = await thenFs.readFile('./files/1.txt', 'utf8')
    console.log(r1)
    const r2 = await thenFs.readFile('./files/2.txt', 'utf8')
    console.log(r2)
    const r3 = await thenFs.readFile('./files/3.txt', 'utf8')
    console.log(r3)
    console.log('D')
}

getAllFile()
console.log('C')

// 输出
// A
// B
// C
// 111
// 222
// 333
// D
```

### EventLoop

#### JavaScript 是单线程的语言

- JavaScript 是一门单线程执行的编程语言。也就是说，同一时间只能做一件事情。

![image-20220414105805674](http://zjp.hxkj.live/MDImage/Vue/JavaScript%e5%8d%95%e7%ba%bf%e7%a8%8b_2022-04-14_10-58-21.png)

- 单线程执行任务队列的问题：如果前一个任务非常耗时，则后续的任务就不得不一直等待，从而导致程序假死的问题。

#### 同步任务和异步任务

- 为了防止某个耗时任务导致程序假死的问题，JavaScript 把待执行的任务分为了两类：
  - 同步任务（synchronous）
    - 又叫做非耗时任务，指的是在主线程上排队执行的那些任务
    - 只有前一个任务执行完毕，才能执行后一个任务
  - 异步任务（asynchronous）
    - 又叫做耗时任务，异步任务由 JavaScript 委托给宿主环境进行执行
    - 当异步任务执行完成后，会通知 JavaScript 主线程执行异步任务的回调函数

#### 同步任务和异步任务的执行过程

1. 同步任务由 JavaScript 主线程次序执行
2. 异步任务委托给宿主环境执行
3. 已完成的异步任务对应的回调函数，会被加入到任务队列中等待执行
4. JavaScript 主线程的执行栈被清空后，会读取任务队列中的回调函数，次序执行
5. JavaScript 主线程不断重复上面的第 4 步

![image-20220414110140963](http://zjp.hxkj.live/MDImage/Vue/%e5%90%8c%e6%ad%a5%e4%bb%bb%e5%8a%a1%e5%92%8c%e5%bc%82%e6%ad%a5%e4%bb%bb%e5%8a%a1%e7%9a%84%e6%89%a7%e8%a1%8c%e8%bf%87%e7%a8%8b_2022-04-14_11-01-51.png)

#### EventLoop 的基本概念

- JavaScript 主线程从“任务队列”中读取异步任务的回调函数，放到执行栈中依次执行。这个过程是循环不断的，所以整个的这种运行机制又称为 EventLoop（事件循环）。

```javascript
import thenFs from 'then-fs'

console.log('A')
thenFs.readFile('./files/1.txt', 'utf8').then(dataStr => {
    console.log('B')
})
setTimeout(()=>{
    console.log('C')
}, 0)
console.log('D')

// 输出
// A
// D
// C
// B
```

- A 和 D 属于同步任务。会根据代码的先后顺序依次被执行
- C 和 B 属于异步任务。它们的回调函数会被加入到任务队列中，等待主线程空闲时再执行



### 宏任务和微任务

- JavaScript 把异步任务又做了进一步的划分，异步任务又分为两类，分别是：
  - 宏任务（macrotask）
    - 异步 Ajax 请求
    - setTimeout、setInterval
    - 文件操作
    - 其它宏任务
  -  微任务（microtask）
    - Promise.then、.catch 和 .finally
    - process.nextTick
    - 其它微任务

![image-20220414112011541](http://zjp.hxkj.live/MDImage/Vue/%e5%ae%8f%e4%bb%bb%e5%8a%a1%e5%92%8c%e5%be%ae%e4%bb%bb%e5%8a%a1_2022-04-14_11-20-27.png)

#### 宏任务和微任务的执行顺序

- 每一个宏任务执行完之后，都会检查是否存在待执行的微任务，如果有，则执行完所有微任务之后，再继续执行下一个宏任务。

![image-20220414112103035](http://zjp.hxkj.live/MDImage/Vue/%e5%ae%8f%e4%bb%bb%e5%8a%a1%e5%92%8c%e5%be%ae%e4%bb%bb%e5%8a%a1%e7%9a%84%e6%89%a7%e8%a1%8c%e9%a1%ba%e5%ba%8f_2022-04-14_11-21-09.png)

![image-20220414112708595](http://zjp.hxkj.live/MDImage/Vue/%e5%ae%8f%e4%bb%bb%e5%8a%a1%e5%92%8c%e5%be%ae%e4%bb%bb%e5%8a%a1%e7%9a%84%e6%89%a7%e8%a1%8c%e9%a1%ba%e5%ba%8f_2022-04-14_11-27-11.png)



![image-20220414112821455](http://zjp.hxkj.live/MDImage/Vue/%e5%ae%8f%e4%bb%bb%e5%8a%a1%e5%92%8c%e5%be%ae%e4%bb%bb%e5%8a%a1%e7%9a%84%e6%89%a7%e8%a1%8c%e9%a1%ba%e5%ba%8f_2022-04-14_11-28-23.png)

### API 接口案例

- 基于 MySQL 数据库 + Express 对外提供用户列表的 API 接口服务。用到的技术点如下：
  - 第三方包 express 和 mysql2
  -  ES6 模块化
  -  Promise
  - async/await

- 主要的实现步骤
  1. 搭建项目的基本结构
  2. 创建基本的服务器
  3. 创建 db 数据库操作模块
  4. 创建 user_ctrl 业务模块
  5. 创建 user_router 路由模块

#### 搭建项目的基本结构

- 启用 ES6 模块化支持

  - 初始化项目 package.json

  ```bash
  npm init -y
  ```

  - 在 package.json 中声明 `"type": "module",`

- 安装第三方依赖包

  - 运行 npm install express@4.17.1 mysql2@2.2.5

  ```bash
  npm install express@4.17.1 mysql2@2.2.5
  ```



#### 创建基本的服务器

- 在根目录下创建 `app.js` 文件
- 初始化 `app.js` 文件代码内容

```javascript
// 使用 ES6 的默认导入语法
import express from "express";
const app = express();

app.listen(80, () => {
    console.log('server running at http://127.0.0.1');
})
```



#### 创建 db 数据库操作模块

- 在根目录下创建 `db` 文件夹，并创建 `index.js` 文件
- 初始化 `index.js` 文件代码内容

```javascript
import mysql from 'mysql2'

const pool = mysql.createPool({
    host: '127.0.0.1',
    port: 3306,
    database: 'my_db_01', // 请填写要操作的数据库的名称
    user: 'root', // 请填写登陆数据库的用户名
    password: '1234' // 请填写登陆数据库的密码
})


// 默认导出一个支持 Promise API 的 pool
export default pool.promise()
```



#### 创建 user_ctrl 模块

- 在根目录下创建 `controller` 文件夹，并创建 `user_ctrl.js` 文件

- 初始化 `user_ctrl.js` 文件代码内容

```javascript
import db from '../db/index.js';

// 获取所有用户的列表数据
export async function getAllUser(req, res) {
    // db.query() 函数的返回值是 Promise 的实例对象。因此，可以使用 async/await 进行简化
    const [rows] = await db.query('select id, username, nickname from ev_users')
    res.send({
        status: 0,
        message: '获取用户列表数据成功',
        data: rows
    })
}
```



##### 使用 try…catch 捕获异常

```javascript
import db from '../db/index.js';

// 使用 ES6 的按需导出语法，将 getAllUser 方法导出出去
// 获取所有用户的列表数据
export async function getAllUser(req, res) {
    // 使用 try...catch 捕获 Promise 异步任务中产生的异常错误，并在 catch 块中进行处理
    try {
        // ev_users 表中没有 xxx 字段，所以此 SQL 语句会"执行异常"
        const [rows] = await db.query('select id, username, nickname, xxx from ev_users')
        res.send({
            status: 0,
            message: '获取用户列表数据成功',
            data: rows
        })
    } catch (e) {
        res.send({
            status: 1,
            message: '获取用户列表数据失败',
            desc: e.message
        })
    }
}
```







#### 创建 user_router 模块

- 在根目录下创建 `router` 文件夹，并创建 `user_router.js` 文件
- 初始化 `user_router.js` 文件代码内容

```javascript
import express from "express";
// 从 user_ctrl.js 模块中按需导入 getAllUser 函数
import { getAllUser } from "../controller/user_ctrl.js"

// 创建路由对象
const router = new express.Router()
// 挂载路由规则
router.get('/user', getAllUser)

// 使用 ES6 的默认导出语法，将路由对象共享出去
export default router
```



#### 导入并挂载路由模块

- 在 `app.js` 的头部区域导入用户路由模块

```javascript
// 使用默认导入语法，导入路由对象
import userRouter from './router/user_router.js'
```

- 在 `app.js` 的内部挂载用户路由模块

```javascript
// 挂载用户路由模块
app.use('/api', userRouter)
```

- 完整代码

```javascript
// 使用 ES6 的默认导入语法
import express from "express";
// 使用默认导入语法，导入路由对象
import userRouter from './router/user_router.js'
const app = express();

// 挂载用户路由模块
app.use('/api', userRouter)

app.listen(80, () => {
    console.log('server running at http://127.0.0.1');
})
```

#### 测试接口

- 使用 `Postman`，向 `http://127.0.0.1/api/user` ，发起 `GET` 请求，测试接口

![image-20220414195525221](http://zjp.hxkj.live/MDImage/Vue/%e6%b5%8b%e8%af%95%e6%8e%a5%e5%8f%a3_2022-04-14_19-55-29.png)













#### 注意

1. 所有的 import 语句，都写在当前模块的最头部区域。

```javascript
// 使用 ES6 的默认导入语法
import express from "express";
// 使用默认导入语法，导入路由对象
import userRouter from './router/user_router.js'


// 逻辑编写……
```









## 前端工程化

- 小白眼中的前端开发：
  - 会写 HTML + CSS + JavaScript 就会前端开发
  - 需要美化页面样式，就拽一个bootstrap 过来
  - 需要操作 DOM 或发起 Ajax 请求，再拽一个 jQuery 过来
    -  需要快速实现网页布局效果，就拽一个 Layui 过来
- 实际的前端开发：
  - 模块化（js 的模块化、css 的模块化、资源的模块化）
  - 组件化（复用现有的 UI 结构、样式、行为）
  - 规范化（目录结构的划分、编码规范化、接口规范化、文档规范化、 Git 分支管理）
  - 自动化（自动化构建、自动部署、自动化测试）

- 前端工程化指的是：在企业级的前端项目开发中，把前端开发所需的工具、技术、流程、经验等进行规范化、标准化。
- 企业中的 Vue 项目和 React 项目，都是基于工程化的方式进行开发的。
- 好处：前端开发自成体系，有一套标准的开发方案和流程。

- 早期的前端工程化解决方案：
  - grunt（ https://www.gruntjs.net/ ）
  - gulp（ https://www.gulpjs.com.cn/ ）
- 目前主流的前端工程化解决方案：
  - webpack（ https://www.webpackjs.com/ ）
  - parcel（ https://zh.parceljs.org/ ）



## webpack

- 概念：webpack 是前端项目工程化的具体解决方案。

- 主要功能：它提供了友好的前端模块化开发支持，以及代码压缩混淆、处理浏览器端 JavaScript 的兼容性、性
  能优化等强大的功能。
- 好处：让程序员把工作的重心放到具体功能的实现上，提高了前端开发效率和项目的可维护性。
- 注意：目前 Vue，React 等前端项目，基本上都是基于 webpack 进行工程化开发的。

### 创建列表隔行变色项目

- 步骤
  - 新建项目空白目录，并运行 `npm init –y` 命令，初始化包管理配置文件 `package.json`
  -  新建 `src` **源代码目录**
  -  新建 `src -> index.html` 首页和 `src -> index.js` 脚本文件
  -  初始化首页基本的结构
  - 运行 `npm install jquery –S` 命令，安装 jQuery
    - `-S` 的作用是让 `package.json` 记录 `jquery` 的版本信息，完整写法 `--save`，不加也可以。
  - 通过 ES6 模块化的方式导入 `jQuery`，实现列表隔行变色效果



```html
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="./index.js"></script>
</head>

<body>
    <ui>
        <li>这是第 1 个 li</li>
        <li>这是第 2 个 li</li>
        <li>这是第 3 个 li</li>
        <li>这是第 4 个 li</li>
        <li>这是第 5 个 li</li>
        <li>这是第 6 个 li</li>
        <li>这是第 7 个 li</li>
        <li>这是第 8 个 li</li>
        <li>这是第 9 个 li</li>
    </ui>
</body>

</html>
```



```javascript
// 1. 使用 ES6 导入语法，导入 jQuery
import $ from 'jquery';

// 2. 定义 jQuery 的入口函数
$(function() {
    // 3. 实现奇偶行变色
    // 奇数行为红色
    $('li:odd').css('background-color', 'red');
    $('li:even').css('background-color', 'pink');
    // 0 是偶数
    // 1 是奇数
});
```

- `import $ from 'jquery';` 存在兼容性问题，无法运行。

![image-20220410171543183](http://zjp.hxkj.live/MDImage/Vue/%e6%b5%8f%e8%a7%88%e5%99%a8%e5%85%bc%e5%ae%b9%e6%80%a7%e9%97%ae%e9%a2%98_2022-04-10_17-16-03.png)

### webpack 的基本使用

#### 安装

- 在终端运行如下的命令，安装webpack 相关的两个包：

```bash
# -D 是 --save-dev 的简写 开发环境需要使用，生产环境不需要使用
# -S 是 --save 的简写 开发环境和生产环境都需要使用
npm install webpack@5.42.1 webpack-cli@4.9.0 -D
```

#### 配置和使用

- 在项目根目录中，创建名为 `webpack.config.js` 的 `webpack` 配置文件，并初始化如下的基本配置：

```javascript
module.exports = {
    // mode 代表 webpack 运行的模式，可选值有两个 development 和 production
    // 结论：开发时候一定要用 development，因为追求的是打包的速度，而不是体积；
    // 反过来，发布上线的时候一定能要用 production，因为上线追求的是体积小，而不是打包速度快！
    mode: 'development' // mode 用来指定构建模式。可选值有 development 和 production
}
```

- 在 `package.json` 的 `scripts` 节点下，新增 dev 脚本如下：

```json
// “dev” 可以取其他名字，只是一个执行脚本名
"scripts": {
    "dev": "webpack",  // script 节点下的脚本，可以通过 npm run 运行。例如 npm run dev
},
```

-  在终端中运行 `npm run dev` 命令，启动 webpack 进行项目的打包构建

```bash
npm run dev
```

##### mode 的可选值

- mode 节点的可选值有两个，分别是：
  1. development
     - 开发环境
     - **不会**对打包生成的文件进行代码压缩和性能优化
     - 打包速度快，适合在开发阶段使用
  2. production
     - 生产环境
     - **会**对打包生成的文件进行代码压缩和性能优化
     - 打包速度很慢，仅适合在项目发布阶段使用

##### webpack.config.js 文件的作用

- webpack.config.js 是 webpack 的配置文件。webpack 在真正开始打包构建之前，会先读取这个配置文件，
  从而基于给定的配置，对项目进行打包。
- 注意：由于 webpack 是基于 node.js 开发出来的打包工具，因此在它的配置文件中，支持使用 node.js 相关
  的语法和模块进行 webpack 的个性化配置。

#####  webpack 中的默认约定

- 在 webpack 4.x 和 5.x 的版本中，有如下的默认约定：
  - 默认的打包入口文件为 `src -> index.js`
  - 默认的输出文件路径为 `dist -> main.js`

- 注意：可以在 webpack.config.js 中修改打包的默认约定

##### 自定义打包的入口与出口

- 在 `webpack.config.js` 配置文件中，通过 entry 节点指定打包的入口。通过 output 节点指定打包的出口。
  示例代码如下

```javascript
// 导入 node.js 中专门操作路径模块
const path = require('path');

entry: path.join(__dirname, './src/index.js'), // 打包入口文件的路径
    output: {
        path: path.join(__dirname, './dist'), // 输出文件的存放地址
            filename: 'bundle.js' // 输出文件的名称
    },
}
```

### webpack-dev-server 插件

- 类似于 `node.js` 阶段用到的 `nodemon` 工具
- 每当修改了源代码，`webpack` 会自动进行项目的打包和构建

- webpack-dev-server 可以让 webpack 监听项目源代码的变化，从而进行自动打包构建。

#### 安装

- 运行如下的命令，即可在项目中安装此插件：

```bash
npm install webpack-dev-server@4.9.0 -D
```

#### 配置

- 修改 `package.json -> scripts` 中的 `dev ` 命令如下：

```json
"scripts": {
    /*
    "dev": "webpack",
    */
    "dev": "webpack serve",  // script 节点下的脚本，可以通过 npm run 运行。例如 npm run dev
},
```

- 再次运行 `npm run dev`命令，重新进行项目的打包

```bash
npm run dev
```

- 修改 `index.html` 中 `js` 文件的索引

```html
<!-- 旧索引 -->
<!-- <script src="../dist/main.js"></script> -->
<!-- 加载和引用内存中的 main.js -->
<script src="/main.js"></script>
```

- 在浏览器中访问 http://localhost:8080 地址，进入 `src` 目录，查看自动打包效果

- 注意：webpack-dev-server 会启动一个实时打包的 http 服务器



##### devServer 节点

- 在 webpack.config.js 配置文件中，可以通过 devServer 节点对 webpack-dev-server 插件进行更多的配置，
  示例代码如下：

```javascript
module.exports = { 
    devServer: {
        // 首次打包成功后，自动打开浏览器
        open: true,
        // 在 http 协议中，如果端口号是 80，则可以被省略
        port: 80,
        // 指定运行的主机地址
        host: '127.0.0.1'
    },
}
```

- 注意：凡是修改了 webpack.config.js 配置文件，或修改了 package.json 配置文件，必须重启实时打包的服
  务器，否则最新的配置文件无法生效！



#### 注意事项

- 打包生成的文件哪儿去了？
  - 不配置 webpack-dev-server 的情况下，webpack 打包生成的文件，会存放到实际的物理磁盘上
    - 严格遵守开发者在 webpack.config.js 中指定配置
    - 根据 output 节点指定路径进行存放
  - 配置了 webpack-dev-server 之后，打包生成的文件存放到了内存中
    - 不再根据 output 节点指定的路径，存放到实际的物理磁盘上
    - 提高了实时打包输出的性能，因为内存比物理磁盘速度快很多



- 生成到内存中的文件该如何访问？
  - webpack-dev-server 生成到内存中的文件，默认放到了项目的根目录中，而且是虚拟的、不可见的。
  - 可以直接用 / 表示项目根目录，后面跟上要访问的文件名称，即可访问内存中的文件
  - 例如 /bundle.js 就表示要访问 webpack-dev-server 生成到内存中的 bundle.js 文件













### html-webpack-plugin 插件

- webpack 中的 HTML 插件（类似于一个模板引擎插件）
- 可以通过此插件自定制 index.html 页面的内容
- html-webpack-plugin 是 webpack 中的 HTML 插件，可以通过此插件自定制 index.html 页面的内容。
- 需求：通过 html-webpack-plugin 插件，将 src 目录下的 index.html 首页，复制到项目根目录中一份

#### 安装

- 运行如下的命令，即可在项目中安装此插件：

```bash
npm install html-webpack-plugin@5.3.2 -D
```

#### 配置

- 在 `webpack.config.js` 中配置 `html-webpack-plugin`

```javascript
// 1. 导入 html-webpack-plugin 这个插件，得到插件的构造函数
const HtmlPlugin = require('html-webpack-plugin');
```

```javascript
// 2. new 构造函数，创建插件的实例对象
const htmlPlugin = new HtmlPlugin({
    // 指定要复制哪个页面
    template: './src/index.html',
    // 指定复制出来的文件名和存放路径
    filename: './index.html'
});
```

```javascript
module.exports = {
    plugins: [htmlPlugin], // 通过 plugins 节点，使 htmlPlugin 插件生效
}
```

#### 功能

- 通过 HTML 插件复制到项目根目录中的 `index.html` 页面，也被放到了内存中
- HTML 插件在生成的 `index.html` 页面，自动注入了打包的 .js 文件，所以在 `index.html` 中需要注释掉 `js` 文件的引用

```html
<!-- <script src="/main.js"></script> -->
```





### webpack 中的 loader

- 在实际开发过程中，webpack 默认只能打包处理以 .js 后缀名结尾的模块。其他非 .js 后缀名结尾的模块，
  webpack 默认处理不了，需要调用 loader 加载器才可以正常打包，否则会报错！
- loader 加载器的作用：协助 webpack 打包处理特定的文件模块。比如：
  - css-loader 可以打包处理 .css 相关的文件
  - less-loader 可以打包处理 .less 相关的文件
  - babel-loader 可以打包处理 webpack 无法处理的高级 JS 语法

![image-20220411004233638](http://zjp.hxkj.live/MDImage/Vue/loader%e5%a4%84%e7%90%86%e8%bf%87%e7%a8%8b_2022-04-11_00-42-40.png)

#### 打包处理 css文件

- 一切皆模块，但在 `index.js` 文件中导入 `css` 路径，打包时候会报错

```css
li {
    list-style: none;
}
```



```javascript
// 导入样式
// 在 webpack 中，一切皆模块，都可以通过 ES6 导入语法进行导入和使用
// 如果某个模块中，使用 from 接收到的成员为 undefined，则没有必要进行接收
import './css/index.css';
```



##### 安装

-  运行命令，安装处理 css 文件的 loader

```bash
npm i style-loader@3.0.0 css-loader@5.2.6 -D
```

##### 配置和处理 css 文件

-  在 `webpack.config.js` 的 module -> rules 数组中，添加 loader 规则如下：
- 其中，test 表示匹配的文件类型， use 表示对应要调用的 loader

```javascript
module.exports = {
    // 所有第三方文件模块的匹配规则
    module: {
        rules: [
            // 文件后缀名的匹配规则
            // 处理 .css 文件的 loader
            { test: /\.css$/, use: ['style-loader', 'css-loader'] },
        ]
    },
}
```

- 注意：
  - use 数组中指定的 loader 顺序是固定的
  - 多个 loader 的调用顺序是：从后往前调用

![01.loader调用的过程 - 副本](http://zjp.hxkj.live/MDImage/Vue/loader%e8%b0%83%e7%94%a8%e7%9a%84%e8%bf%87%e7%a8%8b_2022-04-11_01-03-17.png)

#### 打包处理 less 文件

- 一切皆模块，但在 `index.js` 文件中导入 `less` 路径，打包时候会报错

```less
html,
body,
ul {
    margin: 0;
    padding: 0;

    li {
        line-height: 30px;
        padding-left: 20px;
        font-size: 12px;
    }
}
```



```javascript
// 导入样式
// 在 webpack 中，一切皆模块，都可以通过 ES6 导入语法进行导入和使用
import './css/index.less';
```

##### 安装

-  运行命令，安装处理 less 文件的 loader，同时也需要安装处理 css 文件的 loader

```javascript
npm i style-loader@3.0.0 css-loader@5.2.6 -D
npm i less-loader@10.0.1 less@4.1.1 -D
```

##### 配置和处理 less 文件

-  在 webpack.config.js 的 module -> rules 数组中，添加 loader 规则如下：

```javascript
module.exports = {
    // 所有第三方文件模块的匹配规则
    module: {
        rules: [
            // 文件后缀名的匹配规则
            // 处理 .less 文件的 loader
            { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
        ]
    },
}
```



#### 打包处理样式表中与 url 路径相关的文件

- 小图片为了防止多次请求，有以下解决方案
  - 精灵图
  - 转换为 base64，[网址](https://c.runoob.com/front-end/59/)
- 一切皆模块，但在 `index.js` 文件中导入图片路径，赋值给 `index.html` 中 `<img>` 标签的 `src` 值，打包时候会报错
- 问题： webpack 处理不了 jpg 结尾的文件，需要加载 url 相关 loader。

```html
<!-- 把 /src/images/logo.jpg 设置给 src 属性 -->
<img src="" alt="" class="box">
```

```javascript
// 1. 导入图片，得到图片文件
import logo from './images/logo.jpg';
// 2. 给 img 标签的 src 动态赋值
$('.box').attr('src', logo);
```



##### 安装

- 运行命令，安装处理 url 路径相关文件

```bash
npm i url-loader@4.1.1 file-loader@6.2.0 -D
```

##### 配置和处理 url 文件

-  在 webpack.config.js 的 module -> rules 数组中，添加 loader 规则如下：

```javascript
module.exports = {
    // 所有第三方文件模块的匹配规则
    module: {
        rules: [
            // 文件后缀名的匹配规则
            // 处理 .jpg|.png|.gif 文件的 loader
            { test: /\.jpg|png|gif$/, use: 'url-loader' },
        ]
    },
}
```

- 其中赋值的 `src `是 `base64` 字符串或者路径地址。

###### 配置 use 属性值

- 其中 ? 之后的是 loader 的参数项：
  - limit 用来指定图片的大小，单位是字节（byte）
  - 只有 ≤ limit 大小的图片，才会被转为 base64 格式的图片

```javascript
// 图片小于等于 22229 字节的图片，会被转换成 base64 格式
// 图片大于 22229 字节的图片，不会被转换
{ test: /\.jpg|png|gif$/, use: 'url-loader?limit=22229' },
```

- `outputPath` 指定非 `base64 `格式的图片存放的路径
- 多参数之间使用 & 连接

```javascript
{ test: /\.jpg|png|gif$/, use: 'url-loader?limit=470&outputPath=images' },
```



#### 打包处理 js 文件中的高级语法

- webpack 只能打包处理一部分高级的JavaScript 语法。对于那些 webpack 无法处理的高级 js 语法，需要借
  助于 babel-loader 进行打包处理。例如 webpack 无法处理下面的 JavaScript 代码：

- 在 `index.js` 中使用 js 的高级语法，在打包的时候会出错

```javascript
// 定义名为 info 的装饰器函数
function info(target) {
    // 为模板添加静态属性 info
    target.info = 'Person info.'
}

// 定义一个普通的类
// 为 Person 类应用 info 装饰器
@info
class Person {}

// 打印 Person 的静态属性 info
console.log(Person.info);
```



##### 安装

- 运行命令，安装 babel-loader 相关的包

```javascript
npm i babel-loader@8.2.2 @babel/core@7.14.6 @babel/plugin-proposal-decorators@7.14.5 -D
```



##### 配置和使用

- 在 webpack.config.js 的 module -> rules 数组中，添加 loader 规则如下：

```javascript
module.exports = {
    // 所有第三方文件模块的匹配规则
    module: {
        rules: [
            // 文件后缀名的匹配规则
            // 使用 babel-loader 处理高级的 JS 语法
            // 在配置 babel-loader 的时候，程序员只需要把自己的代码进行转换即可；一定要排除 node_modules 目录中的 JS 文件
            // 因为第三方包中的 JS 兼容性，不需要程序员关心
            { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ }
        ]
    },
}
```

- `@babel/plugin-proposal-decorators@7.14.5` 是 `babel-loader` 中的插件，支持 `js` 装饰器的打包，使用需额外配置
- 在项目根目录下，创建名为 babel.config.js 的配置文件，定义 Babel 的配置项如下：

```javascript
module.exports = {
    // 声明 babel 可用的插件
    // 将来，webpack 在调用 babel-loader 的时候，会先加载 plugins 插件来使用
    plugins: [
        ['@babel/plugin-proposal-decorators', { legacy: true }]
    ]
}
```



### 打包发布

- 项目开发完成之后，需要使用webpack 对项目进行打包发布，主要原因有以下两点：
  - 开发环境下，打包生成的文件存放于内存中，无法获取到最终打包生成的文件
  -  开发环境下，打包生成的文件不会进行代码压缩和性能优化
- 为了让项目能够在生产环境中高性能的运行，因此需要对项目进行打包发布。



#### 配置和使用

- 在 `package.json` 文件的 `scripts` 节点下，新增 `build` 命令如下：

```json
"scripts": {
    "dev": "webpack serve",  // 开发环境中，运行 dev 命令
    "build": "webpack --mode production"  // 项目发布时，运行 build 命令
},
```

- --model 是一个参数项，用来指定 webpack 的运行模式。production 代表生产环境，会对打包生成的文件
  进行代码压缩和性能优化。
- 注意：通过 --model 指定的参数项，会覆盖 webpack.config.js 中的 model 选项。
- 运行 `npm run build` 发布最终文件，路径在 `/dist` 中

##### 把 JavaScript 文件统一生成到 js 目录中

- 在 webpack.config.js 配置文件的 output 节点中，进行如下的配置：

```javascript
module.exports = {
    output: {
        // 存放的目录
        path: path.join(__dirname, 'dist'),
        // 生成的文件名
        filename: 'js/bundle.js'
    },
}
```

##### 把图片文件统一生成到 image 目录中

- 修改 webpack.config.js 中的 url-loader 配置项，新增 `outputPath` 选项即可指定图片文件的输出路径：

```javascript
{ test: /\.jpg|png|gif$/, use: 'url-loader?limit=470&outputPath=images' },
```



#### 自动清理 `dist` 目录下的旧文件

- 为了在每次打包发布时自动清理掉 `dist` 目录中的旧文件，可以安装并配置 `clean-webpack-plugin` 插件：

```bash
npm install clean-webpack-plugin@3.0.0 -D
```

- 导入插件，得到插件的构造函数

```javascript
// 导入插件，得到插件的构造函数
// 注意：左侧花括号是解构赋值
const { CleanWebpackPlugin } = require('clean-webpack-plugin');
```

- 创建插件的实例对象

```javascript
// 创建插件的实例对象
const cleanPlugin = new CleanWebpackPlugin();
```

- 把创建的 `cleanPlugin` 插件实例对象，挂载到 `plugins` 节点中

```javascript
module.exports = {
    plugins: [htmlPlugin, cleanPlugin],
}
```



### Source Map

- 前端项目在投入生产环境之前，都需要对 JavaScript 源代码进行压缩混淆，从而减小文件的体积，提高文件的
  加载效率。此时就不可避免的产生了另一个问题：
- 对压缩混淆之后的代码除错（debug）是一件极其困难的事情
  - 变量被替换成没有任何语义的名称
  - 空行和注释被剔除

- Source Map 就是一个信息文件，里面储存着位置信息。也就是说，Source Map 文件中存储着压缩混淆后的
  代码，所对应的转换前的位置。
- 有了它，出错的时候，除错工具将直接显示原始代码，而不是转换后的代码，能够极大的方便后期的调试。



#### 默认 Source Map 的问题

- 在开发环境下，webpack 默认启用了 Source Map 功能。当程序运行出错时，可以直接在控制台提示错误行
  的位置，并定位到具体的源代码：

- 开发环境下默认生成的 Source Map，记录的是生成后的代码的位置。会导致运行时报错的行数与源代码的行
  数不一致的问题。示意图如下：

![image-20220411041014445](http://zjp.hxkj.live/MDImage/Vue/%e9%bb%98%e8%ae%a4Source_Map%e7%9a%84%e9%97%ae%e9%a2%98_2022-04-11_04-10-30.png)

#### 开发环境下的 Source Map

- 开发环境下，推荐在 webpack.config.js 中添加如下的配置，即可保证运行时报错的行数与源代码的行数
  保持一致：

```javascript
module.exports = {
    // 在开发调试阶段，建议大家都把 devtool 的值设置为 eval-source-map
    devtool: 'eval-source-map',
}
```

#### 生产环境下的 Source Map

- 生产环境中，推荐在 webpack.config.js 中添加如下的配置。
- 在生产环境下，如果省略了 `devtool` 选项，则最终生成的文件中不包含 Source Map。这能够防止原始代码通
  过 Source Map 的形式暴露给别有所图之人。

```javascript
module.exports = {
    // 在实际发布的时候，建议大家把 devtool 的值设置为 nosources-source-map 或直接关闭 SourceMap
    // devtool: 'nosources-source-map',
}
```

##### 只定位行数不暴露源码

- 在生产环境下，如果只想定位报错的具体行数，且不想暴露源码。此时可以将 `devtool` 的值设置为
  `nosources-source-map`。实际效果如图所示：

```javascript
module.exports = {
    // 在实际发布的时候，建议大家把 devtool 的值设置为 nosources-source-map 或直接关闭 SourceMap
    devtool: 'nosources-source-map',
}
```

##### 定位行数且暴露源码

- 在生产环境下，如果想在定位报错行数的同时，展示具体报错的源码。此时可以将 devtool 的值设置为
  source-map。实际效果如图所示：

```javascript
module.exports = {
    devtool: 'source-map',
}
```

- 采用此选项后：你应该将你的服务器配置为，不允许普通用户访问source map 文件！

##### Source Map 总结

- 开发环境下：
  - 建议把 devtool 的值设置为 eval-source-map
  - 好处：可以精准定位到具体的错误行
- 生产环境下：
  - 建议关闭 Source Map 或将 devtool 的值设置为 nosources-source-map
  - 好处：防止源码泄露，提高网站的安全性



### webpack 中 @ 的使用

- 当目录层级很深的时候，需要用到 `../../../` 获取文件太麻烦，也不优雅。
- 使用 @ 代替 `src` 目录，使得引用更加清晰，配置方式如下，添加 `webpack.config.js` 中的配置项 `resolve` 下的 `alias`：

```javascript
module.exports = {
    resolve: {
        alias: {
            // 告诉 webpack，程序员写的代码中，@ 符号表示 src 这一层目录
            '@': path.join(__dirname, './src/');
        }
    }
}
```



```javascript
// 示例
import '@/css/index.css';
```







## Vue

- 官方给出的概念：Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的前端框架。
- 构建用户界面
  + 用 vue 往 html 页面中填充数据，非常的方便
- 框架
  + 框架是一套现成的解决方案，程序员只能遵守框架的规范，去编写自己的业务功能！
  + 要学习 vue，就是在学习 vue 框架中规定的用法！
  + vue 的指令、组件（是对 UI 结构的复用）、路由、Vuex、vue 组件库
  + 只有把上面老师罗列的内容掌握以后，才有开发 vue 项目的能力！

![image-20220411110447509](http://zjp.hxkj.live/MDImage/Vue/Vue%e7%ae%80%e4%bb%8b_2022-04-11_11-04-55.png)

### 特性

- vue 框架的特性，主要体现在如下两方面：

  1. 数据驱动视图
     + 数据的变化**会驱动视图**自动更新
     + 好处：程序员只管把数据维护好，那么页面结构会被 vue 自动渲染出来！

  2. 双向数据绑定

     > 在网页中，form 表单负责**采集数据**，Ajax 负责**提交数据**。

     + js 数据的变化，会被自动渲染到页面上
     + 页面上表单采集的数据发生变化的时候，会被 vue 自动获取到，并更新到 js 数据中

> 注意：数据驱动视图和双向数据绑定的底层原理是 MVVM（Mode 数据源、View 视图、ViewModel 就是 vue 的实例）



#### 数据驱动视图

- 在使用了 vue 的页面中，vue 会监听数据的变化，从而自动重新渲染页面的结构。示意图如下：
- 好处：当页面数据发生变化时，页面会自动重新渲染！
- 注意：数据驱动视图是单向的数据绑定。

![image-20220411111347617](http://zjp.hxkj.live/MDImage/Vue/%e6%95%b0%e6%8d%ae%e9%a9%b1%e5%8a%a8%e8%a7%86%e5%9b%be_2022-04-11_11-13-55.png)

#### 双向数据绑定

- 在填写表单时，双向数据绑定可以辅助开发者在不操作 DOM 的前提下，自动把用户填写的内容同步到数据源
  中。示意图如下：
- 好处：开发者不再需要手动操作 DOM 元素，来获取表单元素最新的值！

![image-20220411112116827](http://zjp.hxkj.live/MDImage/Vue/%e5%8f%8c%e5%90%91%e6%95%b0%e6%8d%ae%e7%bb%91%e5%ae%9a_2022-04-11_11-21-23.png)

### MVVM

- MVVM 是 vue 实现数据驱动视图和双向数据绑定的核心原理。MVVM 指的是 Model、View 和 ViewModel，
  它把每个 HTML 页面都拆分成了这三个部分，如图所示：

![image-20220411112441542](http://zjp.hxkj.live/MDImage/Vue/MVVM_2022-04-11_11-24-46.png)

#### 工作原理

- ViewModel 作为 MVVM 的核心，是它把当前页面的数据源（Model）和页面的结构（View）连接在了一起。

![image-20220411112730366](http://zjp.hxkj.live/MDImage/Vue/MVVM%e7%9a%84%e5%b7%a5%e4%bd%9c%e5%8e%9f%e7%90%86_2022-04-11_11-27-36.png)

- 当数据源发生变化时，会被 ViewModel 监听到，VM 会根据最新的数据源自动更新页面的结构
- 当表单元素的值发生变化时，也会被 VM 监听到，VM 会把变化过后最新的值自动同步到Model 数据源中



### 版本

- 当前，vue 共有 3 个大版本，其中：
  - 2.x 版本的 vue 是目前企业级项目开发中的主流版本
  - 3.x 版本的 vue 于 2020-09-19 发布，生态还不完善，尚未在企业级项目开发中普及和推广
  - 1.x 版本的 vue 几乎被淘汰，不再建议学习与使用
- 总结：
  - 3.x 版本的 vue 是未来企业级项目开发的趋势；
  - 2.x 版本的 vue 在未来（1 ~ 2年内）会被逐渐淘汰；

### 基本使用

- 导入 vue.js 的 script 脚本文件
- 在页面中声明一个将要被 vue 所控制的 DOM 区域
- 创建 vm 实例对象（vue 实例对象）

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <!-- 希望 Vue 能够控制下面的这个 div，帮我们在把数据填充到 div 内部 -->
    <div id="app">{{ username }}</div>

    <!-- 1. 导入 Vue 的库文件，在 window 全局就有了 Vue 这个构造函数 -->
    <script src="./lib/vue-2.6.12.js"></script>
    <!-- 2. 创建 Vue 的实例对象 -->
    <script>
        // 创建 Vue 的实例对象
        const vm = new Vue({
            // el 属性是固定的写法，表示当前 vm 实例要控制页面上的哪个区域，接收的值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                username: 'zhangsan'
            }
        })
    </script>
</body>

</html>
```

#### 基本代码与 MVVM 的对应关系

![image-20220411144926061](http://zjp.hxkj.live/MDImage/Vue/%e5%9f%ba%e6%9c%ac%e4%bb%a3%e7%a0%81%e4%b8%8eMVVM%e7%9a%84%e5%af%b9%e5%ba%94%e5%85%b3%e7%b3%bb_2022-04-11_14-49-30.png)

### 调试工具 vue_devtools

- vue 官方提供的 vue-devtools 调试工具，能够方便开发者对 vue 项目进行调试与开发。
- 安装地址：https://chrome.google.com/webstore/detail/vuejs-devtools/ljjemllljcmogpfapbkkighbhhppjdbg

#### Chrome 浏览器安装 vue 调试工具

- Chrome 网上应用商店搜索调试工具，并添加至 Chorme

![image-20220415015052573](http://zjp.hxkj.live/MDImage/Vue/Chrome%e6%b5%8f%e8%a7%88%e5%99%a8%e5%ae%89%e8%a3%85vue%e8%b0%83%e8%af%95%e5%b7%a5%e5%85%b7_2022-04-15_01-51-04.png)

- Chrome 浏览器打开开发者模式

![image-20220411104607586](http://zjp.hxkj.live/MDImage/Vue/Chrome%e6%b5%8f%e8%a7%88%e5%99%a8%e5%ae%89%e8%a3%85vue%e8%b0%83%e8%af%95%e5%b7%a5%e5%85%b7_2022-04-11_10-46-09.png)



- 插件 `Vue.js devtools` 打开详细，开启允许访问文件网址

![image-20220415015250931](http://zjp.hxkj.live/MDImage/Vue/Chrome%e6%b5%8f%e8%a7%88%e5%99%a8%e5%ae%89%e8%a3%85vue%e8%b0%83%e8%af%95%e5%b7%a5%e5%85%b7_2022-04-15_01-52-54.png)

#### 使用 vue-devtools 调试 vue 页面

- 在浏览器中访问一个使用了 vue 的页面，打开浏览器的开发者工具，切换到 Vue 面板，即可使用 vue-devtools
  调试当前的页面。
- 修改数据，对应的页面结构也会跟随改变，数据驱动视图。

![image-20220411145848819](http://zjp.hxkj.live/MDImage/Vue/%e4%bd%bf%e7%94%a8vue-devtools%e8%b0%83%e8%af%95vue%e9%a1%b5%e9%9d%a2_2022-04-11_14-58-58.png)



### 指令

- 指令（Directives）是 vue 为开发者提供的模板语法，用于辅助开发者渲染页面的基本结构。
- vue 中的指令按照不同的用途可以分为如下 6 大类：
  1. 内容渲染指令
  2. 属性绑定指令
  3. 事件绑定指令
  4. 双向绑定指令
  5. 条件渲染指令
  6. 列表渲染指令
- 注意：指令是 vue 开发中最基础、最常用、最简单的知识点。

#### 内容渲染指令

- 内容渲染指令用来辅助开发者渲染 DOM 元素的文本内容。常用的内容渲染指令有如下 3 个：
  1.  v-text
  2.  {{ }}
  3.  v-html

##### v-text 语法

- `v-text` 指令的缺点：会覆盖元素内部原有的内容！

- 用法示例：

```html
<!-- 把 username 对应的值，渲染到第一个 p 标签中 -->
<p v-text="username"></p>

<!-- 把 gender 对应的值，渲染到第二个 p 标签中 -->
<!-- 注意：第二个 p 标签中，默认的文本 "性别：" 会被 gender 的值覆盖掉 -->
<p v-text="gender">性别：</p>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <!-- 把 username 对应的值，渲染到第一个 p 标签中 -->
        <p v-text="username"></p>
        
        <!-- 把 gender 对应的值，渲染到第二个 p 标签中 -->
        <!-- 注意：第二个 p 标签中，默认的文本 "性别：" 会被 gender 的值覆盖掉 -->
        <p v-text="gender">性别：</p>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                username: 'zhangsan',
                gender: '男'
            }
        })
    </script>
</body>

</html>
```

![image-20220411154144921](http://zjp.hxkj.live/MDImage/Vue/v-text%e4%bd%bf%e7%94%a8%e7%a4%ba%e4%be%8b_2022-04-11_15-41-46.png)

##### {{ }} 语法(插值表达式)

- vue 提供的 {{ }} 语法，专门用来解决 v-text 会覆盖默认文本内容的问题。这种 {{ }} 语法的专业名称是插值表达式（英文名为：Mustache）。
- 注意：相对于 v-text 指令来说，插值表达式在开发中更常用一些！因为它不会覆盖元素中默认的文本内容。
- `{{ }}` 插值表达式：在实际开发中用的最多，只是内容的占位符，不会覆盖原有的内容！

- 用法示例：

```html
<!-- 使用 {{ }} 插值表达式，将对应的值渲染到元素的内容节点中 -->
<!-- 同时保留元素自身的默认值 -->
<p>姓名：{{ username }}</p>
<p>性别：{{ gender }}</p>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <!-- 使用 {{ }} 插值表达式，将对应的值渲染到元素的内容节点中 -->
        <!-- 同时保留元素自身的默认值 -->
        <p>姓名：{{ username }}</p>
        <p>性别：{{ gender }}</p>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                username: 'zhangsan',
                gender: '男'
            }
        })
    </script>
</body>

</html>
```

![image-20220411155134747](http://zjp.hxkj.live/MDImage/Vue/%e6%8f%92%e5%80%bc%e8%a1%a8%e8%be%be%e5%bc%8f%e4%bd%bf%e7%94%a8%e7%a4%ba%e4%be%8b_2022-04-11_15-51-45.png)

##### v-html 语法

- v-text 指令和插值表达式只能渲染纯文本内容。如果要把包含 HTML 标签的字符串渲染为页面的 HTML 元素，
  则需要用到 v-html 这个指令：
- `v-html` 指令的作用：可以把带有标签的字符串，渲染成真正的 HTML 内容

- 用法示例：

```html
<!-- 假设 data 中定义了名为 discription 的数据，数据的值包含 HTML 标签的字符串： -->
<!-- '<h5 style="color: red; font-weight: bold;">我在黑马程序员学习 vue.js</h5>' -->
<div v-html="discription"></div>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <!-- 假设 data 中定义了名为 discription 的数据，数据的值包含 HTML 标签的字符串： -->
        <!-- '<h5 style="color: red; font-weight: bold;">我在黑马程序员学习 vue.js</h5>' -->
        <div v-html="discription"></div>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                discription: '<h5 style="color: red; font-weight: bold;">我在黑马程序员学习 vue.js</h5>'
            }
        })
    </script>
</body>

</html>
```

![image-20220411163321779](http://zjp.hxkj.live/MDImage/Vue/v-html%e8%af%ad%e6%b3%95%e7%a4%ba%e4%be%8b_2022-04-11_16-33-30.png)

#### el 属性的使用注意项

- 一般 Vue 项目是使用一个 `<div id="app">`  标签来包裹项目进行接管所控制，无需修改该内容。`el: '#app'` 也无需修改。

#### 属性绑定指令

> 注意：插值表达式只能用在元素的**内容节点**中，不能用在元素的**属性节点**中！

- 如果需要为元素的属性动态绑定属性值，则需要用到 v-bind 属性绑定指令。用法示例如下：
- 在 vue 中，可以使用 `v-bind:` 指令，为元素的属性动态绑定值；
- 由于 v-bind 指令在开发中使用频率非常高，因此，vue 官方为其提供了简写形式（简写为英文的 : ）。
- 简写是英文的 `:`

```html
<!-- 假设有如下的 data 数据：
data: {
inputValue:'请输入内容',
imgSrc:'https://cn.vuejs.org/images/logo.svg'
} 
-->

<!-- 使用 v-bind 指令，为 input 的 placeholder 动态绑定属性值 -->
<input type="text" v-bind:placeholder="inputValue">
<br />
<!-- 使用 v-bind 指令，为 img 的 src 动态绑定属性值 -->
<img v-bind:src="imgSrc" alt="">
<!-- 简写 -->
<!-- <input type="text" :placeholder="inputValue"> -->
<!-- <img :src="imgSrc" alt=""> -->
```

- 使用示例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <!-- 使用 v-bind 指令，为 input 的 placeholder 动态绑定属性值 -->
        <input type="text" v-bind:placeholder="inputValue">
        <br />
        <!-- 使用 v-bind 指令，为 img 的 src 动态绑定属性值 -->
        <img v-bind:src="imgSrc" alt="">
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                inputValue: '请输入内容',
                imgSrc: 'https://cn.vuejs.org/images/logo.svg'
            }
        })
    </script>
</body>

</html>
```

![image-20220411165300209](http://zjp.hxkj.live/MDImage/Vue/v-bind%e8%af%ad%e6%b3%95%e7%a4%ba%e4%be%8b_2022-04-11_16-53-14.png)

#### 模板渲染语法中使用 Javascript 表达式

- 在 vue 提供的模板渲染语法中，除了支持绑定简单的数据值之外，还支持Javascript 表达式的运算，例如：
- 在使用 v-bind 属性绑定期间，如果绑定内容需要进行动态拼接，则字符串的外面应该包裹单引号

```html
{{ number +1 }}

{{ ok? 'YES' : 'NO' }}

{{ messgae.split('').reverse().join('') }}
<!-- 在使用 v-bind 属性绑定期间，如果绑定内容需要进行动态拼接，则字符串的外面应该包裹单引号 -->
<div v-bind:id="'list-' + id">
```

- 使用示例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <div>1 + 2 的结果是：{{ 1 + 2 }}</div>
        <div>{{ tips }} 反转的结果是：{{ tips.split('').reverse().join('') }}</div>
        <div :title="'box' + index">这是一个 div</div>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                tips: '请输入用户名',
                index: 3
            }
        })
    </script>
</body>

</html>
```

![image-20220411170813682](http://zjp.hxkj.live/MDImage/Vue/%e4%bd%bf%e7%94%a8js%e8%a1%a8%e8%be%be%e5%bc%8f_2022-04-11_17-08-22.png)

#### 事件绑定指令

- vue 提供了 v-on 事件绑定指令，用来辅助程序员为 DOM 元素绑定事件监听。语法格式如下：
- 注意：原生 DOM 对象有 onclick、oninput、onkeyup 等原生事件，替换为 vue 的事件绑定形式后，分别为：v-on:click、v-on:input、v-on:keyup

```html
<h3>count 的值是：{{ count }}</h3>
<!-- 语法格式为 v-on:事件名称="事件处理函数名称" -->
<button v-on:click="addCount">+1</button>
```

- 通过 v-on 绑定的事件处理函数，需要在 methods 节点中进行声明：

```javascript
const vm = new Vue({
    el: '#app',
    data: {
        count: 0,
    },
    // v-on 绑定的事件处理函数，需要声明在 methods 节点中
    methods: {
        // 事件处理函数的名字
        // addCount: function(){}
        // 简写
        addCount() {
            // this 表示当前 new 出来的 vm 实例对象
            // 通过 this 可以访问到 data 中的数据
            this.count += 1;
        }
    }
});
```

- 使用示例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <h3>count 的值是：{{ count }}</h3>
        <!-- 语法格式为 v-on:事件名称="事件处理函数名称" -->
        <button v-on:click="addCount">+1</button>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                count: 0,
            },
            // v-on 绑定的事件处理函数，需要声明在 methods 节点中
            methods: {
                // 事件处理函数的名字
                // addCount: function(){}
                // 简写
                addCount() {
                    // this 表示当前 new 出来的 vm 实例对象
                    // 通过 this 可以访问到 data 中的数据
                    this.count += 1;
                }
            }
        });
    </script>
</body>

</html>
```

- 在绑定事件处理函数的时候，可以使用 () 传递参数

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <h3>count 的值是：{{ count }}</h3>
        <!-- 语法格式为 v-on:事件名称="事件处理函数名称" -->
        <button v-on:click="addCount(2)">+2</button>
        <button v-on:click="subCount(subNum)">-{{subNum}}</button>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                count: 0,
                subNum: 3,
            },
            // v-on 绑定的事件处理函数，需要声明在 methods 节点中
            methods: {
                // 事件处理函数的名字
                // addCount: function(){}
                // 简写
                addCount(n) {
                    // this 表示当前 new 出来的 vm 实例对象
                    // 通过 this 可以访问到 data 中的数据
                    this.count += n;
                },
                subCount() {
                    this.count -= this.subNum;
                }
            }
        });
    </script>
</body>

</html>
```

- 由于 v-on 指令在开发中使用频率非常高，因此，vue 官方为其提供了简写形式（简写为英文的 @ ）
- `v-on:` 简写是 `@`

```html
<h3>count 的值是：{{ count }}</h3>
<!-- 完整写法 -->
<button v-on:click="addCount">+1</button>

<!-- 简写形式，把 v-on: 简写为 @ 符号 -->
<!-- 如果事件处理函数中的代码足够简单，只有一行代码，则可以简写到行内 -->
<button @click="count += 1">+1</button>
```

##### 事件处理函数传参和事件参数对象

- 在使用 v-on 指令绑定事件时，可以使用 ( ) 进行传参，示例代码如下：

- 在 v-on 指令（简写为 @ ）所绑定的事件处理函数中，同样可以接收到事件参数对象 event，示例代码如下：
- vue 提供了内置变量，名字叫做 $event，它就是原生 DOM 的事件对象 e
- $event 是 vue 提供的特殊变量，用来表示原生的事件参数对象 event。$event 可以解决事件参数对象 event 被覆盖的问题。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <h3>count 的值是：{{ count }}</h3>
        <!-- 仅传入自定义参数 -->
        <button @click="addCount1(1)">+1</button>
        
        <!-- 仅传入事件对象 -->
        <!-- <button @click="addCount2($event)">+2</button> -->
        <!-- 简写 -->
        <button @click="addCount2">+2</button>
        
        <!-- 同时传入事件对象和自定义参数 -->
        <button @click="addCount3(3, $event)">+3</button>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                count: 0,
            },
            methods: {
                addCount1(n) {
                    this.count += n;
                },
                addCount2(e) {
                    this.count += 2;
                    if (this.count % 2 === 0) {
                        e.target.style.backgroundColor = 'red';
                    }
                    else {
                        e.target.style.backgroundColor = '';
                    }
                },
                addCount3(n, e) {
                    this.count += n;
                    if (this.count % 2 === 0) {
                        e.target.style.backgroundColor = 'blue';
                    }
                    else {
                        e.target.style.backgroundColor = '';
                    }
                },
            }
        });
    </script>
</body>

</html>
```



##### 事件修饰符

- 在事件处理函数中调用event.preventDefault() 或 event.stopPropagation() 是非常常见的需求。因此，vue 提供了事件修饰符的概念，来辅助程序员更方便的对事件的触发进行控制。常用的 5 个事件修饰符如下：

![image-20220411182702001](http://zjp.hxkj.live/MDImage/Vue/%e4%ba%8b%e4%bb%b6%e4%bf%ae%e9%a5%b0%e7%ac%a6_2022-04-11_18-27-07.png)

- `.prevent` 用法示例：

```html
<!-- 触发 click 点击事件时，阻止 a 链接的默认跳转行为 -->
<a href="http://www.baidu.com" @click.prevent="show">百度首页</a>
```

- `.prevent` 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <!-- 触发 click 点击事件时，阻止 a 链接的默认跳转行为 -->
        <a href="http://www.baidu.com" @click.prevent="show">百度首页</a>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            methods: {
                show() {
                    console.log('点击了 a 链接')
                }
            },
        });
    </script>
</body>

</html>
```

- `.stop` 用法示例：

```html
<div style="height: 150px;background-color: orange;padding-left: 100px; line-height: 150px;"
     @click="divHandler">
    <!-- 触发 click 点击事件时，阻止 button 的冒泡行为 -->
    <button @click.stop="btnHandler">按钮</button>
</div>
```

- `.stop` 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <div style="height: 150px;background-color: orange;padding-left: 100px; line-height: 150px;"
            @click="divHandler">
            <!-- 触发 click 点击事件时，阻止 button 的冒泡行为 -->
            <button @click.stop="btnHandler">按钮</button>
        </div>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            methods: {
                divHandler() {
                    console.log('divHandler')
                },
                btnHandler() {
                    console.log('btnHandler')
                }
            },
        });
    </script>
</body>

</html>
```



##### 按键修饰符

- 在监听**键盘事件**时，我们经常需要判断详细的按键。此时，可以为键盘相关的事件添加按键修饰符 ，例如：

```html
<!-- 只有在 key 是 enter 时调用 vm.submit() -->
<input @keyup.enter='submit'>

<!-- 只有在 key 是 esc 时调用 vm.clearInput() -->
<input @keyup.esc='clearInput'>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <!-- 只有在 key 是 enter 时调用 vm.submit() -->
        <input @keyup.enter='submit'>

        <!-- 只有在 key 是 esc 时调用 vm.clearInput() -->
        <input @keyup.esc='clearInput'>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            methods: {
                submit(e) {
                    console.log(e.target.value);
                },
                clearInput(e) {
                    e.target.value = "";
                }
            },
        });
    </script>
</body>

</html>
```

#### 双向绑定指令

- vue 提供了 v-model 双向数据绑定指令，用来辅助开发者在不操作 DOM 的前提下，快速获取表单的数据。
- v-model 只用于表单元素，使得页面上的数据改动会影响到数据源上，从而重新渲染页面，双向的绑定。
- v-model 会自动识别表单元素的 type 类型，根据不同的 type 类型，设置不同属性。例如：`text` 设置 `value`，`checkbox` 设置 `check`
- input 输入框
  + type="radio"
  + type="checkbox"
  + type="xxxx"
- textarea
- select
- 用法示例：

```html
<p>用户的名字是：{{ username }}</p>
<!-- v-model 是双向的绑定，数据源的数据会同步到页面上，页面上的改动会同步到数据源上，而且 v-model 默认监听修改 value 值，无需使用 value 属性 -->
<input type="text" v-model="username">
<hr>
<!-- v-bind 是单向的绑定,数据源的数据会同步到页面上，页面上的改动不会同步到数据源上 -->
<input type="text" :value="username">
<hr>
<!-- div 标签属性绑定 v-model 没有意义，因为数据无法呈现和修改交互 -->
<!-- <div v-model="username">aa</div> -->
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <p>用户的名字是：{{ username }}</p>
        <!-- v-model 是双向的绑定，数据源的数据会同步到页面上，页面上的改动会同步到数据源上 -->
        <input type="text" v-model="username">
        <hr>
        <!-- v-bind 是单向的绑定,数据源的数据会同步到页面上，页面上的改动不会同步到数据源上 -->
        <input type="text" :value="username">
        <hr>
        <!-- div 标签属性绑定 v-model 没有意义，因为数据无法呈现和修改交互 -->
        <!-- <div v-model="username">aa</div> -->
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                username: 'zhangsan'
            },
        });
    </script>
</body>

</html>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <select v-model="city">
          <option value="">请选择城市</option>
          <option value="1">北京</option>
          <option value="2">上海</option>
          <option value="3">广州</option>
        </select>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                city: '2'
            },
        });
    </script>
</body>

</html>
```

##### v-model 修饰符

- 为了方便对用户输入的内容进行处理，vue 为 v-model 指令提供了 3 个修饰符，分别是：

![image-20220412054229036](http://zjp.hxkj.live/MDImage/Vue/v-model%e4%bf%ae%e9%a5%b0%e7%ac%a6_2022-04-12_05-42-37.png)

- 用法示例：

```html
<input type="text" v-model.number="n1">+
<input type="text" v-model.number="n2">=
<span>{{n1 + n2}}</span>
<hr>
<input type="text" v-model.trim="username">
<button @click="showName">获取用户名</button>
<hr>
<!-- 数据修改的时候不会立马同步到数据源，修改完毕再同步到数据源 -->
<input type="text" v-model.lazy="username">
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <input type="text" v-model.number="n1">+
        <input type="text" v-model.number="n2">=
        <span>{{n1 + n2}}</span>
        <hr>
        <input type="text" v-model.trim="username">
        <button @click="showName">获取用户名</button>
        <hr>
        <!-- 数据修改的时候不会立马同步到数据源，修改完毕再同步到数据源 -->
        <input type="text" v-model.lazy="username">
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                n1: '',
                n2: '',
                username: '',
            },
            methods: {
                showName() {
                    console.log(`"${this.username}"`);
                }
            },
        });
    </script>
</body>

</html>
```

#### 条件渲染指令

- 条件渲染指令用来辅助开发者按需控制 DOM 的显示与隐藏。条件渲染指令有如下两个，分别是：
  - v-if
  - v-show
- 用法示例：

```html
<!-- flag 可以使用布尔值，或者条件判断 -->
<!-- <p v-if="type === 'A'">这是被 v-if 控制的元素</p> -->
<p v-if="flag">这是被 v-if 控制的元素</p>
<p v-show="flag">这是被 v-show 控制的元素</p>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <p v-if="flag">这是被 v-if 控制的元素</p>
        <p v-show="flag">这是被 v-show 控制的元素</p>
        <button @click="click">改变条件</button>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                flag: true,
            },
            methods: {
                click() {
                    this.flag = !this.flag;
                }
            },
        });
    </script>
</body>

</html>
```

![image-20220412061602473](http://zjp.hxkj.live/MDImage/Vue/%e6%9d%a1%e4%bb%b6%e6%b8%b2%e6%9f%93%e6%8c%87%e4%bb%a4_2022-04-12_06-16-04.png)

##### v-if 和 v-show 的区别

> 在实际开发中，绝大多数情况，不用考虑性能问题，直接使用 v-if 就好了！！！

- 实现原理不同：
  - v-if 指令会动态地创建或移除DOM 元素，从而控制元素在页面上的显示与隐藏；
    - 如果刚进入页面的时候，某些元素默认不需要被展示，而且后期这个元素很可能也不需要被展示出来，此时 v-if 性能更好
  - v-show 指令会动态为元素添加或移除 style="display: none;" 样式，从而控制元素的显示与隐藏；
    - 如果要频繁的切换元素的显示状态，用 v-show 性能会更好

- 性能消耗不同：
  - v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此：
    - 如果需要非常频繁地切换，则使用 v-show 较好
    -  如果在运行时条件很少改变，则使用 v-if 较好

##### v-else

- v-if 可以单独使用，或配合 v-else 指令一起使用：
- 注意：v-else 指令必须配合 v-if 指令一起使用，否则它将不会被识别！
- 用法示例：

```html
<div v-if="type === 'A'">优秀</div>
<div v-else>不优秀</div>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <div v-if="type === 'A'">优秀</div>
        <div v-else>不优秀</div>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                type: 'B',
            },

        });
    </script>
</body>

</html>
```

##### v-else-if

- v-else-if 指令，顾名思义，充当 v-if 的“else-if 块”，可以连续使用：
- 注意：v-else-if 指令必须配合 v-if 指令一起使用，否则它将不会被识别！
- 用法示例：

```html
<div v-if="type === 'A'">优秀</div>
<div v-else-if="type === 'B'">良好</div>
<div v-else-if="type === 'C'">一般</div>
<div v-else>差</div>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <div v-if="type === 'A'">优秀</div>
        <div v-else-if="type === 'B'">良好</div>
        <div v-else-if="type === 'C'">一般</div>
        <div v-else>差</div>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                type: 'B',
            },

        });
    </script>
</body>

</html>
```

#### 列表渲染指令

- vue 提供了 v-for 列表渲染指令，用来辅助开发者基于一个数组来循环渲染一个列表结构。v-for 指令需要使用 item in items 形式的特殊语法，其中：
  - items 是待循环的数组
  - item 是被循环的每一项
- v-for 指令还支持一个可选的第二个参数，即当前项的索引。语法格式为 (item, index) in items，示例代码如下：
- 注意：v-for 指令中的 item 项和 index 索引都是形参，可以根据需要进行重命名。例如 (user, i) in userlist

- 用法示例：

``` javascript
data: {
    // 列表数据
    list: [{
        id: 1,
        name: 'zs'
    }, {
        id: 2,
        name: 'ls'
    }]
}
```

```html
<ul>
    <li v-for="item in list">姓名是：{{item.name}}</li>
</ul>
```

- 使用示例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./lib/bootstrap.css">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <table class="table table-bordered table-hover table-striped">
            <thead>
                <th>索引</th>
                <th>Id</th>
                <th>姓名</th>
            </thead>
            <tbody>
                <!-- 官方建议：只要用到了 v-for 指令，那么一定要绑定一个 :key 属性 -->
                <!-- 而且，尽量把 id 作为 key 的值 -->
                <!-- 官方对 key 的值类型，是有要求的：字符串或数字类型 -->
                <!-- key 的值是千万不能重复的，否则会终端报错：Duplicate keys detected -->
                <tr v-for="(item, index) in list" :title="item.id + item.name" :key="item.id">
                    <td>{{ index }}</td>
                    <td>{{ item.id }}</td>
                    <td>{{ item.name }}</td>
                </tr>
            </tbody>
        </table>
    </div>

    <script src="./lib/vue-2.6.12.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                // 列表数据
                list: [{
                    id: 1,
                    name: '张三'
                }, {
                    id: 2,
                    name: '李四'
                }, {
                    id: 3,
                    name: '王五'
                }, {
                    id: 4,
                    name: '张三'
                }, ]
            }
        })
    </script>
</body>

</html>
```

##### 使用 key 维护列表的状态

- 当列表的数据变化时，默认情况下，vue 会尽可能的复用已存在的DOM 元素，从而提升渲染的性能。但这种默认的性能优化策略，会导致有状态的列表无法被正确更新。
- 为了给 vue 一个提示，以便它能跟踪每个节点的身份，从而在保证有状态的列表被正确更新的前提下，提升渲染的性能。此时，需要为每项提供一个唯一的 key 属性：

```html
<ul>
    <!-- 加 key 属性的好处 -->
    <!-- 1. 正确维护列表的状态 -->
    <!-- 2. 复用现有的 DOM 元素，提升渲染的性能 -->
    <li v-for="user in userlist" :key="user.id">
        <input type="checkbox">
        姓名：{{user.name}}
    </li>
</ul>
```

- key 的注意事项
  - key 的值只能是字符串或数字类型
  - key 的值必须具有唯一性（即：key 的值不能重复）
  - 建议把数据项 id 属性的值作为 key 的值（因为 id 属性的值具有唯一性）
  - 使用 index 的值当作 key 的值没有任何意义（因为index 的值不具有唯一性）
  - 建议使用 v-for 指令时一定要指定 key 的值（既提升性能、又防止列表状态紊乱）

##### label 的 for 属性

- label 的 for 属性设置，会让选择文本也会操作对应 id 属性值相同的表单元素，提升用户体验

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <input type="checkbox" id="cb1">
    <label for="cb1">男</label>
    <hr>
    <input type="checkbox" id="cb2">
    <label for="cb2">女</label>
</body>

</html>
```





### axiois

> axios 是一个专注于网络请求的库

- 基本使用

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>

    <script src="./lib/axios.js"></script>
    <script>
        // http://www.liulongbin.top:3006/api/getbooks

        // 1. 调用 axios 方法得到的返回值是 Promise 对象
        axios({
            // 请求方式
            method: 'GET',
            // 请求的地址
            url: 'http://www.liulongbin.top:3006/api/getbooks',
            // URL 中的查询参数
            params: {
                id: 1
            },
            // 请求体参数
            data: {}
        }).then(function(result) {
            console.log(result)
        })
    </script>
</body>

</html>
```

![axios 封装的 6 个属性 - 副本](http://zjp.hxkj.live/MDImage/Vue/axios%e5%b0%81%e8%a3%85%e7%9a%846%e4%b8%aa%e5%b1%9e%e6%80%a7_2022-04-12_17-31-46.png)

#### 使用 await 和 async 和解构简写请求

- POST 请求

```javascript
document.querySelector('#btnPost').addEventListener('click', async function() {
    // 如果调用某个方法的返回值是 Promise 实例，则前面可以添加 await！
    // await 只能用在被 async “修饰”的方法中
    const {data} = await axios({
        method: 'POST',
        url: 'http://www.liulongbin.top:3006/api/post',
        data: {
            name: 'zs',
            age: 20
        }
    });

    console.log(data);
})
```

- GET 请求

```javascript
document.querySelector('#btnGet').addEventListener('click', async function() {
    // 解构赋值的时候，使用 : 进行重命名
    // 1. 调用 axios 之后，使用 async/await 进行简化
    // 2. 使用解构赋值，从 axios 封装的大对象中，把 data 属性解构出来
    // 3. 把解构出来的 data 属性，使用 冒号 进行重命名，一般都重命名为 { data: res }
    const {data: res} = await axios({
        method: 'GET',
        url: 'http://www.liulongbin.top:3006/api/getbooks',
        params: {
            id: 1
        },
    });

    console.log(res.data)
});
```

- `axios.get` 和 `axios.post`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <button id="btnGET">GET</button>
    <button id="btnPOST">POST</button>

    <script src="./lib/axios.js"></script>
    <script>
        document.querySelector('#btnGET').addEventListener('click', async function() {
            /* axios.get('url地址', {
              // GET 参数
              params: {}
            }) */

            const { data: res } = await axios.get('http://www.liulongbin.top:3006/api/getbooks', {
                params: {
                    id: 1
                }
            })
            console.log(res)
        })

        document.querySelector('#btnPOST').addEventListener('click', async function() {
            // axios.post('url', { /* POST 请求体数据 */ })
            const { data: res } = await axios.post('http://www.liulongbin.top:3006/api/post', {
                name: 'zs',
                gender: '女'
            })
            console.log(res)
        })
    </script>
</body>

</html>
```









## Vue组件

### 单页面应用程序

- 单页面应用程序（英文名：Single Page Application）简称 SPA，顾名思义，指的是一个 Web 网站中只有唯一的一个HTML 页面，所有的功能与交互都在这唯一的一个页面内完成。

- 例如资料中的这个 Demo 项目：

![image-20220412185249926](http://zjp.hxkj.live/MDImage/Vue/%e5%8d%95%e9%a1%b5%e9%9d%a2%e5%ba%94%e7%94%a8%e7%a8%8b%e5%ba%8f_2022-04-12_18-52-59.png)

![image-20220412185306814](http://zjp.hxkj.live/MDImage/Vue/%e5%8d%95%e9%a1%b5%e9%9d%a2%e5%ba%94%e7%94%a8%e7%a8%8b%e5%ba%8f_2022-04-12_18-53-08.png)



#### 单页面应用程序特点

- 单页面应用程序将所有的功能局限于一个 web 页面中，仅在该 web 页面初始化时加载相应的资源（ HTML、JavaScript 和 CSS）。
- 一旦页面加载完成了，SPA 不会因为用户的操作而进行页面的重新加载或跳转。而是利用 JavaScript 动态地变换HTML 的内容，从而实现页面与用户的交互。

#### 单页面应用程序优点

- SPA 单页面应用程序最显著的 3 个优点如下：
  1. 良好的交互体验
     - 单页应用的内容的改变不需要重新加载整个页面
     - 获取数据也是通过 Ajax 异步获取
     - 没有页面之间的跳转，不会出现“白屏现象”
  2. 良好的前后端工作分离模式
     - 后端专注于提供 API 接口，更易实现 API 接口的复用
     - 前端专注于页面的渲染，更利于前端工程化的发展
  3. 减轻服务器的压力
     - 服务器只提供数据，不负责页面的合成与逻辑的处理，吞吐能力会提高几倍

#### 页面应用程序的缺点

- 任何一种技术都有自己的局限性，对于 SPA 单页面应用程序来说，主要的缺点有如下两个：
  1. 首屏加载慢
     - 路由懒加载
     - 代码压缩
     - CDN 加速
     - 网络传输压缩
  2. 不利于 SEO
     - SSR 服务器端渲染



### 快速创建 SPA 项目

- vue 官方提供了两种快速创建工程化的 SPA 项目的方式：
  - 基于 vite 创建 SPA 项目
  - 基于 vue-cli 创建 SPA 项目

![image-20220415003025909](http://zjp.hxkj.live/MDImage/Vue/%e5%bf%ab%e9%80%9f%e5%88%9b%e5%bb%baSPA%e9%a1%b9%e7%9b%ae_2022-04-15_00-30-33.png)

### Vite

#### 创建 vite 的项目

- 按照顺序执行如下的命令，即可基于 vite 创建 vue 3.x 的工程化项目：
- 在目录下运行：

```bash
npm init vite-app 项目名称
# 示例
npm init vite-app test
```

- 如果第一次运行，需要 `y` 回车，安装 `create-vite-app`

```bash
y
```

- 进入项目根目录

```bash
cd test
```

- 安装依赖包

```bash
npm i
```

- 运行项目

```bash
npm run dev
```



#### 项目结构

- 使用 vite 创建的项目结构如下：

![image-20220415004632654](http://zjp.hxkj.live/MDImage/Vue/vite%e9%a1%b9%e7%9b%ae%e7%bb%93%e6%9e%84_2022-04-15_00-46-40.png)





- 在 src 这个项目源代码目录之下，包含了如下的文件和文件夹：

![image-20220415004813011](http://zjp.hxkj.live/MDImage/Vue/vite%e9%a1%b9%e7%9b%ae%e7%bb%93%e6%9e%84src_2022-04-15_00-48-17.png)

#### vite 项目的运行流程

- 在工程化的项目中，vue 要做的事情很单纯：通过 main.js 把 App.vue 渲染到 index.html 的指定区域中。
  - App.vue 用来编写待渲染的模板结构
  - index.html 中需要预留一个 el 区域
  - main.js 把 App.vue 渲染到了 index.html 所预留的区域中

##### 在 App.vue 中编写模板结构

- 清空 App.vue 的默认内容，并书写如下的模板结构：

```vue
<!-- /src/App.vue -->
<template>
  <h1>这是 App 根组件</h1>
</template>
```

##### 在 index.html 中预留 el 区域

- 打开 index.html 页面，确认预留了 el 区域：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vite App</title>
</head>

<body>
    <!-- id 为 app 的 div 元素，就是将来 vue 要控制的区域 -->
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script>
</body>

</html>
```

##### 在 main.js 中进行渲染

- 按照 vue 3.x 的标准用法，把 App.vue 中的模板内容渲染到 index.html 页面的 el 区域中：

```javascript
// 从 vue 中按需导入 createApp 函数
// creatApp 函数的作用：创建 vue 的"单页面应用程序实例"
import { createApp } from 'vue'
// 导入待渲染的 App 组件
import App from './App.vue'
// import './index.css'

// 调用 createApp() 函数，返回值是"单页面应用程序的实例"
// 同时把 App 组件作为参数传给 createApp 函数，表示要把 App 渲染到 index.html 页面上
// 调用 mount() 方法，用来指定 vue 实际要控制的区域
createApp(App).mount('#app')
```





### 组件化开发

- 组件化开发指的是：根据封装的思想，把页面上可重用的部分封装为组件，从而方便项目的开发和维护。
- 方式，快速生成一个页面的布局结构。例如：http://www.ibootstrap.cn/ 所展示的效果，就契合了组件化开发的思想。用户可以通过拖拽组件的

#### 组件化开发的好处

- 前端组件化开发的好处主要体现在以下两方面：
  - 提高了前端代码的复用性和灵活性
  - 提升了开发效率和后期的可维护性



#### vue 中的组件化开发

- vue 是一个完全支持组件化开发的框架。vue 中规定组件的后缀名是 .vue。之前接触到的 App.vue 文件本质上就是一个 vue 的组件。



#### vue 组件组成结构

- 每个 .vue 组件都由 3 部分构成，分别是：
  1. template -> 组件的**模板结构**
  2. script -> 组件的 **JavaScript 行为**
  3. style -> 组件的**样式**

- 其中，**每个组件中必须包含 template 模板结构**，而 **script 行为**和 **style 样式**是**可选**的组成部分。



#### 组件的 template 节点

- vue 规定：每个组件对应的模板结构，需要定义到 `<template>` 节点中。
- 注意
  - `<template>` 是 vue 提供的容器标签，只起到包裹性质的作用，它不会被渲染为真正的 DOM 元素

```vue
<template>
  <!-- 当前组件的 DOM 结构，需要定义到 template 标签内部 -->
</template>
```

##### 在 template 中使用指令

- 在组件的 `<template>` 节点中，支持使用指令语法，来辅助开发者渲染当前组件的DOM 结构。代码示例如下：
- 支持在  `<template>` 节点中定义多个根节点

```vue
<!-- /src/App.vue -->
<template>
  <h1>这是 App 根组件</h1>
  <!-- 使用 {{}} 插值表达式 -->
  <p>生成一个随机数字：{{ (Math.random() * 10).toFixed(2) }}</p>
  <!-- 使用 v-bind 属性绑定 -->
  <p :title="new Date().toLocaleTimeString()">我在黑马程序员学习</p>
  <!-- 属性 v-on 事件绑定 -->
  <button @click="showInfo">按钮</button>
</template>
```

#### 组件的 script 节点

- vue 规定：组件内的 `<script>` 节点是可选的，开发者可以在 `<script>` 节点中封装组件的 JavaScript 业务逻辑。`<script>` 节点的基本结构如下：

```vue
<script>
// 今后，组件相关的 data 数据、methods 方法等
// 都需要定义到 export default 所导出的对象中
export default {

};
</script>
```

##### script 中的 name 节点

- 可以通过 name 节点为当前组件定义一个名称：
- 作用：在使用 vue-devtools 进行项目调试的时候，自定义的组件名称可以清晰的区分每个组件：

```vue
<script>
export default {
  // name 属性指向的是当前组件的名称（建议：每个单词的首字母大写）
  name: "MyApp",
};
</script>
```

![image-20220415015541377](http://zjp.hxkj.live/MDImage/Vue/script%e8%8a%82%e7%82%b9%e4%b8%adname%e5%b1%9e%e6%80%a7%e7%9a%84%e4%bd%9c%e7%94%a8_2022-04-15_01-56-02.png)

##### script 中的 data 节点

- vue 组件渲染期间需要用到的数据，可以定义在data 节点中：
- vue 规定：组件中的 data 必须是一个函数，不能直接指向一个数据对象。

```vue
<script>
export default {
  // 组件的名称
  name: "MyApp",
  // 组件的数据（data 方法中 return 出去的对象，就是当前组件渲染期间需要用到的数据对象）
  data() {
    return {
      username: "娃哈哈",
    };
  },
};
</script>
```



##### script 中的 methods 节点

- 组件中的事件处理函数，必须定义到 methods 节点中，示例代码如下：

```vue
<script>
export default {
  // 组件的名称
  name: "MyApp",
  // 组件的数据
  data() {
    return {
      count: 0,
    };
  },
  // 处理函数
  methods: {
    addCount() {
      this.count++;
    },
  },
};
</script>
```



#### 组件的 style 节点

- vue 规定：组件内的 `<style>` 节点是可选的，开发者可以在 `<style>` 节点中编写样式美化当前组件的 UI 结构。`<script>` 节点的基本结构如下：
- 其中 `<style>` 标签上的 `lang="css"` 属性是可选的，它表示所使用的样式语言。默认只支持普通的 css 语法，可选值还有 less、scss 等。

```vue
<style lang="css">
h1 {
  font-weight: normal;
}
</style>
```

​	

##### 让 style 中支持 less 语法

- 如果希望使用 less 语法编写组件的 style 样式，可以按照如下两个步骤进行配置：

- 运行 `npm install less -D` 命令安装依赖包，从而提供 less 语法的编译支持

```bash
npm install less -D
```

- 在 `<style>` 标签上添加 lang="less" 属性，即可使用 less 语法编写组件的样式

```vue
<style lang="less">
h1 {
  color: red;
  i {
    color: blue;
  }
}
</style>
```



### 组件的基本使用

- 组件之间可以进行相互的引用，例如：
- vue 中组件的引用原则：先注册后使用。

![image-20220415100339261](http://zjp.hxkj.live/MDImage/Vue/%e7%bb%84%e4%bb%b6%e9%97%b4%e7%9b%b8%e4%ba%92%e5%bc%95%e7%94%a8_2022-04-15_10-03-49.png)



#### 注册组件的两种方式

- vue 中注册组件的方式分为“全局注册”和“局部注册”两种，其中：
  - 被全局注册的组件，可以在全局任何一个组件内使用
  - 被局部注册的组件，只能在当前注册的范围内使用

![image-20220415100522718](http://zjp.hxkj.live/MDImage/Vue/%e5%85%a8%e5%b1%80%e6%b3%a8%e5%86%8c%e7%bb%84%e4%bb%b6_2022-04-15_10-05-28.png)

![image-20220415100536387](http://zjp.hxkj.live/MDImage/Vue/%e5%b1%80%e9%83%a8%e6%b3%a8%e5%86%8c%e7%bb%84%e4%bb%b6_2022-04-15_10-05-41.png)



#### 全局注册组件

##### 定义全局组件

```vue
<!-- /components/MySwiper.vue -->
<template>
  <!-- 撰写组件功能 -->
  <h3>MySwiper</h3>
</template>

<script>
export default {
  // 设置 name 组件名
  name: "MySwiper",
};
</script>
```



##### 全局注册组件

```javascript
// /src/main.js
import { createApp } from 'vue'
import App from './App.vue'
// import './index.css'
// 导入 Swiper 组件
import Swiper from './components/MySwiper.vue'

const app = createApp(App)

// 调用 app 实例的 component() 方法，在全局注册 MySwiper 组件
app.component('MySwiper', Swiper)



app.mount('#app')
```



##### 使用全局注册组件

- 使用 app.component() 方法注册的全局组件，直接以标签的形式进行使用即可，例如：

```vue
<!-- /src/App.vue -->
<template>
  <!-- 使用全局注册组件 -->
  <MySwiper></MySwiper>
</template>
```



#### 局部注册组件

##### 定义局部组件

```vue
<!-- /components/MySearch.vue -->
<template>
  <!-- 撰写组件功能 -->
  <h3>MySearch</h3>
</template>

<script>
export default {
  // 设置 name 组件名
  name: "MySearch",
};
</script>
```

##### 局部注册组件

```vue
<template>
  <!-- 使用局部注册组件 -->
  <MySearch></MySearch>
</template>

<script>
// 导入 Search 组件
import Search from "./components/MySearch.vue";

export default {
  name: "App",
  // 通过 components 节点，为当前的组件注册私有子组件
  components: {
    "MySearch": Search,
  },
};
</script>
```

#### 全局注册和局部注册的区别

- 被全局注册的组件，可以在全局任何一个组件内使用
- 被局部注册的组件，只能在当前注册的范围内使用

- 应用场景
  - 如果某些组件在开发期间的使用频率很高，推荐进行全局注册；
  - 如果某些组件只在特定的情况下会被用到，推荐进行局部注册。



#### 组件注册时名称的大小写

- 在进行组件的注册时，定义组件注册名称的方式有两种：
  1. 使用 kebab-case 命名法（俗称短横线命名法，例如 my-swiper 和 my-search）
  2. 使用 PascalCase 命名法（俗称帕斯卡命名法或大驼峰命名法，例如 MySwiper 和 MySearch）

- 短横线命名法的特点：
  - 必须严格按照短横线名称进行使用
- 帕斯卡命名法的特点：
  - 既可以严格按照帕斯卡名称进行使用，又可以转化为短横线名称进行使用

- 注意：在实际开发中，推荐使用帕斯卡命名法为组件注册名称，因为它的适用性更强



#### 通过 name 属性注册组件

- 在注册组件期间，除了可以直接提供组件的注册名称之外，还可以把组件的 name 属性作为注册后组件的名称，示例代码如下：

```javascript
import { createApp } from 'vue'
import App from './App.vue'
// import './index.css'
// 导入 Swiper 组件
import Swiper from './components/MySwiper.vue'

const app = createApp(App)

// 调用 app 实例的 component() 方法，在全局注册 my-swiper 组件
// 使用组件的 name 属性作为注册后组件的名称
app.component(Swiper.name, Swiper)

app.mount('#app')
```



```vue
<template>
  <!-- 使用局部注册组件 -->
  <Search></Search>
</template>

<script>
// 导入 Search 组件
import Search from "./components/MySearch.vue";

export default {
  name: "App",
  // 通过 components 节点，为当前的组件注册私有子组件
  components: {
    Search,
  },
};
</script>
```



### 组件之间的样式冲突问题

- 默认情况下，写在 .vue 组件中的样式会全局生效，因此很容易造成多个组件之间的样式冲突问题。导致组件之间样式冲突的根本原因是：
  - 单页面应用程序中，所有组件的 DOM 结构，都是基于唯一的 index.html 页面进行呈现的
  - 每个组件中的样式，都会影响整个 index.html 页面中的 DOM 元素
- 解决方案原理：为每个组件分配唯一的自定义属性，在编写组件样式时，通过属性选择器来控制样式的作用域，示例代码如下：

```vue
<template>
  <!-- 赋予标签属性，用于样式属性选择器过滤 -->
  <h3 data-v-001>当前组件内容</h3>
  <Search></Search>
</template>

<script>
import Search from "./components/MySearch.vue";
export default {
  name: "App",
  components: {
    Search,
  },
};
</script>

<style>
/* 通过中括号"属性选择器"，来防止组件之间的样式冲突问题，因为每个组件分配的自定义属性是"唯一的" */
h3[data-v-001] {
  color: red;
}
</style>
```



#### style 节点的 scoped 属性

- 为了提高开发效率和开发体验，vue 为 style 节点提供了 scoped 属性，从而防止组件之间的样式冲突问题：

```vue
<template>
  <div>
    <h3>当前组件内容</h3>
    <Search></Search>
    <MySwiper></MySwiper>
  </div>
</template>

<script>
import Search from "./components/MySearch.vue";
export default {
  name: "App",
  components: {
    Search,
  },
};
</script>

<style lang="less" scoped>
/* style 节点 scoped 属性，用来自动为每一个组件分配唯一的"自定义属性",
   并自动为当前组件的 DOM 标签和 style 标签应用这个自定义属性，防止组件的样式冲突问题 */
h3 {
  color: red;
}
</style>

```

- 注意：scoped 属性会为当前组件的所有 DOM 标签以及子组件的第一层级标签添加"自定义属性"。
- 开发中为防止组件样式冲突，style 节点都必须加 scoped 属性。



#### :deep() 样式穿透

- 如果给当前组件的 style 节点添加了 scoped 属性，则当前组件的样式对其子组件是不生效的。如果想让某些样式对子组件生效，可以使用 :deep() 深度选择器。

```vue
<style lang="less" scoped>
/* 样式穿透，对子组件的样式进行影响 */
:deep(h3) {
  color: red;
}
</style>
```



### 组件的 props

- 为了提高组件的复用性，在封装 vue 组件时需要遵守如下的原则：
  - 组件的 DOM 结构、Style 样式要尽量复用
  - 组件中要展示的数据，尽量由组件的使用者提供
- 为了方便使用者为组件提供要展示的数据，vue 组件提供了 props 的概念。

- props 是组件的自定义属性，组件的使用者可以通过 props 把数据传递到子组件内部，供子组件内部进行使用。代码示例如下：

```vue
</template>
    <!-- 通过自定义 props，把文章的标题和作者，传递到 MyArticle 组件中 -->
    <!-- 传递两个自定义属性 -->
    <MyArticle title="面朝大海，春暖花开" author="海子"></MyArticle>
</template>
```

- props 的作用：父组件通过 props 向子组件传递要展示的数据。
- props 的好处：提高了组件的复用性。

#### 在组件中声明 props

- 在封装 vue 组件时，可以把动态的数据项声明为 props 自定义属性。自定义属性可以在当前组件的模板结构中被直接使用。示例代码如下：

```vue
<template>
  <div>
    <h3>标题{{ title }}</h3>
    <h5>作者{{ author }}</h5>
  </div>
</template>

<script>
export default {
  name: "Article",
  // 外界可以传递指定的数据，到当前的组件中
  // 父组件传递给 MyArticle 组件的数据，必须在 props 节点中声明
  props: ["title", "author"],
};
</script>

<style lang="less" scoped>
</style>
```



```vue
<template>
  <div>
    <!-- 通过自定义 props，把文章的标题和作者，传递到 MyArticle 组件中 -->
    <!-- 传递两个自定义属性 -->
    <Article title="面朝大海，春暖花开" author="海子"></Article>
  </div>
</template>

<script>
import Article from "./components/Article.vue";
export default {
  name: "App",
  components: {
    Article,
  },
};
</script>

<style lang="less" scoped>
</style>
```



#### 无法使用未声明的 props

- 如果父组件给子组件传递了未声明的 props 属性，则这些属性会被忽略，无法被子组件使用，示例代码如下：

```vue
<template>
  <div>
    <h3>标题:{{ title }}</h3>
    <h5>作者:{{ author }}</h5>
  </div>
</template>


<script>
export default {
  name: "Article",
  // author 属性没有声明，因此子组件中无法访问到 author 的值
  props: ["title"],
};
</script>

<style lang="less" scoped>
</style>
```



#### 动态绑定 props 的值

- 可以使用 v-bind 属性绑定的形式，为组件动态绑定 props 的值，示例代码如下：

```vue
<template>
  <div>
    <!-- 通过 v-bind 属性绑定，为 title 动态赋予一个变量的值 -->
    <!-- 通过 v-bind 属性绑定，为 author 动态赋予一个表达式的值 -->
    <Article :title="info.title" :author="info.author"></Article>
  </div>
</template>

<script>
import Article from "./components/Article.vue";
export default {
  name: "App",
  components: {
    Article,
  },
  data() {
    return {
      info: {
        title: "abc",
        author: "123",
      },
    };
  },
};
</script>

<style lang="less" scoped>
</style>
```



#### props 的大小写命名

- 组件中如果使用“camelCase(驼峰命名法)”声明了 props 属性的名称，则有两种方式为其绑定属性的值：

```vue
<template>
  <div>
    <h3>标题:{{ myTitle }}</h3>
    <h5>作者:{{ myAuthor }}</h5>
  </div>
</template>


<script>
export default {
  name: "Article",
  // 采用"驼峰命名法"为当前的组件声明了属性
  props: ["myTitle", "myAuthor"],
};
</script>

<style lang="less" scoped>
</style>
```



```vue
<template>
  <div>
    <!-- 既可以直接使用"驼峰命名法"的形式为组件绑定属性的值 -->
    <!-- 也可以使用其等价的"短横线分割命名"的形式为组件绑定属性的值 -->
    <Article :myTitle="info.title" :my-author="info.author"></Article>
  </div>
</template>

<script>
import Article from "./components/Article.vue";
export default {
  name: "App",
  components: {
    Article,
  },
  data() {
    return {
      info: {
        title: "abc",
        author: "123",
      },
    };
  },
};
</script>

<style lang="less" scoped>
</style>
```





### Class 与 Style 绑定

- 在实际开发中经常会遇到动态操作元素样式的需求。因此，vue 允许开发者通过 v-bind 属性绑定指令，为元素动态绑定 class 属性的值和行内的 style 样式。



#### 动态绑定 HTML 的 class

- 可以通过三元表达式，动态的为元素绑定class 的类名。示例代码如下：

```vue
<!-- components/Style.vue -->
<template>
  <h3 class="thin" :class="isItalic ? 'italic' : ''">Style 组件</h3>
  <button @click="isItalic = !isItalic">Toggle Italic</button>
</template>

<script>
export default {
  name: "Style",
  data() {
    return {
      isItalic: false,
    };
  },
};
</script>

<style lang="less" scoped>
// 字体变细
.thin {
  font-weight: 200;
}

// 倾斜字体
.italic {
  font-style: italic;
}
</style>
```



#### 以数组语法绑定 HTML 的 class

- 如果元素需要动态绑定多个 class 的类名，此时可以使用数组的语法格式：

```vue
<!-- components/Style.vue -->
<template>
  <h3
    class="thin"
    :class="[isItalic ? 'italic' : '', isDelete ? 'delete' : '']"
  >
    Style 组件
  </h3>
  <button @click="isItalic = !isItalic">Toggle Italic</button>
  <button @click="isDelete = !isDelete">Toggle Delete</button>
</template>

<script>
export default {
  name: "Style",
  data() {
    return {
      isItalic: false,
      isDelete: false,
    };
  },
};
</script>

<style lang="less" scoped>
// 字体变细
.thin {
  font-weight: 200;
}

// 倾斜字体
.italic {
  font-style: italic;
}

.delete {
  text-decoration: line-through;
}
</style>
```



#### 以对象语法绑定 HTML 的 class

- 使用数组语法动态绑定class 会导致模板结构臃肿的问题。此时可以使用对象语法进行简化：

```vue
<!-- components/Style.vue -->
<template>
  <h3 class="thin" :class="ClassObj">Style 组件</h3>
  <button @click="ClassObj.italic = !ClassObj.italic">Toggle Italic</button>
  <button @click="ClassObj.delete = !ClassObj.delete">Toggle Delete</button>
</template>

<script>
export default {
  name: "Style",
  data() {
    return {
      // 对象中，属性是 class 类名，值是布尔值
      ClassObj: {
        italic: false,
        delete: false,
      },
    };
  },
};
</script>

<style lang="less" scoped>
// 字体变细
.thin {
  font-weight: 200;
}

// 倾斜字体
.italic {
  font-style: italic;
}

.delete {
  text-decoration: line-through;
}
</style>
```



#### 以对象语法绑定内联的 style

- :style 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。CSS property 名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名

```vue
<!-- components/Style.vue -->
<template>
  <div
    :style="{
      color: active,
      fontSize: fsize + 'px',
      'background-color': bgcolor,
    }"
  >
    黑马程序员
  </div>
  <button @click="fsize += 1">字号 +1</button>
  <button @click="fsize -= 1">字号 -1</button>
</template>

<script>
export default {
  name: "Style",
  data() {
    return {
      // 高亮时的文本颜色
      active: "red",
      // 文字的大小
      fsize: 30,
      // 背景颜色
      bgcolor: "pink",
    };
  },
};
</script>

<style lang="less" scoped>
</style>
```



### 封装组件的案例

![image-20220418105516633](http://zjp.hxkj.live/MDImage/Vue/%e5%b0%81%e8%a3%85%e7%bb%84%e4%bb%b6%e7%9a%84%e6%a1%88%e4%be%8b_2022-04-18_10-55-22.png)

- 封装要求
  - 允许用户自定义 title 标题
  - 允许用户自定义 bgcolor 背景色
  - 允许用户自定义 color 文本颜色
  - MyHeader 组件需要在页面顶部进行 fixed 固定定位，且 z-index 等于 999
- 使用示例

```vue
<template>
  <MyHeader title="黑马程序员" bgcolor="#000" color="#f8f8f8"></MyHeader>
</template>
```

```vue
<!-- /components/MyHeader.vue -->
<template>
  <div
    class="header-container"
    :style="{ backgroundColor: bgcolor, color: color }"
  >
    {{ title || "Header组件" }}
  </div>
</template>

<script>
export default {
  name: "MyHeader",
  props: ["title", "bgcolor", "color"],
};
</script>

<style lang="less" scoped>
.header-container {
  height: 45px;
  background-color: pink;
  text-align: center;
  line-height: 45px;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 999;
}
</style>
```



```vue
<!-- /App.vue -->
<template>
  <div class="app-container">
    <MyHeader title="黑马程序员" bgcolor="#000" color="#f8f8f8"></MyHeader>
  </div>
</template> 

<script>
import MyHeader from "./components/MyHeader.vue";
export default {
  name: "App",
  components: {
    MyHeader,
  },
  data() {
    return {};
  },
};
</script>

<style lang="less" scoped>
.app-container {
  margin-top: 45px;
}
</style>
```



### props 验证

- 指的是：在封装组件时对外界传递过来的props 数据进行合法性的校验，从而防止数据不合法的问题。

![image-20220418112140434](http://zjp.hxkj.live/MDImage/Vue/props%e9%aa%8c%e8%af%81_2022-04-18_11-21-46.png)

- 使用数组类型的 props 节点的缺点：无法为每个 prop 指定具体的数据类型。



#### 对象类型的 props 节点

- 使用对象类型的 props 节点，可以对每个 prop 进行数据类型的校验，示意图如下：

![image-20220418112458026](http://zjp.hxkj.live/MDImage/Vue/props%e5%af%b9%e8%b1%a1%e7%b1%bb%e5%9e%8b_2022-04-18_11-25-08.png)

- 代码

```vue
<!-- /components/Count.vue -->
<template>
  <div>
    <p>数量：{{ count }}</p>
    <p>状态：{{ state }}</p>
  </div>
</template>

<script>
export default {
  name: "MyCount",
  props: {
    count: Number,
    state: Boolean,
  },
};
</script>

<style lang="less" scoped>
</style>
```



#### props 验证

- 对象类型的 props 节点提供了多种数据验证方案，例如：
  - 基础的类型检查
  - 多个可能的类型
  - 必填项校验
  - 属性默认值
  - 自定义验证函数



##### 基础的类型检查

- 可以直接为组件的 prop 属性指定基础的校验类型，从而防止组件的使用者为其绑定错误类型的数据：

```vue
<script>
export default {
  props: { // 支持 8 种基础类型
    propA: String, // 字符串类型
    propB: Number, // 数字类型
    propC: Boolean, // 布尔值类型
    propD: Array, // 数组类型
    propE: Object, // 对象类型
    propF: Date, // 日期类型
    propG: Function, // 函数类型
    propH: Symbol, // 符号类型
  },
};
</script>
```



##### 多个可能的类型

- 如果某个 prop 属性值的类型不唯一，此时可以通过数组的形式，为其指定多个可能的类型，示例代码如下：

```vue
<script>
export default {
  props: {
    // propA 属性值可以是"字符串"或者"数字"
    propA: [String, Number],
  },
};
</script>
```



##### 必填项校验

- 如果组件的某个 prop 属性是必填项，必须让组件的使用者为其传递属性的值。此时，可以通过如下的方式将其设置为必填项：

```vue
<script>
export default {
  props: {
    // 通过"配置对象"的形式，来定义 propA 属性的验证规则
    propA: {
      type: String, // 当前属性的值必须是 String 字符串类型
      required: true, // 当前属性的值是必须项，如果使用者没指定 propA 属性的值，则在终端进行警告提示
    },
  },
};
</script>
```



##### 属性默认值

- 在封装组件时，可以为某个 prop 属性指定默认值。示例代码如下：

```vue
<script>
export default {
  props: {
    // 通过"配置对象"的形式，来定义 propA 属性的验证规则
    propA: {
      type: Number,
      default: 100, // 如果使用者没有指定 propA 的值，则 propA 属性的默认值为 100
    },
  },
};
</script>
```



##### 自定义验证函数

- 在封装组件时，可以为prop 属性指定自定义的验证函数，从而对 prop 属性的值进行更加精确的控制：

```vue
<script>
export default {
  props: {
    // 通过"配置对象"的形式，来定义 propA 属性的验证规则
    propA: {
      default: 100,
      // 通过 validator 函数，对 propA 属性的值进行校验，"属性的值"可以通过形参 value 进行接收
      validator(value) {
        // validator 函数的返回值为 true 表示验证通过，false 表示验证失败
        if (value >= 100) {
          return true;
        } else {
          return false;
        }
      },
    },
  },
};
</script>
```



### 计算属性

- 计算属性本质上就是一个 function 函数，它可以实时监听 data 中数据的变化，并 return 一个计算后的新值，供组件渲染 DOM 时使用。
- 计算属性需要以 function 函数的形式声明到组件的 computed 选项中，示例代码如下：
- 注意：计算属性侧重于得到一个计算的结果，因此计算属性中必须有 return 返回值！

```vue
<!-- /components/Count.vue -->
<template>
  <div>
    <input type="text" v-model.number="count" />
    <p>{{ count }} 乘以 2 的值为：{{ plus }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 1,
    };
  },
  computed: {
    plus() {
      return this.count * 2;
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```

- 注意：
  1. 计算属性必须定义在 computed 节点中
  2. 计算属性必须是一个 function 函数
  3. 计算属性必须有返回值
  4. 计算属性必须当做普通属性使用

#### 计算属性 vs 方法

- 相对于方法来说，计算属性会缓存计算的结果，只有计算属性的依赖项发生变化时，才会重新进行运算。因此计算属性的性能更好：
- 方法

```vue
<!-- /components/Count.vue -->
<template>
  <div>
    <input type="text" v-model.number="count" />
    <!-- 方法会被调用三遍 -->
    <p>{{ count }} 乘以 2 的值为：{{ plus() }}</p>
    <p>{{ count }} 乘以 2 的值为：{{ plus() }}</p>
    <p>{{ count }} 乘以 2 的值为：{{ plus() }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 1,
    };
  },
  //   computed: {
  //     plus() {
  //       console.log("计算属性被调用了");
  //       return this.count * 2;
  //     },
  //   },
  methods: {
    plus() {
      console.log("方法被调用了");
      return this.count * 2;
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```

- 计算属性

```vue
<!-- /components/Count.vue -->
<template>
  <div>
    <input type="text" v-model.number="count" />
    <!-- 计算属性会被调用一遍 -->
    <p>{{ count }} 乘以 2 的值为：{{ plus }}</p>
    <p>{{ count }} 乘以 2 的值为：{{ plus }}</p>
    <p>{{ count }} 乘以 2 的值为：{{ plus }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 1,
    };
  },
  computed: {
    plus() {
      console.log("计算属性被调用了");
      return this.count * 2;
    },
  },
  //   methods: {
  //     plus() {
  //       console.log("方法被调用了");
  //       return this.count * 2;
  //     },
  //   },
};
</script>

<style lang="less" scoped>
</style>
```



### 自定义事件

- 在封装组件时，为了让组件的使用者可以监听到组件内状态的变化，此时需要用到组件的自定义事件。

![image-20220418175804981](http://zjp.hxkj.live/MDImage/Vue/%e8%87%aa%e5%ae%9a%e4%b9%89%e4%ba%8b%e4%bb%b6_2022-04-18_17-58-10.png)

- 自定义事件的 3 个使用步骤

  - 在封装组件时：
    1. 声明自定义事件
    2. 触发自定义事件

  - 在使用组件时：
    1. 监听自定义事件

#### 声明自定义事件

- 开发者为自定义组件封装的自定义事件，必须事先在 emits 节点中声明，示例代码如下：

```vue
<script>
export default {
  // Count 组件的自定义事件，必须事先声明到 emits 节点中
  emits: ["change"],
};
</script>
```

#### 触发自定义事件

- 在 emits 节点下声明的自定义事件，可以通过 this.$emit('自定义事件的名称') 方法进行触发，示例代码如下：

```vue
<!-- /components/Count.vue -->
<template>
  <div>
    <button @click="onBtnClick">+1</button>
  </div>
</template>

<script>
export default {
  // Count 组件的自定义事件，必须事先声明到 emits 节点中
  emits: ["change"],
  methods: {
    onBtnClick() {
      // 当点击 +1 按钮时，调用 this.$emit() 方法，触发自定义的 change 事件
      this.$emit("change");
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```



#### 监听自定义事件

- 在使用自定义的组件时，可以通过 v-on 的形式监听自定义事件。示例代码如下：

```vue
<!-- /components/Count.vue -->
<template>
  <div>
    <button @click="onBtnClick">+1</button>
    <p>{{ number }}</p>
  </div>
</template>

<script>
export default {
  name: "Count",
  // Count 组件的自定义事件，必须事先声明到 emits 节点中
  emits: ["change"],
  data() {
    return {
      number: 0,
    };
  },
  methods: {
    onBtnClick() {
      this.number += 1;
      // 当点击 +1 按钮时，调用 this.$emit() 方法，触发自定义的 change 事件
      this.$emit("change");
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```



```vue
<!-- /App.vue -->
<template>
  <div>
    <Count @change="getCount"></Count>
  </div>
</template> 

<script>
import Count from "./components/Count.vue";
export default {
  name: "App",
  components: {
    Count,
  },
  methods: {
    getCount() {
      console.log("监听到了 count 值的变化");
    },
  },
};
</script>

<style lang="less" scoped>
</style>

```



#### 自定义事件传参

- 在调用 this.$emit() 方法触发自定义事件时，可以通过第2 个参数为自定义事件传参，示例代码如下：

```vue
<!-- /components/Count.vue -->
<template>
  <div>
    <button @click="onBtnClick">+1</button>
    <p>{{ number }}</p>
  </div>
</template>

<script>
export default {
  name: "Count",
  // Count 组件的自定义事件，必须事先声明到 emits 节点中
  emits: ["change"],
  data() {
    return {
      number: 0,
    };
  },
  methods: {
    onBtnClick() {
      this.number += 1;
      // 触发自定义事件时，通过第二个参数传参
      this.$emit("change", this.number);
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```



```vue
<!-- /App.vue -->
<template>
  <div>
    <Count @change="getCount"></Count>
  </div>
</template> 

<script>
import Count from "./components/Count.vue";
export default {
  name: "App",
  components: {
    Count,
  },
  methods: {
    // 子组件参数传递过来，到 val 中
    getCount(val) {
      console.log("监听到了 count 值的变化,数值为：" + val);
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```



### 组件上的 v-model

- v-model 是双向数据绑定指令，当需要维护组件内外数据的同步时，可以在组件上使用 v-model 指令。示意图如下：
- 外界数据的变化会自动同步到 counter 组件中
- counter 组件中数据的变化，也会自动同步到外界

![image-20220418192906733](http://zjp.hxkj.live/MDImage/Vue/%e7%bb%84%e4%bb%b6%e4%b8%8a%e7%9a%84v-model_2022-04-18_19-29-14.png)

#### 父组件传数据给子组件

![image-20220418193325856](http://zjp.hxkj.live/MDImage/Vue/%e7%88%b6%e7%bb%84%e4%bb%b6%e4%bc%a0%e6%95%b0%e6%8d%ae%e7%bb%99%e5%ad%90%e7%bb%84%e4%bb%b6_2022-04-18_19-33-51.png)

```vue
<!-- /App.vue -->
<template>
  <div>
    <h1>{{ count }}</h1>
    <button @click="count += 1">+1</button>
    <Counter :number="count"></Counter>
  </div>
</template> 

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
  data() {
    return {
      count: 0,
    };
  },
};
</script>

<style lang="less" scoped>
</style>

```



```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <p>count的值是：{{ number }}</p>
  </div>
</template>

<script>
export default {
  name: "Counter",
  props: ["number"],
};
</script>

<style lang="less" scoped>
</style>
```



#### 子组件传数据给父组件

![image-20220418194133840](http://zjp.hxkj.live/MDImage/Vue/%e5%ad%90%e7%bb%84%e4%bb%b6%e4%bc%a0%e6%95%b0%e6%8d%ae%e7%bb%99%e7%88%b6%e7%bb%84%e4%bb%b6_2022-04-18_19-41-40.png)

```vue
<!-- /App.vue -->
<template>
  <div>
    <h1>{{ count }}</h1>
    <button @click="count += 1">+1</button>
    <Counter v-model:number="count"></Counter>
  </div>
</template> 

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
  data() {
    return {
      count: 0,
    };
  },
};
</script>

<style lang="less" scoped>
</style>

```



```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <p>count的值是：{{ number }}</p>
    <button @click="add">+1</button>
  </div>
</template>

<script>
export default {
  name: "Counter",
  props: ["number"],
  emits: ["update:number"],
  methods: {
    add() {
      this.$emit("update:number", this.number + 1);
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```



### watch 侦听器

- watch 侦听器允许开发者监视数据的变化，从而针对数据的变化做特定的操作。例如，监视用户名的变化并发起请求，判断用户名是否可用。

- 开发者需要在 watch 节点下，定义自己的侦听器。实例代码如下：

```vue
<!-- /App.vue -->
<template>
  <div>
    <input type="text" v-model.trim="username" />
  </div>
</template> 

<script>
export default {
  name: "App",
  data() {
    return {
      username: "",
    };
  },
  watch: {
    // 侦听器本质上是一个函数，要监视哪个数据的变化，就把数据名作为方法名即可
    // 新值在前，旧值在后
    // newVal 是"变化后的新值"，oldVal 是"变化之前的旧值"
    username(newVal, oldVal) {
      console.log(newVal, oldVal);
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```



#### 使用 watch 检测用户名是否可用

- 监听 username 值的变化，并使用 axios 发起 Ajax 请求，检测当前输入的用户名是否可用：

```vue
<!-- /App.vue -->
<template>
  <div>
    <input type="text" v-model.trim="username" />
  </div>
</template> 

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      username: "",
    };
  },
  watch: {
    async username(newVal, oldVal) {
      console.log(newVal, oldVal);
      // 解构赋值出 data 属性，并重命名为 res
      const { data: res } = await axios.get(
        "https://www.escook.cn/api/finduser/" + newVal
      );
      console.log(res);
    },
  },
};
</script>

<style lang="less" scoped>
</style>

```



#### immediate 选项

- 默认情况下，组件在初次加载完毕后不会调用 watch 侦听器。如果想让 watch 侦听器立即被调用，则需要使用 immediate 选项。实例代码如下：

```vue
<!-- /App.vue -->
<template>
  <div>
    <input type="text" v-model.trim="username" />
  </div>
</template> 

<script>
export default {
  name: "App",
  data() {
    return {
      username: "",
    };
  },
  watch: {
    // 定义对象格式的侦听器
    username: {
      // 侦听器的处理函数
      // handler 是固定写法，表示 username 的值变化时，自动调用 handler 处理函数
      handler(newVal, oldVal) {
        console.log(newVal, oldVal);
      },
      // immediate 选项的默认值是 false
      // immediate 的作用是：控制侦听器是否自动触发一次！
      // 表示页面初次渲染好之后，就立即触发当前的 watch 侦听器
      immediate: true,
    },
  },
};
</script>

<style lang="less" scoped>
</style>
```



#### deep 选项

- 当 watch 侦听的是一个对象，如果对象中的属性值发生了变化，则无法被监听到。此时需要使用 deep 选项，代码示例如下：

```vue
<!-- /App.vue -->
<template>
  <div>
    <input type="text" v-model.trim="info.username" />
  </div>
</template> 

<script>
export default {
  name: "App",
  data() {
    return {
      info: {
        username: "admin",
      },
    };
  },
  watch: {
    // 直接监听 info 对象的变化
    info: {
      // 侦听器的处理函数
      // handler 是固定写法，表示 info 对象任意一个的值变化时，自动调用 handler 处理函数
      handler(newVal) {
        console.log(newVal.username);
      },
      // 需要使用 deep 选项，否则 username 值的变化无法被监听到
      deep: true,
    },
  },
};
</script>

<style lang="less" scoped>
</style>

```

#### 监听对象单个属性的变化

- 如果只想监听对象中单个属性的变化，则可以按照如下的方式定义 watch 侦听器：

```vue
<!-- /App.vue -->
<template>
  <div>
    <input type="text" v-model.trim="info.username" />
  </div>
</template> 

<script>
export default {
  name: "App",
  data() {
    return {
      info: {
        username: "admin",
        age: 20,
      },
    };
  },
  watch: {
    // 只监听 info.username 属性值的变化
    "info.username": {
      // 侦听器的处理函数
      // handler 是固定写法，表示 info.username 属性值变化时，自动调用 handler 处理函数
      handler(newVal) {
        console.log(newVal.username);
      },
    },
  },
};
</script>

<style lang="less" scoped>
</style>

```

#### 计算属性 vs 侦听器

- 计算属性和侦听器侧重的应用场景不同：
  - 计算属性侧重于监听多个值的变化，最终计算并返回一个新值
  - 侦听器侧重于监听单个数据的变化，最终执行特定的业务处理，不需要有任何返回值



### 组件的生命周期

- 组件的生命周期指的是：组件从创建 -> 运行（渲染） -> 销毁的整个过程，强调的是一个时间段。

![image-20220418205856076](http://zjp.hxkj.live/MDImage/Vue/%e7%bb%84%e4%bb%b6%e7%9a%84%e8%bf%90%e8%a1%8c%e8%bf%87%e7%a8%8b_2022-04-18_20-59-02.png)



#### 监听组件的不同时刻

- vue 框架为组件内置了不同时刻的生命周期函数，生命周期函数会伴随着组件的运行而自动调用。例如：
  -  当组件在内存中被创建完毕之后，会自动调用 created 函数
  - 当组件被成功的渲染到页面上之后，会自动调用 mounted 函数
  - 当组件被销毁完毕之后，会自动调用 unmounted 函数

```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <div>Counter 组件</div>
  </div>
</template>

<script>
export default {
  name: "Counter",
  // 组件在内存中被创建完毕了
  created() {
    console.log("created");
  },
  // 组件第一次被渲染到了页面上
  mounted() {
    console.log("mounted");
  },
  // 组件被销毁完毕了
  unmounted() {
    console.log("unmounted");
  },
};
</script>

<style lang="less" scoped>
</style>
```



```vue
<!-- /App.vue -->
<template>
  <div>
    <Counter v-if="flag"></Counter>
    <button @click="flag = !flag">Toggle</button>
  </div>
</template> 

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  data() {
    return {
      flag: true,
    };
  },
  components: {
    Counter,
  },
};
</script>

<style lang="less" scoped>
</style>
```



#### 监听组件的更新

- 当组件的 data 数据更新之后，vue 会自动重新渲染组件的 DOM 结构，从而保证 View 视图展示的数据和 Model 数据源保持一致。
- 当组件被重新渲染完毕之后，会自动调用 updated 生命周期函数。

```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <div>Counter 组件{{ count }}</div>
    <button type="button" @click="count += 1">+1</button>
  </div>
</template>

<script>
export default {
  name: "Counter",
  data() {
    return {
      count: 0,
    };
  },
  // 组件在内存中被创建完毕了
  created() {
    console.log("created");
  },
  // 组件第一次被渲染到了页面上
  mounted() {
    console.log("mounted");
  },
  // 组件被销毁完毕了
  unmounted() {
    console.log("unmounted");
  },
  // 组件被重新渲染完毕了
  updated() {
    console.log("updated");
  },
};
</script>

<style lang="less" scoped>
</style>
```



#### 组件中主要的生命周期函数

- 注意：在实际开发中，created 是最常用的生命周期函数！

![image-20220418212307953](http://zjp.hxkj.live/MDImage/Vue/%e7%bb%84%e4%bb%b6%e4%b8%ad%e4%b8%bb%e8%a6%81%e7%9a%84%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f%e5%87%bd%e6%95%b0_2022-04-18_21-23-20.png)



#### 组件中全部的生命周期函数

![image-20220418212539947](http://zjp.hxkj.live/MDImage/Vue/%e7%bb%84%e4%bb%b6%e4%b8%ad%e5%85%a8%e9%83%a8%e7%9a%84%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f%e5%87%bd%e6%95%b0_2022-04-18_21-25-45.png)

- 可以参考 vue 官方文档给出的“生命周期图示”，进一步理解组件生命周期执行的过程：https://v3.cn.vuejs.org/guide/instance.html#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE%E7%A4%BA



###  组件之间的数据共享

#### 组件之间的关系

- 在项目开发中，组件之间的关系分为如下 3 种：
  - 父子关系
  - 兄弟关系
  - 后代关系

![image-20220419100607930](http://zjp.hxkj.live/MDImage/Vue/%e7%bb%84%e4%bb%b6%e4%b9%8b%e9%97%b4%e7%9a%84%e5%85%b3%e7%b3%bb_2022-04-19_10-06-15.png)



#### 父子组件之间的数据共享

- 父子组件之间的数据共享又分为：
  - 父 -> 子共享数据
  - 子 -> 父共享数据
  - 父 <-> 子双向数据同步

##### 父组件向子组件共享数据

- 父组件通过 v-bind 属性绑定向子组件共享数据。同时，子组件需要使用 props 接收数据。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <!-- 父向子传值 -->
    <MyTest :msg="message" :user="userinfo"></MyTest>
  </div>
</template>

<script>
// 导入子组件
import MyTest from "./components/MyTest.vue";

export default {
  name: "App",
  components: {
    MyTest,
  },
  data() {
    return {
      message: "hello vue",
      userinfo: { name: "zs", age: 20 },
    };
  },
};
</script>
```



```vue
<!-- /components/MyTest.vue -->
<template>
  <div>
    <h3>测试父子传值</h3>
    <p>{{ msg }}</p>
    <p>{{ user }}</p>
  </div>
</template>

<script>
export default {
  name: "MyTest",
  props: ["msg", "user"],
};
</script>
```



##### 子组件向父组件共享数据

- 子组件通过自定义事件的方式向父组件共享数据。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <!-- 子向父传值 -->
    <!-- 监听子组件的自定义事件 -->
    <MyTest @n1change="getn1"></MyTest>
    <h1>{{ n1FromSon }}</h1>
  </div>
</template>

<script>
// 导入子组件
import MyTest from "./components/MyTest.vue";

export default {
  name: "App",
  components: {
    MyTest,
  },
  data() {
    return {
      n1FromSon: 0,
    };
  },
  methods: {
    // 通过形参，接收子组件传递过来的数据
    getn1(n1) {
      this.n1FromSon = n1;
    },
  },
};
</script>

```



```vue
<!-- /components/MyTest.vue -->
<template>
  <div>
    <h3>测试父子传值</h3>
    <button @click="addN1">+1</button>
  </div>
</template>

<script>
export default {
  name: "MyTest",
  emits: ["n1change"],
  data() {
    return {
      n1: 0,
    };
  },
  methods: {
    addN1() {
      this.n1++;
      // 数据变化的时候，触发自定义事件，并把值传给父组件
      this.$emit("n1change", this.n1);
    },
  },
};
</script>

```

##### 父子组件之间数据的双向同步

- 父组件在使用子组件期间，可以使用 v-model 指令维护组件内外数据的双向同步：

![image-20220419104036450](http://zjp.hxkj.live/MDImage/Vue/%e7%88%b6%e5%ad%90%e7%bb%84%e4%bb%b6%e4%b9%8b%e9%97%b4%e6%95%b0%e6%8d%ae%e7%9a%84%e5%8f%8c%e5%90%91%e5%90%8c%e6%ad%a5_2022-04-19_10-40-49.png)



```vue
<!-- App.vue -->
<template>
  <div>
    <h1>{{ num }}</h1>
    <button @click="num += 1">+1</button>
    <hr />
    <!-- 父子双向传值 -->
    <MyTest v-model:num="num"></MyTest>
  </div>
</template>

<script>
// 导入子组件
import MyTest from "./components/MyTest.vue";

export default {
  name: "App",
  components: {
    MyTest,
  },
  data() {
    return {
      num: 0,
    };
  },
  methods: {
    add() {
      this.num += 1;
    },
  },
};
</script>

```



```vue
<!-- /components/MyTest.vue -->
<template>
  <div>
    <h3>{{ num }}</h3>
    <button @click="add">+1</button>
  </div>
</template>

<script>
export default {
  name: "MyTest",
  props: ["num"],
  emits: ["update:num"],
  methods: {
    add() {
      let newNum = this.num + 1;
      this.$emit("update:num", newNum);
    },
  },
};
</script>
```



#### 兄弟组件之间的数据共享

- 兄弟组件之间实现数据共享的方案是 EventBus。可以借助于第三方的包 mitt 来创建 eventBus 对象，从而实现兄弟组件之间的数据共享。示意图如下

![image-20220419112622540](http://zjp.hxkj.live/MDImage/Vue/%e5%85%84%e5%bc%9f%e7%bb%84%e4%bb%b6%e4%b9%8b%e9%97%b4%e7%9a%84%e6%95%b0%e6%8d%ae%e5%85%b1%e4%ba%ab_2022-04-19_11-26-32.png)

##### 安装 mitt 依赖包

- 在项目中运行如下的命令，安装 mitt 依赖包：

```bash
npm i mitt@2.1.0
```



##### 创建公共的 EventBus 模块

- 在根目录下创建 eventBus.js

- 在项目中创建公共的 eventBus 模块如下：

```javascript
// eventBus.js
// 导入 mitt 包
import mitt from "mitt";
// 创建 EventBus 的实例对象
const bus = mitt();
// 将 EventBus 的实例对象共享出去
export default bus;
```



##### 在数据接收方自定义事件

- 在数据接收方，调用 bus.on('事件名称', 事件处理函数) 方法注册一个自定义事件。示例代码如下：

```vue
<template>
  <div>
    <h1>MyRight接收方</h1>
    <h1>{{ count }}</h1>
  </div>
</template>

<script>
// 导入 eventBus.js 模块，得到共享的 bus 对象
import bus from "../../eventBus.js";
export default {
  data() {
    return {
      count: 0,
    };
  },
  created() {
    // 调用 bus.on() 方法注册一个自定义事件，通过事件处理函数的形参接收数据
    bus.on("countChange", (count) => {
      this.count = count;
    });
  },
};
</script>
```



##### 在数据接发送方触发事件

- 在数据发送方，调用 bus.emit('事件名称', 要发送的数据) 方法触发自定义事件。示例代码如下：

```vue
<template>
  <div>
    <h1>MyLeft发送方</h1>
    <h1>{{ count }}</h1>
    <button @click="add">+1</button>
  </div>
</template>

<script>
// 导入 eventBus.js 模块，得到共享的 bus 对象
import bus from "../../eventBus.js";
export default {
  data() {
    return { count: 0 };
  },
  methods: {
    add() {
      this.count += 1;
      // 调用 bus.emit() 方法触发自定义事件，并发送数据
      bus.emit("countChange", this.count);
    },
  },
};
</script>
```



#### 后代关系组件之间的数据共享

- 后代关系组件之间共享数据，指的是父节点的组件向其子孙组件共享数据。此时组件之间的嵌套关系比较复杂，可以使用 provide 和 inject 实现后代关系组件之间的数据共享。

##### 父节点通过 provide 共享数据

- 父节点的组件可以通过provide 方法，对其子孙组件共享数据：

```vue
<!-- App.vue -->
<template>
  <div>
    <h1>{{ num }}</h1>
    <hr />
    <MyLeft></MyLeft>
  </div>
</template>

<script>
// 导入子组件
import MyLeft from "./components/MyLeft.vue";
export default {
  name: "App",
  components: {
    MyLeft,
  },
  data() {
    return {
      // 定义父组件要向子孙组件共享的数据
      num: 20,
    };
  },
  // provide 函数 return 的对象中，包含了要向子孙组件共享的数据
  provide() {
    return {
      number: this.num,
    };
  },
};
</script>

```

##### 子孙节点通过 inject 接收数据

- 子孙节点可以使用 inject 数组，接收父级节点向下共享的数据。示例代码如下：

```vue
<template>
  <div>
    <h1>{{ number }}</h1>
  </div>
</template>

<script>
export default {
  // 子孙组件，使用 inject 接收父节点向下共享的 number 数据，并在页面上使用
  inject: ["number"],
};
</script>
```



##### 父节点对外共享响应式的数据

- 父节点使用 provide 向下共享数据时，可以结合computed 函数向下共享响应式的数据。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <h1>{{ num }}</h1>
    <button @click="add">+1</button>
    <hr />
    <MyLeft></MyLeft>
  </div>
</template>

<script>
// 从 vue 中按需导入 computed 函数
import { computed } from "vue";
import MyLeft from "./components/MyLeft.vue";
export default {
  name: "App",
  components: {
    MyLeft,
  },
  data() {
    return {
      // 定义父组件要向子孙组件共享的数据
      num: 20,
    };
  },
  methods: {
    add() {
      this.num += 1;
    },
  },
  // provide 函数 return 的对象中，包含了要向子孙组件共享的数据
  provide() {
    return {
      // 使用 computed 函数，可以把要共享的数据包装成响应式的数据
      number: computed(() => this.num),
    };
  },
};
</script>

```



##### 子孙节点使用响应式的数据

- 如果父级节点共享的是响应式的数据，则子孙节点必须以 .value 的形式进行使用。示例代码如下：

```vue
<template>
  <div>
    <!-- 响应式的数据，必须以 .value 的形式进行使用 -->
    <h1>{{ number.value }}</h1>
  </div>
</template>

<script>
export default {
  // 子孙组件，使用 inject 接收父节点向下共享的 number 数据，并在页面上使用
  inject: ["number"],
};
</script>
```



### Vuex

- vuex 是终极的组件之间的数据共享方案。在企业级的 vue 项目开发中，vuex 可以让组件之间的数据共享变得高效、清晰、且易于维护。

![image-20220419164232569](http://zjp.hxkj.live/MDImage/Vue/vuex_2022-04-19_16-42-37.png)



### 全局配置 axios

- 在实际项目开发中，几乎每个组件中都会用到 axios 发起数据请求。此时会遇到如下两个问题：
  - 每个组件中都需要导入axios（代码臃肿）
  - 每次发请求都需要填写完整的请求路径（不利于后期的维护）



![image-20220419164743813](http://zjp.hxkj.live/MDImage/Vue/%e5%85%a8%e5%b1%80%e9%85%8d%e7%bd%aeaxios_2022-04-19_16-47-50.png)



- 步骤
- 在 main.js 入口文件中，通过 `app.config.globalProperties` 全局挂载 axios，示例代码如下：
- 其中 `$http` 是自定义属性名，可按需修改

![image-20220419165112882](http://zjp.hxkj.live/MDImage/Vue/%e5%85%a8%e5%b1%80%e9%85%8d%e7%bd%aeaxios_2022-04-19_16-51-15.png)

```javascript
// /main.js
import { createApp } from 'vue';
import App from './App.vue';
// 导入 axios 模块
import axios from 'axios';

const app = createApp(App);
// 为 axios 配置请求的根路径
axios.defaults.baseURL = 'https://www.escook.cn';
// 将 axios 挂载为 app 的全局自定义属性
// 每个组件可以通过 this 直接访问到全局挂载的自定义属性，vue 的内置成员都以 $ 开头
app.config.globalProperties.$http = axios;
app.mount('#app');
```

- POST 模块

```vue
<!-- /components/PostInfor.vue -->
<template>
  <div>
    <button @click="postInfo">POST</button>
  </div>
</template>

<script>
export default {
  methods: {
    async postInfo() {
      const { data: res } = await this.$http.post("/api/post", {
        name: "zs",
        age: 20,
      });
      console.log(res);
    },
  },
};
</script>
```

-  GET 模块

```vue
<!-- /components/GetInfor.vue -->
<template>
  <div>
    <button @click="getInfo">GET</button>
  </div>
</template>

<script>
export default {
  methods: {
    async getInfo() {
      const { data: res } = await this.$http.get("/api/get", {
        params: {
          name: "ls",
          age: 33,
        },
      });
      console.log(res);
    },
  },
};
</script>
```



### ref 引用

- ref 用来辅助开发者在不依赖于jQuery 的情况下，获取 DOM 元素或组件的引用。
- 每个 vue 的组件实例上，都包含一个$refs 对象，里面存储着对应的DOM 元素或组件的引用。默认情况下，组件的 $refs 指向一个空对象。

```vue
<template>
  <div>
    <h1>MyRef 组件</h1>
    <button @click="getRef">获取 $refs 引用</button>
  </div>
</template>
<script>
export default {
  methods: {
    getRef() {
      // this 代表当前组件的实例对象
      console.log(this); // 其中 Target 表示当前组件
      // this.$refs 默认指向空对象
      console.log(this.$refs); // 打印：{}
    },
  },
};
</script>
```



#### 使用 ref 引用 DOM 元素

- 如果想要使用 ref 引用页面上的 DOM 元素，则可以按照如下的方式进行操作：

```vue
<template>
  <div>
    <!-- 使用 ref 属性，为对应的 DOM 添加引用名称 -->
    <h3 ref="myh3">MyRef 组件</h3>
    <button @click="getRef">获取 $refs 引用</button>
  </div>
</template>
<script>
export default {
  methods: {
    getRef() {
      // 通过 this.$$refs.引用的名称，可以获取到 DOM 元素的引用
      console.log(this.$refs.myh3);
      // 操作 DOM 元素，把文本颜色改为红色
      this.$refs.myh3.style.color = "red";
    },
  },
};
</script>
```



#### 使用 ref 引用组件实例

- 如果想要使用 ref 引用页面上的组件实例，则可以按照如下的方式进行操作：

```vue
<!-- App.vue -->
<template>
  <div>
    <button @click="reset">重置</button>
    <hr />
    <!-- 使用 ref 属性，为对应组件添加引用名称，命名统一以 Ref 结尾 -->
    <Counter ref="counterRef"></Counter>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
  methods: {
    reset() {
      // 通过 this.$refs.引用的名称 可以引用组件的实例
      console.log(this.$refs.counterRef);
      // 引用到组件的实例之后，就可以调用组件上的 methods 方法
      this.$refs.counterRef.reset();
    },
  },
};
</script>
```



```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <h1>{{ count }}</h1>
    <button @click="add">+1</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    add() {
      this.count += 1;
    },
    reset() {
      this.count = 0;
    },
  },
};
</script>
```

##### 控制文本框和按钮的按需切换

- 通过布尔值 inputVisible 来控制组件中的文本框与按钮的按需切换。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <input type="text" v-if="inputVisible" />
    <button v-else @click="showInput">展示 input 输入框</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      inputVisible: false,
    };
  },
  methods: {
    showInput() {
      // 要展示文本框
      this.inputVisible = true;
    },
  },
};
</script>

```



##### 让文本框自动获得焦点

- 当文本框展示出来之后，如果希望它立即获得焦点，则可以为其添加 ref 引用，并调用原生 DOM 对象的.focus() 方法即可。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <input type="text" v-if="inputVisible" ref="inputRef" />
    <button v-else @click="showInput">展示 input 输入框</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      inputVisible: false,
    };
  },
  methods: {
    showInput() {
      // 要展示文本框
      this.inputVisible = true;
      // 获取文本框的引用对象，然后调用 focus() 方法
      this.$refs.inputRef.focus(); // 报错，原因 DOM 元素的更新是异步的，当执行到该代码时，DOM 未完成更新，获取 inputRef 失败，为 undefined
    },
  },
};
</script>

```

##### this.$nextTick(cb) 方法

- 组件的 $nextTick(cb) 方法，会把 cb 回调推迟到下一个 DOM 更新周期之后执行。通俗的理解是：等组件的DOM 异步地重新渲染完成后，再执行 cb 回调函数。从而能保证cb 回调函数可以操作到最新的 DOM 元素。

```vue
<!-- App.vue -->
<template>
  <div>
    <input type="text" v-if="inputVisible" ref="inputRef" />
    <button v-else @click="showInput">展示 input 输入框</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      inputVisible: false,
    };
  },
  methods: {
    showInput() {
      // 要展示文本框
      this.inputVisible = true;
      // 获取文本框的引用对象，然后调用 focus() 方法
      this.$nextTick(() => {
        // 把对 input 文本框的操作，推迟到下次 DOM 更新之后。否则页面上根部不存在文本框元素
        this.$refs.inputRef.focus();
      });
    },
  },
};
</script>

```



### 动态组件

- 动态组件指的是动态切换组件的显示与隐藏。vue 提供了一个内置的 `<component>` 组件，专门用来实现组件的动态渲染。
  - ` <component>` 是组件的占位符
  - 通过 is 属性动态指定要渲染的组件名称
  - `<component is="要渲染的组件的名称"></component>`

```vue
<!-- App.vue -->
<template>
  <div>
    <!-- 点击按钮，动态切换组件的名称 -->
    <button @click="cutMyLeft">显示MyLeft</button>
    <button @click="cutMyRight">显示MyRight</button>
    <!-- 通过 is 属性，动态指定要渲染的组件的名称 -->
    <component :is="comName" v-if="comName != ''"></component>
    <MyLeft></MyLeft>
    <MyRight></MyRight>
  </div>
</template>

<script>
import MyLeft from "./components/MyLeft.vue";
import MyRight from "./components/MyRight.vue";
export default {
  name: "App",
  components: {
    MyLeft,
    MyRight,
  },
  data() {
    return {
      // 当前要渲染的组件的名称
      comName: "",
    };
  },
  methods: {
    cutMyLeft() {
      // 设置要渲染的组件的名称
      this.comName = "MyLeft";
    },
    cutMyRight() {
      // 设置要渲染的组件的名称
      this.comName = "MyRight";
    },
  },
};
</script>
```

#### 使用 keep-alive 保持状态

- 默认情况下，切换动态组件时无法保持组件的状态。此时可以使用vue 内置的 `<keep-alive>` 组件保持动态组件的状态。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <button @click="cutMyLeft">显示MyLeft</button>
    <button @click="cutMyRight">显示MyRight</button>
    <!-- keep-aliv，保持组件的状态，让组件在隐藏的时候不会销毁，而是存储在内存中 -->
    <keep-alive>
      <component :is="comName" v-if="comName != ''"></component>
    </keep-alive>
  </div>
</template>

<script>
import MyLeft from "./components/MyLeft.vue";
import MyRight from "./components/MyRight.vue";
export default {
  name: "App",
  components: {
    MyLeft,
    MyRight,
  },
  data() {
    return {
      comName: "",
    };
  },
  methods: {
    cutMyLeft() {
      this.comName = "MyLeft";
    },
    cutMyRight() {
      this.comName = "MyRight";
    },
  },
};
</script>

```



### 插槽

- 插槽（Slot）是 vue 为组件的封装者提供的能力。允许开发者在封装组件时，把不确定的、希望由用户指定的部分定义为插槽。

![image-20220420091735660](http://zjp.hxkj.live/MDImage/Vue/%e6%8f%92%e6%a7%bd_2022-04-20_09-17-40.png)

- 可以把插槽认为是组件封装期间，为用户预留的内容的占位符。

#### 插槽的基础用法

- 在封装组件时，可以通过 `<slot>` 元素定义插槽，从而为用户预留内容占位符。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <p>App.vue</p>
    <Counter>
      <!-- 在使用 Counter 组件时，为插槽指定具体的内容 -->
      <p>在 Counter.vue 插槽中额外添加标签</p>
    </Counter>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>

```



```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <!-- 通过 slot 标签，为用户预留内容占位符（插槽） -->
    <slot></slot>
  </div>
</template>

<script>
export default {};
</script>
```

#### 没有预留插槽的内容会被丢弃

- 如果在封装组件时没有预留任何 `<slot>` 插槽，则用户提供的任何自定义内容都会被丢弃。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <p>App.vue</p>
    <Counter>
      <!-- 自定义内容会被丢弃 -->
      <p>在 Counter.vue 插槽中额外添加标签</p>
    </Counter>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>

```



```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <!-- 封装组件时，没有预留任何插槽 -->
  </div>
</template>

<script>
export default {};
</script>
```



#### 后备内容

- 封装组件时，可以为预留的 `<slot>` 插槽提供后备内容（默认内容）。如果组件的使用者没有为插槽提供任何内容，则后备内容会生效。示例代码如下：

```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <!-- 通过 slot 标签，为用户预留内容占位符（插槽） -->
    <slot>这是后备内容，在组件使用者没有提供插槽内容的时候生效</slot>
  </div>
</template>

<script>
export default {};
</script>
```



#### 具名插槽

- 如果在封装组件时需要预留多个插槽节点，则需要为每个 `<slot>` 插槽指定具体的 name 名称。这种带有具体名称的插槽叫做“具名插槽”。示例代码如下：

- 注意：没有指定 name 名称的插槽，会有隐含的名称叫做 “default”。

```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <header>
      <!-- 把页头放在这里 -->
      <slot name="header"></slot>
    </header>
    <main>
      <!-- 把主要内容放在这里 -->
      <slot></slot>
    </main>
    <footer>
      <!-- 把页脚放在这里 -->
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<script>
export default {};
</script>
```

- 在向具名插槽提供内容的时候，我们可以在一个 `<template>` 元素上使用 v-slot 指令，并以 v-slot 的参数的形式提供其名称。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <Counter>
      <template v-slot:header>
        <h1>标题</h1>
      </template>
      <template v-slot:default>
        <p>正文</p>
      </template>
      <template v-slot:footer>
        <p>页脚</p>
      </template>
    </Counter>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>
```

##### 简写

- 跟 v-on 和 v-bind 一样，v-slot 也有缩写，即把参数之前的所有内容 (v-slot:) 替换为字符 #。例如 v-slot:header可以被重写为 #header

```vue
<!-- App.vue -->
<template>
  <div>
    <Counter>
      <template #header>
        <h1>标题</h1>
      </template>
      <template #default>
        <p>正文</p>
      </template>
      <template #footer>
        <p>页脚</p>
      </template>
    </Counter>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>
```



#### 作用域插槽

- 在封装组件的过程中，可以为预留的 `<slot>` 插槽绑定 props 数据，这种带有 props 数据的 `<slot>` 叫做“作用域插槽”。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <Counter>
      <!-- 接收插槽外向传的数据，默认使用 scope 进行接收 -->
      <template #default="scope">
        <p>{{ scope }}</p>
        <!-- { "age": 18, "sex": "男" } -->
        <p>我今年{{ scope.age }}岁</p>
        <!-- 我今年18岁 -->
        <p>我是{{ scope.sex }}生</p>
        <!-- 我是男生 -->
      </template>
    </Counter>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>

```



```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <!-- 设定插槽需要向外传递的属性值，供使用者调用 -->
    <slot :age="age" :sex="sex"></slot>
  </div>
</template>

<script>
export default {
  data() {
    return {
      age: 18,
      sex: "男",
    };
  },
};
</script>
```



##### 解构作用域插槽的 Prop

- 作用域插槽对外提供的数据对象，可以使用解构赋值简化数据的接收过程。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <Counter>
      <!-- 作用域插槽对外提供的数据对象，可以通过"结构赋值"简化接收的过程 -->
      <template #default="{ age, sex }">
        <p>我今年{{ age }}岁</p>
        <!-- 我今年18岁 -->
        <p>我是{{ sex }}生</p>
        <!-- 我是男生 -->
      </template>
    </Counter>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>

```



```vue
<!-- /components/Counter.vue -->
<template>
  <div>
    <!-- 设定插槽需要向外传递的属性值，供使用者调用 -->
    <slot :age="age" :sex="sex"></slot>
  </div>
</template>

<script>
export default {
  data() {
    return {
      age: 18,
      sex: "男",
    };
  },
};
</script>
```



##### 使用场景

- 封装组件的时候如果不确定组件的 DOM 渲染成什么样子，需要使用者进行样式调整，就需要声明作用域插槽把数据传递给使用者，进行样式调整。

```vue
<!-- App.vue -->
<template>
  <div>
    <Counter>
      <template #default="{ user }">
        <!-- 根据需求修改样式，从而不影响组件 -->
        <td>{{ user.id }}</td>
        <td>{{ user.name }}</td>
        <td>
          <input type="checkbox" :checked="user.state" />
        </td>
      </template>
    </Counter>
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>

```



```vue
<template>
  <table>
    <!-- 表头区域 -->
    <thead>
      <tr>
        <th>Id</th>
        <th>Name</th>
        <th>State</th>
      </tr>
    </thead>
    <!-- 表格主体区域 -->
    <tbody>
      <!-- 循环渲染表格数据 -->
      <tr v-for="item in list" :key="item.id">
        <slot :user="item"></slot>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "Counter",
  data() {
    return {
      // 列表的数据
      list: [
        { id: 1, name: "张三", state: true },
        { id: 2, name: "李四", state: false },
        { id: 3, name: "赵六", state: false },
      ],
    };
  },
};
</script>

<style lang="less" scoped></style>

```



### 自定义指令

- vue 官方提供了 v-for、v-model、v-if 等常用的内置指令。除此之外 vue 还允许开发者自定义指令。
- vue 中的自定义指令分为两类，分别是：
  - 私有自定义指令
  - 全局自定义指令

- 自定义指令使用必须以 v- 开头，声明的时候不需要。

#### 私有自定义指令

- 在每个 vue 组件中，可以在 directives 节点下声明私有自定义指令。示例代码如下：
- 在使用自定义指令时，需要加上 v- 前缀。示例代码如下：

```vue
<template>
  <div>
    <!-- 声明自定义指令时，指定的名称是 focus -->
    <!-- 使用自定义指令时，需要加上 v- 指令前缀 -->
    <input type="text" v-focus />
  </div>
</template>

<script>
export default {
  name: "Counter",
  directives: {
    // 自定义一个私有指令
    focus: {
      // 当被绑定的元素插入到 DOM 中时，自动触发 mounted 函数
      mounted(el) {
        el.focus(); // 让被触发的元素自动获得焦点
      },
    },
  },
};
</script>

<style lang="less" scoped></style>
```



#### 全局自定义指令

- 全局共享的自定义指令需要通过“单页面应用程序的实例对象”进行声明，示例代码如下：

```javascript
// /main.js
import { createApp } from 'vue';
import App from './App.vue';

const app = createApp(App);
// 注册一个全局自定义指令 v-focus
app.directive('focus', {
    // 当被绑定的元素插入到 DOM 中时，自动触发 mounted 函数
    mounted(el) {
        el.focus();
    }
})
app.mount('#app');
```



```vue
<!-- App.vue -->
<template>
  <div>
    <!-- 使用全局自定义指令 v-focus -->
    <input type="text" v-focus />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

```

#### update 函数

- mounted 函数只在元素第一次插入 DOM 时被调用，当 DOM 更新时 mounted 函数不会被触发。 updated 函数会在每次 DOM 更新完成后被调用。示例代码如下：

```javascript
// /main.js
import { createApp } from 'vue';
import App from './App.vue';

const app = createApp(App);
// 注册一个全局自定义指令 v-focus
app.directive('focus', {
    // 第一次插入 DOM 时触发这个函数
    mounted(el) {
        el.focus();
    },
    // 每次 DOM 更新时都会触发 updated 函数
    updated(el) {
        el.focus();
    },
})
app.mount('#app');
```

#### 简写

- 如果 mounted 和updated 函数中的逻辑完全相同，则可以简写成如下格式：

```javascript
// /main.js
import { createApp } from 'vue';
import App from './App.vue';

const app = createApp(App);
// 注册一个全局自定义指令 v-focus
app.directive('focus', (el) => {
    // 在 mounted 和 updated 时都会触发相同的业务处理
    el.focus();
})
app.mount('#app');
```



```vue
<template>
  <div>
    <input type="text" v-focus />
  </div>
</template>

<script>
export default {
  name: "Counter",
  directives: {
    // 在 mounted 和 updated 时都会触发相同的业务处理
    focus(el) {
      el.focus();
    },
  },
};
</script>

<style lang="less" scoped></style>
```



#### 指令的参数值

- 在绑定指令时，可以通过“等号”的形式为指令绑定具体的参数值，示例代码如下：
- 全局自定义指令

```javascript
// /main.js
import { createApp } from 'vue';
import App from './App.vue';

const app = createApp(App);
// 注册一个全局自定义指令 v-color
// 一般形参都定义为 binding
app.directive('color', (el, binding) => {
    // binding.value 就是通过"等号"为指令绑定的值
    el.style.color = binding.value;
})
app.mount('#app');
```



```vue
<template>
  <div>
    <!-- 在使用 v-color 指令时，可以通过"等号"绑定指令的值 -->
    <p v-color="'red'">Counter 组件</p>
  </div>
</template>

<script>
export default {
  name: "Counter",
};
</script>

<style lang="less" scoped></style>
```

- 私有自定义指令

```vue
<template>
  <div>
    <!-- 在使用 v-color 指令时，可以通过"等号"绑定指令的值 -->
    <p v-color="'red'">Counter 组件</p>
  </div>
</template>

<script>
export default {
  name: "Counter",
  directives: {
    // 自定义一个私有指令
    color(el, binding) {
      el.style.color = binding.value;
    },
  },
};
</script>

<style lang="less" scoped></style>
```





### 插件安装

- Path Autocomplete ：用于提示路径
  - 在vs code 设置中 setting.json 的开头添加以下配置信息

```json
// 导入文件时是否携带文件的拓展名
"path-autocomplete.extensionOnImport": true,
// 配置 @ 的路径提示
"path-autocomplete.pathMappings": {
    "@": "${folder}/src"
},
```

- Auto Close Tag：自动闭合 HTML 标签

## vue-router

### 路由

- 路由（英文：router）就是对应关系。路由分为两大类：
  - 后端路由
  - 前端路由

#### 后端路由

- 后端路由指的是：请求方式、请求地址与 function 处理函数之间的对应关系。在 node.js 课程中，express 路由的基本用法如下：

```javascript
import express from "express";
import router = express.Router();


router.get('/userlist', function(req, res) { /* 路由的处理函数 */ });
router.post('/adduser', function(req, res) { /* 路由的处理函数 */ });

export default router;
```



#### SPA 与前端路由

- SPA 指的是一个 web 网站只有唯一的一个 HTML 页面，所有组件的展示与切换都在这唯一的一个页面内完成。此时，不同组件之间的切换需要通过前端路由来实现。
- 结论：在 SPA 项目中，不同功能之间的切换，要依赖于前端路由来完成！



#### 前端路由

- 通俗易懂的概念：Hash 地址与组件之间的对应关系。



##### 前端路由的工作方式

1. 用户点击了页面上的路由链接
2. 导致了 URL 地址栏中的 Hash 值发生了变化
3. 前端路由监听了到 Hash 地址的变化
4. 前端路由把当前 Hash 地址对应的组件渲染都浏览器中

![image-20220420113031458](http://zjp.hxkj.live/MDImage/Vue/%e5%89%8d%e7%ab%af%e8%b7%af%e7%94%b1%e7%9a%84%e5%b7%a5%e4%bd%9c%e6%96%b9%e5%bc%8f_2022-04-20_11-30-38.png)

- 结论：前端路由，指的是 Hash 地址与组件之间的对应关系！

##### 实现简易的前端路由

- 步骤1：导入并注册 MyHome、MyMovie、MyAbout 三个组件。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div></div>
</template>

<script>
import MyHome from "./components/MyHome.vue";
import MyMove from "./components/MyMove.vue";
import MyAbout from "./components/MyAbout.vue";
export default {
  name: "App",
  components: {
    MyHome,
    MyMove,
    MyAbout,
  },
};
</script>
```

- 步骤2：通过 `<component>` 标签的 is 属性，动态切换要显示的组件。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <component :is="comName"></component>
  </div>
</template>

<script>
import MyHome from "./components/MyHome.vue";
import MyMove from "./components/MyMove.vue";
import MyAbout from "./components/MyAbout.vue";
export default {
  name: "App",
  components: {
    MyHome,
    MyMove,
    MyAbout,
  },
  data() {
    return {
      comName: "MyHome",
    };
  },
};
</script>
```

- 步骤3：在组件的结构中声明如下 3 个 `<a>` 链接，通过点击不同的 `<a>` 链接，切换浏览器地址栏中的Hash 值：

```vue
<!-- App.vue -->
<template>
  <div>
    <a href="#/home">Home</a>&nbsp; <a href="#/move">Move</a>&nbsp;
    <a href="#/about">About</a>&nbsp;
    <component :is="comName"></component>
  </div>
</template>

<script>
import MyHome from "./components/MyHome.vue";
import MyMove from "./components/MyMove.vue";
import MyAbout from "./components/MyAbout.vue";
export default {
  name: "App",
  components: {
    MyHome,
    MyMove,
    MyAbout,
  },
  data() {
    return {
      comName: "MyHome",
    };
  },
};
</script>

```

- 步骤4：在 created 生命周期函数中监听浏览器地址栏中 Hash 地址的变化，动态切换要展示的组件的名称：

```vue
<!-- App.vue -->
<template>
  <div>
    <a href="#/home">Home</a>&nbsp; <a href="#/move">Move</a>&nbsp;
    <a href="#/about">About</a>&nbsp;
    <component :is="comName"></component>
  </div>
</template>

<script>
import MyHome from "./components/MyHome.vue";
import MyMove from "./components/MyMove.vue";
import MyAbout from "./components/MyAbout.vue";
export default {
  name: "App",
  components: {
    MyHome,
    MyMove,
    MyAbout,
  },
  data() {
    return {
      comName: "MyHome",
    };
  },
  created() {
    window.onhashchange = () => {
      switch (location.hash) {
        case "#/home":
          this.comName = "MyHome";
          break;
        case "#/move":
          this.comName = "MyMove";
          break;
        case "#/about":
          this.comName = "MyAbout";
          break;
      }
    };
  },
};
</script>
```

###  vue-router

- vue-router 是 vue.js 官方给出的路由解决方案。它只能结合 vue 项目进行使用，能够轻松的管理 SPA 项目中组件的切换。

- vue-router 目前有 3.x 的版本和 4.x 的版本。其中：
  - vue-router 4.x 只能结合 vue3 进行使用
- vue-router 4.x 的官方文档地址：https://next.router.vuejs.org/





### 使用步骤

1. 在项目中安装 vue-router
2. 定义路由组件
3. 声明路由链接和占位符
4. 创建路由模块
5. 导入并挂载路由模块



#### 在项目中安装 vue-router

- 在 vue3 的项目中，只能安装并使用vue-router 4.x。安装的命令如下：

```bash
# 指定版本为 next，就会安装 4.x 最新版本
npm i vue-router@next -S
```



#### 定义路由组件

- 在项目中定义 MyHome.vue、MyMovie.vue、MyAbout.vue三个组件，将来要使用vue-router 来控制它们的展示与切换：

```vue
<!-- /components/MyHome.vue -->
<template>
  <div>
    <h1>MyHome</h1>
  </div>
</template>
<script>
export default {
  name: "MyHome",
};
</script>
```

```vue
<!-- /components/MyMovie.vue -->
<template>
  <div>
    <h1>MyMovie</h1>
  </div>
</template>
<script>
export default {
  name: "MyMovie",
};
</script>
```

```vue
<!-- /components/MyAbout.vue -->
<template>
  <div>
    <h1>MyAbout</h1>
  </div>
</template>
<script>
export default {
  name: "MyAbout",
};
</script>
```



#### 声明路由链接和占位符

- 可以使用 `<router-link>` 标签来声明路由链接，并使用 `<router-view>` 标签来声明路由占位符。示例代码如下：

```vue
<!-- App.vue -->
<template>
  <div>
    <!-- 声明路由链接，声明 Hash 地址不需要 #，#可省略-->
    <router-link to="/home">Home</router-link>&nbsp;
    <router-link to="/movie">Movie</router-link>&nbsp;
    <router-link to="/about">About</router-link>&nbsp;

    <!-- 路由的占位符，用来呈现需要展示组件的位置 -->
    <router-view></router-view>
  </div>
</template>

<script>
import MyHome from "./components/MyHome.vue";
import MyMovie from "./components/MyMovie.vue";
import MyAbout from "./components/MyAbout.vue";
export default {
  name: "App",
  components: {
    MyHome,
    MyMovie,
    MyAbout,
  },
};
</script>
```



#### 创建路由模块

- 在项目中创建 router.js 路由模块，在其中按照如下 5 个步骤创建并得到路由的实例对象：
  1. 从 vue-router 中按需导入两个方法
  2. 导入需要使用路由控制的组件
  3. 创建路由实例对象
  4. 向外共享路由实例对象
  5. 在 main.js 中导入并挂载路由模块

- 从 vue-router 中按需导入两个方法

```javascript
// /router.js
// 从 vue-router 中按需导入两个方法
// createRouter 方法用于创建路由的实例对象
// createWebHashHistory 用于指定路由的工作模式（ hash 模式）
import { createRouter, createWebHashHistory } from 'vue-router';
```

- 导入需要使用路由控制的组件

```javascript
// 导入组件，这些组件将要以路由的方式，来控制它们的切换
import Home from './components/MyHome.vue';
import Movie from './components/MyMovie.vue';
import About from './components/MyAbout.vue';
```

- 创建路由实例对象

```javascript
// 创建路由实例对象
const router = createRouter({
    // 通过 history 属性指定路由的工作模式
    history: createWebHashHistory(),
    // 通过 routes 数组，指定路由规则
    routes: [
        // path 是 hash 地址，component 是要展示的组件
        { path: '/home', component: Home },
        { path: '/movie', component: Movie },
        { path: '/about', component: About },

    ],
});
```

- 向外共享路由实例对象

```javascript
// 向外共享路由实例对象，供其他模块导入并使用
export default router;
```

- 在 main.js 中导入并挂载路由模块

```javascript
// /main.js
import { createApp } from 'vue';
import App from './App.vue';
// 导入路由模块
import router from './router.js';

const app = createApp(App);

// 挂载路由模块
// app.use() 方法来挂载"第三方的插件模块"
app.use(router);

app.mount('#app');
```



### 路由重定向

- 路由重定向指的是：用户在访问地址 A 的时候，强制用户跳转到地址 C ，从而展示特定的组件页面。通过路由规则的 redirect 属性，指定一个新的路由地址，可以很方便地设置路由的重定向：

```javascript
const router = createRouter({
    history: createWebHashHistory(),
    routes: [
        // 其中，path 表示需要被重定向的"原地址",redirect 表示将要被重定向到的"新地址"
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/home', component: Home },
        { path: '/movie', component: Movie },
        { path: '/about', component: About },
    ],
});
```



### 路由高亮

- 可以通过如下的两种方式，将激活的路由链接进行高亮显示：
  - 使用默认的高亮 class 类
  - 自定义路由高亮的 class 类

#### 使用默认的高亮 class 类

- 被激活的路由链接，默认会应用一个叫做 router-link-active 的类名。开发者可以使用此类名选择器，为激活的路由链接设置高亮的样式：
- 注意：确保 main.js 中有导入全局样式 `import './index.css';`

```css
/* /index.css */
.router-link-active {
    background-color: red;
    color: white;
    font-weight: bold;
}
```

#### 自定义路由高亮的 class 类

- 在创建路由的实例对象时，开发者可以基于 linkActiveClass 属性，自定义路由链接被激活时所应用的类名：

```javascript
// /router.js
const router = createRouter({
    history: createWebHashHistory(),
    // 指定被激活的路由链接，会应用 router-active 这个类名
    // 默认的 router-link-active 类名会被覆盖掉
    linkActiveClass: 'router-active',
    routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/home', component: Home },
        { path: '/movie', component: Movie },
        { path: '/about', component: About },

    ],
});
```

```css
/* /index.css */

.router-active {
    background-color: red;
    color: white;
    font-weight: bold;
}
```



### 嵌套路由

- 通过路由实现组件的嵌套展示，叫做嵌套路由。

![image-20220420180002361](http://zjp.hxkj.live/MDImage/Vue/%e5%b5%8c%e5%a5%97%e8%b7%af%e7%94%b1_2022-04-20_18-00-07.png)

- 步骤
  1. 声明子路由链接和子路由占位符
  2. 在父路由规则中，通过children 属性嵌套声明子路由规则

#### 声明子路由链接和子路由占位符

- 在 About.vue 组件中，声明 tab1 和 tab2 的子路由链接以及子路由占位符。示例代码如下：

```vue
<!-- /components/MyAbout.vue -->
<template>
  <div>
    <h1>MyAbout</h1>
    <!-- 在关于页面中，声明两个子路由器链接 -->
    <router-link to="/about/tab1">tab1</router-link>&nbsp;
    <router-link to="/about/tab2">tab2</router-link>&nbsp;

    <!-- 在关于页面中，声明 tab1 和 tab2 的路由占位符 -->
    <router-view></router-view>
  </div>
</template>
<script>
export default {
  name: "MyAbout",
};
</script>
```



#### 通过 children 属性声明子路由规则

- 在 router.js 路由模块中，导入需要的组件，并使用children 属性声明子路由规则。示例代码如下：

- 注意：子路由规则的path 不要以 / 开头！
- 可设置重定向

```javascript
// /router.js
import { createRouter, createWebHashHistory } from 'vue-router';

import Home from './components/MyHome.vue';
import Movie from './components/MyMovie.vue';
import About from './components/MyAbout.vue';

// 导入 Tab1 组件
import Tab1 from './components/tabs/MyTab1.vue'
// 导入 Tab2 组件
import Tab2 from './components/tabs/MyTab2.vue'

const router = createRouter({
    history: createWebHashHistory(),
    linkActiveClass: 'router-active',
    routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/home', component: Home },
        { path: '/movie', component: Movie },
        {
            path: '/about',
            // 设置重定向，当 path 为 /about 的时候，重定位为 /about/tab1
            redirect: '/about/tab1',
            component: About,
            // 通过 children 属性嵌套子级路由规则
            children: [
                // 访问 /about/tab1 时，展示 Tab1 组件
                // 注意：path 不要以 / 开头
                { path: 'tab1', component: Tab1 },
                // 访问 /about/tab2 时，展示 Tab2 组件
                { path: 'tab2', component: Tab2 },
            ]
        },

    ],
});

// 向外共享路由实例对象，供其他模块导入并使用
export default router;
```



```vue
<!-- /components/MyAbout.vue -->
<template>
  <div>
    <h1>MyAbout</h1>
    <!-- 在关于页面中，声明两个子路由器链接 -->
    <router-link to="/about/tab1">tab1</router-link>&nbsp;
    <router-link to="/about/tab2">tab2</router-link>&nbsp;

    <!-- 在关于页面中，声明 tab1 和 tab2 的路由占位符 -->
    <router-view></router-view>
  </div>
</template>
<script>
export default {
  name: "MyAbout",
};
</script>
```



```vue
<!-- /components/tabs/MyTab1.vue -->
<template>
  <div>
    <h1>MyTab1</h1>
  </div>
</template>
<script>
export default {
  name: "MyTab1",
};
</script>
```



```vue
<!-- /components/tabs/MyTab2.vue -->
<template>
  <div>
    <h1>MyTab2</h1>
  </div>
</template>
<script>
export default {
  name: "MyTab2",
};
</script>
```



### 动态路由匹配

![image-20220420184505760](http://zjp.hxkj.live/MDImage/Vue/%e5%8a%a8%e6%80%81%e8%b7%af%e7%94%b1%e5%8c%b9%e9%85%8d_2022-04-20_18-45-11.png)

- 动态路由指的是：把 Hash 地址中可变的部分定义为参数项，从而提高路由规则的复用性。在 vue-router 中使用英文的冒号（:）来定义路由的参数项。示例代码如下：

```javascript
// /router.js
import { createRouter, createWebHashHistory } from 'vue-router';

import Home from './components/MyHome.vue';
import Movie from './components/MyMovie.vue';
import About from './components/MyAbout.vue';

import Tab1 from './components/tabs/MyTab1.vue'
import Tab2 from './components/tabs/MyTab2.vue'

const router = createRouter({
    history: createWebHashHistory(),
    linkActiveClass: 'router-active',
    routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/home', component: Home },
        // 路由中的动态参数以 : 进行声明，冒号后面的是动态参数的名称
        { path: '/movie/:id', component: Movie },
        {
            path: '/about',
            component: About,
            redirect: '/about/tab1',
            children: [
                { path: 'tab1', component: Tab1 },
                { path: 'tab2', component: Tab2 },
            ]
        },

    ],
});

// 向外共享路由实例对象，供其他模块导入并使用
export default router;
```



#### $route.params 参数对象

- 通过动态路由匹配的方式渲染出来的组件中，可以使用 $route.params 对象访问到动态匹配的参数值。

```vue
<!-- /components/MyMovie.vue -->
<template>
  <div>
    <!-- $route.params 是路由的"参数对象" -->
    <h1>MyMovie{{ $route.params.id }}</h1>
  </div>
</template>
<script>
export default {
  name: "MyMovie",
};
</script>
```



#### 使用 props 接收路由参数

- 为了简化路由参数的获取形式，vue-router 允许在路由规则中开启props 传参。示例代码如下：

```javascript
// /router.js
import { createRouter, createWebHashHistory } from 'vue-router';

import Home from './components/MyHome.vue';
import Movie from './components/MyMovie.vue';
import About from './components/MyAbout.vue';

// 导入 Tab1 组件
import Tab1 from './components/tabs/MyTab1.vue'
// 导入 Tab2 组件
import Tab2 from './components/tabs/MyTab2.vue'

const router = createRouter({
    history: createWebHashHistory(),
    linkActiveClass: 'router-active',
    routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/home', component: Home },
        // 在定义路由规则时，声明 props: true 选项
        // 即可在 Movie 组件中，以 props 的形式接收到路由规则匹配到的参数项
        { path: '/movie/:id', component: Movie, props: true },
        {
            path: '/about',
            component: About,
            redirect: '/about/tab1',
            children: [
                { path: 'tab1', component: Tab1 },
                { path: 'tab2', component: Tab2 },
            ]
        },

    ],
});

// 向外共享路由实例对象，供其他模块导入并使用
export default router;
```



```vue
<!-- /components/MyMovie.vue -->
<template>
  <div>
    <!-- 直接使用 props 中接收的路由参数-->
    <h1>MyMovie{{ id }}</h1>
  </div>
</template>
<script>
export default {
  name: "MyMovie",
  // 使用 props 接收路由规则中匹配到的参数项
  props: ["id"],
};
</script>
```



### 编程式导航

- 通过调用 API 实现导航的方式，叫做编程式导航。与之对应的，通过点击链接实现导航的方式，叫做声明式导航。例如：
  - 普通网页中点击 `<a>` 链接、vue 项目中点击 `<router-link>` 都属于声明式导航
  - 普通网页中调用 location.href 跳转到新页面的方式，属于编程式导航

#### vue-router 中的编程式导航 API

- vue-router 提供了许多编程式导航的 API，其中最常用的两个 API 分别是：
  - `this.$router.push('hash 地址')` 跳转到指定 Hash 地址，从而展示对应的组件
  - `this.$router.go(数值 n)` 实现导航历史的前进、后退

#### $router.push()

- 调用 this.$router.push() 方法，可以跳转到指定的 hash 地址，从而展示对应的组件页面。示例代码如下：

```vue
<!-- /components/MyHome.vue -->
<template>
  <div>
    <h1>MyHome</h1>
    <button @click="gotoMovie(3)">go to Movie</button>
  </div>
</template>
<script>
export default {
  name: "MyHome",
  methods: {
    // 参数 id 是电影的 id 值
    gotoMovie(id) {
      this.$router.push(`/movie/${id}`);
    },
  },
};
</script>
```



#### $router.go()

- 调用 `this.$router.go()` 方法，可以在浏览历史中进行前进和后退。示例代码如下：
- 在浏览器记录前进一步 `this.$router.go(1)`，前进n步就输入n。
- 在浏览器记录后退一步 `this.$router.go(-1)`，后退n步就输入-n。
- 刷新浏览器 `this.$router.go(0)`

```vue
<!-- /components/MyMovie.vue -->
<template>
  <div>
    <h1>MyMovie{{ id }}</h1>
    <button @click="goBack">后退</button>
  </div>
</template>
<script>
export default {
  name: "MyMovie",
  props: ["id"],
  methods: {
    goBack() {
      // 后退到之前的组件页面
      this.$router.go(-1);
    },
  },
};
</script>
```

### 命令路由

- 通过 name 属性为路由规则定义名称的方式，叫做命名路由。示例代码如下：
- 注意：命名路由的 name 值不能重复，必须保证唯一性！

```javascript
// /router.js
import { createRouter, createWebHashHistory } from 'vue-router';

import Home from './components/MyHome.vue';
import Movie from './components/MyMovie.vue';
import About from './components/MyAbout.vue';

import Tab1 from './components/tabs/MyTab1.vue'
import Tab2 from './components/tabs/MyTab2.vue'

const router = createRouter({
    history: createWebHashHistory(),
    linkActiveClass: 'router-active',
    routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/home', component: Home },
        // 使用 name 属性为当前路由规则定义一个"名称"
        { name: 'mov', path: '/movie/:id', component: Movie, props: true },
        {
            path: '/about',
            component: About,
            redirect: '/about/tab1',
            children: [
                { path: 'tab1', component: Tab1 },
                { path: 'tab2', component: Tab2 },
            ]
        },

    ],
});

export default router;
```



```vue
<!-- /components/MyHome.vue -->
<template>
  <div>
    <h1>MyHome</h1>
    <button @click="gotoMovie(3)">go to Movie</button>
    <!-- 动态绑定 :to 属性的值，使用 name 属性指定要跳转的路由规则，使用 params 属性指定要跳转携带的参数 -->
    <router-link :to="{ name: 'mov', params: { id: 3 } }"
      >to to movie</router-link
    >
  </div>
</template>
<script>
export default {
  name: "MyHome",
  methods: {
    // 参数 id 是电影的 id 值
    gotoMovie(id) {
      this.$router.push(`/movie/${id}`);
    },
  },
};
</script>
```



#### 使用命名路由实现编程式导航

- 调用 push 函数期间指定一个配置对象，name是要跳转到的路由规则、params 是携带的路由参数：

```javascript
// /router.js
import { createRouter, createWebHashHistory } from 'vue-router';

import Home from './components/MyHome.vue';
import Movie from './components/MyMovie.vue';
import About from './components/MyAbout.vue';

import Tab1 from './components/tabs/MyTab1.vue'
import Tab2 from './components/tabs/MyTab2.vue'

const router = createRouter({
    history: createWebHashHistory(),
    linkActiveClass: 'router-active',
    routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/home', component: Home },
        // 使用 name 属性为当前路由规则定义一个"名称"
        { name: 'mov', path: '/movie/:id', component: Movie, props: true },
        {
            path: '/about',
            component: About,
            redirect: '/about/tab1',
            children: [
                { path: 'tab1', component: Tab1 },
                { path: 'tab2', component: Tab2 },
            ]
        },

    ],
});

export default router;
```



```vue
<!-- /components/MyHome.vue -->
<template>
  <div>
    <h1>MyHome</h1>
    <button @click="gotoMovie(3)">go to Movie</button>
    <!-- 动态绑定 :to 属性的值，使用 name 属性指定要跳转的路由规则，使用 params 属性指定要跳转携带的参数 -->
    <router-link :to="{ name: 'mov', params: { id: 3 } }"
      >to to movie</router-link
    >
  </div>
</template>
<script>
export default {
  name: "MyHome",
  methods: {
    // 参数 id 是电影的 id 值
    gotoMovie(id) {
      this.$router.push({ name: "mov", params: { id } });
      // this.$router.push({ name: "mov", params: { id: 3 } });
    },
  },
};
</script>
```



### 导航守卫

- 导航守卫可以控制路由的访问权限。示意图如下：

![image-20220420200614350](http://zjp.hxkj.live/MDImage/Vue/%e5%af%bc%e8%88%aa%e5%ae%88%e5%8d%ab_2022-04-20_20-06-23.png)

#### 全局导航守卫

- 全局导航守卫会拦截每个路由规则，从而对每个路由进行访问权限的控制。可以按照如下的方式定义全局导航守卫：

```javascript
// /router.js
import { createRouter, createWebHashHistory } from 'vue-router';

import Home from './components/MyHome.vue';
import Movie from './components/MyMovie.vue';
import About from './components/MyAbout.vue';

import Tab1 from './components/tabs/MyTab1.vue'
import Tab2 from './components/tabs/MyTab2.vue'

const router = createRouter({
    history: createWebHashHistory(),
    linkActiveClass: 'router-active',
    routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/home', component: Home },
        { name: 'mov', path: '/movie/:id', component: Movie, props: true },
        {
            path: '/about',
            component: About,
            redirect: '/about/tab1',
            children: [
                { path: 'tab1', component: Tab1 },
                { path: 'tab2', component: Tab2 },
            ]
        },

    ],
});



// 调用路由实例对象的 beforeEach 函数，声明"全局前置守卫"
// fn 必须是一个函数，每次拦截到路由的请求，都会调用 fn 进行处理
// 因此 fn 叫做 "守卫方法"
// router.beforeEach(fn);
router.beforeEach(() => {
    console.log('ok');
});


export default router;
```

#### 守卫方法的 3 个形参

- 全局导航守卫的守卫方法中接收 3 个形参，格式为：

```javascript
// to 目标路由对象
// from 当前导航正要离开的路由对象
// next 是一个函数，表示放行
router.beforeEach((to, from, next) => {
    console.log(to);
    console.log(from);
    next();
});
```

注意：

- 在守卫方法中如果不声明 next 形参，则默认允许用户访问每一个路由！
- 在守卫方法中如果声明了 next 形参，则必须调用 next() 函数，否则不允许用户访问任何一个路由！

#### next 函数的 3 种调用方式

1. 直接放行：next()
2. 强制其停留在当前页面：next(false)
3. 强制其跳转到登录页面：next('/login')



#### 结合 token 控制后台主页的访问权限

```javascript
// 获取 token
const token = localStorage.getItem('token')
router.beforeEach((to, from, next) => {
    // 读取 token
    if (to.path === '/home' && !token) { // 想要访问"后台主页"且 token 值不存在
        // 强制其停留在当前页面
        next(false); // 不允许跳转
        // next('/login') // 强制跳转到"登陆页面"
    } else {
        // 直接放行，允许访问
        next();
    }
});
```





## vue-cli

- vue-cli（俗称：vue 脚手架）是 vue 官方提供的、快速生成 vue 工程化项目的工具。
- 特点
  - 开箱即用
  - 基于 webpack
  - 功能丰富且易于拓展
  - 支持创建 vue3 的项目

### 安装

- vue-cli 是 npm 上的一个全局包，使用 npm install 命令，即可方便的把它安装到自己的电脑上：

```bash
npm install -g @vue/cli
```

- 查询 vue-cli 的版本，验证 vue-cli 是否安装成功

```bash
vue -V
```

- 当 Windows PowerShell 不识别 vue 命令
- 以管理员身份运行 PowerShell
- 执行 set-ExecutionPolicy RemoteSigned 命令
- 输入字符 Y ，回车即可

### 创建项目

- vue-cli 提供了创建项目的两种方式：

```bash
# 基于命令行的方式创建 vue 项目
vue create 项目名称

# OR

# 基于【可视化面板】创建 vue 项目
vue ui
```



#### 基于 vue ui 创建 vue 项目

- 步骤1：在终端下运行vue ui 命令，自动在浏览器中打开创建项目的可视化面板：

![image-20220421004056211](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-41-08.png)

- 步骤2：在详情页面填写项目名称：

![image-20220421004151824](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-41-54.png)

- 步骤3：在预设页面选择手动配置项目：

![image-20220421004247615](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-42-49.png)

- 步骤4：在功能页面勾选需要安装的功能（Babel、CSS 预处理器、使用配置文件）：

![image-20220421005031755](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-50-33.png)

- 步骤5：在配置页面勾选 vue 的版本和需要的预处理器：

![image-20220421005146417](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-51-48.png)

- 步骤6：将刚才所有的配置保存为预设（模板），方便下一次创建项目时直接复用之前的配置：

![image-20220421005258830](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-53-01.png)

![image-20220421005537387](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-55-39.png)

- 步骤7：创建项目并自动安装依赖包：

![image-20220421005349967](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-53-53.png)

- vue ui 的本质：通过可视化的面板采集到用户的配置信息后，在后台基于命令行的方式自动初始化项目：

- 项目创建完成后，自动进入项目仪表盘：

![image-20220421005615980](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_00-56-18.png)



#### 基于命令行创建 vue 项目

步骤1：在终端下运行 `vue create test` 命令，基于交互式的命令行创建 vue 的项目：

```bash
vue create test
```

![image-20220421011734949](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-17-37.png)

- 步骤2：选择要安装的功能：

![image-20220421012803541](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-28-06.png)

- 步骤3：使用上下箭头选择 vue 的版本，并使用回车键确认选择：

![image-20220421012836626](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-28-38.png)

- 步骤4：使用上下箭头选择要使用的 css 预处理器，并使用回车键确认选择：

![image-20220421012916789](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-29-19.png)

- 步骤5：使用上下箭头选择如何存储插件的配置信息，并使用回车键确认选择：

![image-20220421013044568](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-30-46.png)

- 步骤6：是否将刚才的配置保存为预设：

![image-20220421013131827](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-31-34.png)

- 步骤8：开始创建项目并自动安装依赖包：

![image-20220421013859777](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-39-02.png)

- 步骤9：项目创建完成：

![image-20220421013512164](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-35-14.png)

- 运行指令，开始跑项目

```bash
# 进入项目文件夹
cd 项目的名称
cd test
# 启动项目
npm run serve
# 上线项目
npm run build
```

![image-20220421015419442](http://zjp.hxkj.live/MDImage/Vue/vueui%e5%88%9b%e5%bb%bavue%e9%a1%b9%e7%9b%ae_2022-04-21_01-54-21.png)





### 插件安装

- Vetur：VScode 中用于高亮 vue 语法
- Vue 3 Snippets：VScode 中用于提示 vue 语法



### 目录介绍

- `src\assets` ：项目中用到的存放静态资源文件，例如：css 样式表、图片资源。
- `src\components` ：程序员封装的、可复用的组件，都要放到 components 目录下。
- `src\main.js`：是项目的入口文件。整个项目的运行，要先执行 main.js。
- `src\App.vue`：是项目的根组件。UI模板结构。

### vue 项目的运行流程

- 在工程化的项目中，vue 要做的事情很单纯：通过 main.js 把 App.vue 渲染到 index.html 的指定区域中。
  - App.vue 用来编写待渲染的模板结构
  - index.html 中需要预留一个 app 区域
  - main.js 把 App.vue 渲染到了 index.html 所预留的区域中（App.vue 会替换掉 index.html 中的预留区域）



```javascript
// /main.js
// 导入 createApp 方法
import { createApp } from 'vue'
// 导入 App.vue 这个根组件，将来要把 App.vue 中的模板结构，渲染到 HTML 页面中
import App from './App.vue'

// 创建 vue 的组件应用
const app = createApp(App);
// 把 Vue 的组件应用，挂载渲染到 HTML 页面中
app.mount('#app');
```



```vue
<!-- App.vue -->
<template>
  <div>App.vue 组件</div>
</template>
```



```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <!-- 这个文件不允许调整和修改 -->
    <!-- 将来会被替换的区域 -->
    <div id="app"></div>
    <!-- 构建的 js 文件会被自动注入到这个位置 -->
    <!-- built files will be auto injected -->
  </body>
</html>

```



## 组件库

- 在实际开发中，前端开发者可以把自己封装的 .vue 组件整理、打包、并发布为 npm 的包，从而供其他人下载和使用。这种可以直接下载并在项目中使用的现成组件，就叫做 vue 组件库。

### vue 组件库和 bootstrap 的区别

- 二者之间存在本质的区别：
  - bootstrap 只提供了纯粹的原材料（ css 样式、HTML 结构以及 JS 特效），需要由开发者做进一步的组装和改造
  - vue 组件库是遵循 vue 语法、高度定制的现成组件，开箱即用

### 最常用的 vue 组件库

- PC 端
  - Element UI（https://element-plus.gitee.io/zh-CN/）
  - View UI（http://v1.iviewui.com/）
- 移动端
  - Mint UI（http://mint-ui.github.io/#!/zh-cn）
  - Vant（https://vant-contrib.gitee.io/vant/#/zh-CN/）



### Element UI

- Element UI 是饿了么前端团队开源的一套 PC 端 vue 组件库。支持在 vue2 和 vue3 的项目中使用：
  - vue3 的项目使用新版的 Element Plus（https://element-plus.gitee.io/zh-CN/）



#### 安装

```bash
npm install element-plus -S
```

#### 引入 element-ui

- 开发者可以一次性完整引入所有的 element-ui 组件，或是根据需求，只按需引入用到的 element-ui 组件：
  - 完整引入：操作简单，但是会额外引入一些用不到的组件，导致项目体积过大
  - 按需引入：操作相对复杂一些，但是只会引入用到的组件，能起到优化项目体积的目的

#### 完整引入

```javascript
// main.js
import { createApp } from 'vue'
import App from './App.vue'

// 导入 ElementUI 组件
import ElementPlus from 'element-plus'
// 导入 ElementUI 组件的样式
import 'element-plus/dist/index.css'


const app = createApp(App)
// 把 ElementUI 注册为 vue 的插件，注册后，即可在每一个组件中直接使用每一个 ElementUI 组件
app.use(ElementPlus)
app.mount('#app')
```



## axios 拦截器

- 拦截器（英文：Interceptors）会在每次发起 ajax 请求和得到响应的时候自动被触发。

![image-20220421144933707](http://zjp.hxkj.live/MDImage/Vue/axios%e6%8b%a6%e6%88%aa%e5%99%a8_2022-04-21_14-49-40.png)

- 应用场景
  - Token 身份认证
  - Loading 效果



### 全局配置 axios

```javascript
// /main.js
import { createApp } from 'vue';
import App from './App.vue';
// 导入 axios 模块
import axios from 'axios';

const app = createApp(App);
// 为 axios 配置请求的根路径
axios.defaults.baseURL = 'https://www.escook.cn';
// 将 axios 挂载为 app 的全局自定义属性
// 每个组件可以通过 this 直接访问到全局挂载的自定义属性，vue 的内置成员都以 $ 开头
app.config.globalProperties.$http = axios;
app.mount('#app');
```



### 配置请求拦截器

- 通过 axios.interceptors.request.use(成功的回调, 失败的回调) 可以配置请求拦截器。示例代码如下：
- 注意：失败的回调函数可以被省略！

```javascript
// 请求拦截器
axios.interceptors.request.use(config => {
    return config
}, error => {
    return Promise.reject(error)
})
```



#### Token 认证

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import axios from 'axios';


const app = createApp(App)
app.use(ElementPlus)

axios.defaults.baseURL = 'https://www.escook.cn';
// 请求拦截器
axios.interceptors.request.use(config => {
    // 为当前请求配置 Token 认证字段
    config.headers.Authorization = 'Bearer xxx'
    // 这是固定写法，成功一定要返回 config
    return config
})


app.config.globalProperties.$http = axios;

app.mount('#app')
```



#### 展示 Loading 效果

- 借助于 element ui 提供的 Loading 效果组件可以方便的实现 Loading 效果的展示：

```javascript
// /main.js
import { createApp } from 'vue'
import App from './App.vue'
import ElementPlus, { ElLoading } from 'element-plus'
import 'element-plus/dist/index.css'

import axios from 'axios';

const app = createApp(App)
app.use(ElementPlus)

axios.defaults.baseURL = 'https://www.escook.cn';
// 声明变量，用来存储 loading 组件的实例对象
let loadingInstance = null;
// 配置请求拦截器
axios.interceptors.request.use(config => {
    // 调用 Loading 组件的 service() 方法，创建 Loading 组件的实例，并全屏展示 loading 效果
    loadingInstance = ElLoading.service({ fullscreen: true })
    return config
})

app.config.globalProperties.$http = axios;

app.mount('#app')
```



### 配置响应拦截器

- 通过 axios.interceptors.response.use(成功的回调, 失败的回调) 可以配置响应拦截器。示例代码如下：

- 注意：失败的回调函数可以被省略！

```javascript
// 响应拦截器
axios.interceptors.response.use(response => {
    return response;
}, function(error) {
    return Promise.reject(error);
})
```

#### 关闭 Loading 效果

- 调用 Loading 实例提供的 close() 方法即可关闭 Loading 效果，示例代码如下：

```javascript
// /main.js
import { createApp } from 'vue'
import App from './App.vue'
import ElementPlus, { ElLoading } from 'element-plus'
import 'element-plus/dist/index.css'

import axios from 'axios';

const app = createApp(App)
app.use(ElementPlus)

axios.defaults.baseURL = 'https://www.escook.cn';
// 声明变量，用来存储 loading 组件的实例对象
let loadingInstance = null;
// 配置请求拦截器
axios.interceptors.request.use(config => {
    // 调用 Loading 组件的 service() 方法，创建 Loading 组件的实例，并全屏展示 loading 效果
    loadingInstance = ElLoading.service({ fullscreen: true })
    return config
})

// 响应拦截器
axios.interceptors.response.use(response => {
    // 调用 Loading 实例的 close 方法即可关闭 Loading 效果
    loadingInstance.close()
    return response
})

app.config.globalProperties.$http = axios;

app.mount('#app')
```

