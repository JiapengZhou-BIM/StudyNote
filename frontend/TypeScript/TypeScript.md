# TypeScript

## 介绍

- TypeScript 是由微软开发的一款开源的编程语言。
- TypeScript 是 Javascript 的超集，遵循最新的 ES6、Es5 规范。TypeScript 扩展了 JavaScript的语法。
- TypeScript 更像后端 java、C#这样的面向对象语言，可以让 js 开发大型企业项目。

- 谷歌也在大力支持 Typescript 的推广，谷歌的 angular2.x+就是基于 Typescript 语法。

- 最新的 Vue 、React 也可以集成 TypeScript。
- Nodejs 框架 Nestjs、midway 中用的就是 TypeScript 语法。

![image-20220427153520004](http://zjp.hxkj.live/MDImage/TypeScript/TypeScript_2022-04-27_15-35-34.png)

## 安装和运行

- 打开终端，运行如下代码

``` bash
npm i -g typescript
```

- 检测安装是否成功

```bash
tsc -v
```

- 由于浏览器不支持 ts 和 es6 语法，需要编译成 js es5 语法

```bash
tsc .\helloworld.ts
```



## Typescript 开发工具 Vscode 自动编译 .ts 文件

- 创建 `tsconfig.json` 配置文件

```bash
tsc --init
```

- 修改配置文件中 `js` 输出路径

```json
"outDir": "./js",
```

- vscode 中 终端->运行任务->typescript->tsc:监视-tsconfig.jso



## 数据类型

- typescript 中为了使编写的代码更规范，更有利于维护，增加了类型校验，在 typescript中主要给我们提供了以下数据类型
  - 布尔类型（boolean）
  - 数字类型（number）
  - 字符串类型(string)
  - 数组类型（array）
  - 元组类型（tuple）
  - 枚举类型（enum）
  - 任意类型（any）
  - null 和 undefined
  - void类型
  - never类型

- 推荐使用 ES6 语法，使用  `var`  、 `let` 、 `const`

- 布尔类型

```typescript
let flag: boolean = true
flag = false
```

- 数字类型，无整型和浮点型区分

```typescript
let a: number = 100
a = 20.5
```

- 字符串类型

```typescript
let str: string = 'this is ts'
str = '你好ts'
```

- 数组类型，数组除非使用 any 类型否则只能是一种类型，

```typescript
let arr: number[] = [1,2,3]
let arr: string[] = ['php', 'js', 'golang']
let arr: any[] = ['123', 123]
```

```typescript
let arr: Array<number> = [1, 2, 3]
let arr: Array<string> = ['php', 'js', 'golang']
```

- 元组类型，可以指定数组中元素多种类型

```typescript
let arr: [string, number, boolean] = ['ts', 3.5, true]
```

- 枚举类型

```typescript
enum Flag {
  success = 2,
  error = -2,
}

let f: Flag = Flag.success
console.log(f) // 返回：2

enum Color {
  red,
  blue,
  green,
}

let c: Color = Color.blue
console.log(c) // 返回：1
```

- 任意类型

```typescript
let num: any = 123
num = '123'
```

- null 和 undefined

```typescript
let num: undefined
console.log(num)

// let num: number
// console.log(num) // 报错

// 类型联合
let num: number | null | undefined
num = 123
console.log(num)
```

- void 类型，一般用于定义方法的时候方法没有返回值

```typescript
function run(): void {
  console.log('run')
}
```

- never 类型，是其他类型。（包括 null 和 undefined）的子类型，代表从不会出现的值，这意味着声明 never 的变量只能被 never 类型所赋值

```typescript
let a: never

a = (() => {
  throw new Error('错误')
})()
```



## 函数

### *ES5 函数

- 函数声明法

```typescript
function run() {
  return 'run'
}

// 调用方法
alert(run()) // 返回：'run'
```

- 匿名函数法

```typescript
var fun = function () {
  return 'fun'
}

// 调用方法
alert(fun()) // 返回：'fun'
```



### 函数

- 函数声明法

```typescript
function run(): string {
  return 'run'
}

// 调用方法
alert(run()) // 返回：'run'
```

- 匿名函数法

```typescript
var fun = function (): string {
  return 'fun'
}

// 调用方法
alert(fun()) // 返回：'fun'
```

- 定义方法传参

```typescript
function getInfo(name: string, age: number): string {
  return `${name} --- ${age}`
}

// 调用方法
alert(getInfo('zs', 20)) // 返回：'zs --- 20'
```

- 匿名函数传参

```typescript
var getInfo = function (name: string, age: number): string {
  return `${name} --- ${age}`
}

alert(getInfo('zs', 20)) // 返回：'zs --- 20'
```

- 方法的可选参数
- 注意：可选参数必须配置到参数的最后面

```typescript
function getInfo(name: string, age?: number): string {
  if (age) {
    return `${name} --- ${age}`
  } else {
    return `${name} --- 年龄保密`
  }
}

alert(getInfo('zs')) // 返回：'zs --- 年龄保密'
alert(getInfo('zs', 20)) // 返回：'zs --- 20'
```

- 方法的默认参数

```typescript
function getInfo(name: string, age: number = 20): string {
  return `${name} --- ${age}`
}

alert(getInfo('zs')) // 返回：'zs --- 20'
```

- 方法的可变参数

```typescript
// 拓展运算符，接收新传过来的值
function sum(...result: number[]): number {
  let sum = 0
  for (let i = 0; i < result.length; i++) {
    sum += result[i]
  }
  return sum
}

alert(sum(1, 2, 3, 4, 5))
```

- 函数重载

```typescript
function getInfo(name: string): string

function getInfo(age: number): string

function getInfo(str: any): any {
  if (typeof str === 'string') {
    return '我叫' + str
  } else {
    return '我的年龄是' + str
  }
}

alert(getInfo('zs')) // 返回：'我叫zs'
alert(getInfo(20)) // 返回：'我的年龄是20'

```



```typescript
function getInfo(name: string): string

function getInfo(name: string, age: number): string

function getInfo(str: any, age?: any): any {
  if (age) {
    return '我叫' + str + '，我的年龄是' + age
  } else {
    return '我叫' + str
  }
}

alert(getInfo('zs')) // 返回：'我叫zs'
alert(getInfo('zs', 20)) // 返回：'我叫zs，我的年龄是20'

```

- 箭头函数
- 注意：箭头函数里面的 this 指向上下文

```typescript
setTimeout(() => {
  alert('run')
}, 1000)
```



## 类

### *ES5 的类

```javascript
// 构造类
function Preson() {
  this.name = '张三'
  this.age = 20

  this.run = function () {
    alert(this.name + '在运动')
  }
}

// 静态方法
Preson.getInfo = function () {
  alert('我是静态方法')
}

// 原型链拓展属性和方法
// 原型链上面的属性会被多个实例共享，构造函数不会
Preson.prototype.set = '男'
Preson.prototype.work = function () {
  alert(this.name + '在工作')
}

// 实例化类
var p = new Preson()
// 调用实例方法
p.run() // 返回：'张三在运动'
p.work() // 返回：'张三在工作'
// 调用静态方法
Preson.getInfo() // 返回：'我是静态方法'
```

### *ES5 的类继承

- 对象冒充实现类继承

```javascript
// 构造类
function Preson() {
  this.name = '张三'
  this.age = 20

  this.run = function () {
    alert(this.name + '在运动')
  }
}

// 静态方法
Preson.getInfo = function () {
  alert('我是静态方法')
}

// 原型链拓展属性和方法
Preson.prototype.set = '男'
Preson.prototype.work = function () {
  alert(this.name + '在工作')
}

// Web 类，继承 Person 类，使用对象冒充的继承模式
function Web() {
  Preson.call(this) // 对象冒充实现继承
}

var w = new Web()
// 对象冒充可以继承构造函数里面的属性和方法
w.run() // 返回：'张三在运动'

// 但是没法继承原型链上面的属性和方法
w.work() // 报错

```

- 原型链实现类继承

```javascript
// 构造类
function Preson() {
  this.name = '张三'
  this.age = 20

  this.run = function () {
    alert(this.name + '在运动')
  }
}

// 静态方法
Preson.getInfo = function () {
  alert('我是静态方法')
}

// 原型链拓展属性和方法
Preson.prototype.set = '男'
Preson.prototype.work = function () {
  alert(this.name + '在工作')
}

// Web 类，继承 Person 类，使用原型链继承模式
function Web() {}
Web.prototype = new Preson() // 使用原型链实现继承
var w = new Web()
// 原型链可以继承构造函数和原型链里面的属性和方法
w.run() // 返回：'张三在运动'

// 原型链可以继承构造函数和原型链里面的属性和方法
w.work() // 返回：'张三在工作'

```

- 注意：原型链继承在实例化的时候没法给父类传参，代码示例如下

```javascript
// 构造类
function Preson(name, age) {
  this.name = name
  this.age = age

  this.run = function () {
    alert(this.name + '在运动')
  }
}

// 静态方法
Preson.getInfo = function () {
  alert('我是静态方法')
}

// 原型链拓展属性和方法
Preson.prototype.set = '男'
Preson.prototype.work = function () {
  alert(this.name + '在工作')
}

// Web 类，继承 Person 类，使用原型链继承模式
function Web(name, age) {}
Web.prototype = new Preson() // 使用原型链实现继承
var w = new Web('张三', 20) // 实例化子类的时候没法给父类传参
// 原型链可以继承构造函数和原型链里面的属性和方法
w.run() // 返回：'underfined在运动'

// 原型链可以继承构造函数和原型链里面的属性和方法
w.work() // 返回：'underfined在工作'
```

- 原型链+对象冒充的组合

```javascript
// 构造类
function Preson(name, age) {
  this.name = name
  this.age = age

  this.run = function () {
    alert(this.name + '在运动')
  }
}

// 静态方法
Preson.getInfo = function () {
  alert('我是静态方法')
}

// 原型链拓展属性和方法
Preson.prototype.set = '男'
Preson.prototype.work = function () {
  alert(this.name + '在工作')
}

// Web 类，继承 Person 类，使用原型链+对象冒充的组合继承模式
function Web(name, age) {
  Preson.call(this, name, age) // 对象冒充继承，可以继承构造函数里面的属性和方法，实例化子类可以给父类传参
}
// Web.prototype = new Preson()
Web.prototype = Preson.prototype // 使用原型链实现继承
var w = new Web('张三', 20)
// 原型链可以继承构造函数和原型链里面的属性和方法
w.run() // 返回：'张三在运动'

// 原型链可以继承构造函数和原型链里面的属性和方法
w.work() // 返回：'张三在工作'

```

### 类

- 定义类

```typescript
class Person {
  // 构造函数，实例化的时候触发的方法
  constructor(name: string) {
    this.name = name
  }
  name: string // 属性  前面省略 public 关键词
  // 方法
  run(): void {
    alert(this.name)
  }
}

let p: Person = new Person('张三')
p.run()
```

- 修改属性

```typescript
class Person {
  constructor(name: string) {
    this.name = name
  }
  name: string
  // 有返回值方法
  getName(): string {
    return this.name
  }
  // 无返回值方法，可修改属性值
  setName(name: string): void {
    this.name = name
  }
}

let p: Person = new Person('张三')
alert(p.getName()) // 返回：'张三'
p.setName('李四')
alert(p.getName()) // 返回：'李四'
```

### 类继承

- 子类会继承父类的属性和方法

```typescript
class Person {
  constructor(name: string) {
    this.name = name
  }
  name: string

  run(): string {
    return `${this.name}在运动`
  }
}

// 继承父类
class Web extends Person {
  constructor(name: string) {
    super(name) // 初始化父类的构造函数
  }
  work(): string {
    return `${this.name}在工作`
  }
}

let w = new Web('张三')
alert(w.run()) // 返回：'张三在运动'
alert(w.work()) // 返回：'张三在工作'
```

- 如果子类和父类方法名重复，则使用子类的方法

```typescript
class Person {
  constructor(name: string) {
    this.name = name
  }
  name: string

  run(): string {
    return `${this.name}在运动`
  }
}

// 继承父类
class Web extends Person {
  constructor(name: string) {
    super(name) // 初始化父类的构造函数
  }
  run(): string {
    return `${this.name}在运动-子类`
  }
  work(): string {
    return `${this.name}在工作`
  }
}

let w = new Web('张三')
alert(w.run()) // 返回：'张三在运动-子类'
alert(w.work()) // 返回：'张三在工作'
```

### 类修饰符

- 定义属性的时候有三种修饰符
  - `public`：公有，在类里面、子类、类外面都可以访问
  - `protected`：保护类型，在类里面和子类都可以访问，在类外部没法访问
  - `private`：在类里面可以访问，在子类和类外部都没法访问
- 属性如果不加修饰符，默认就是公有 `public`

#### public

```typescript
class Person {
  constructor(name: string) {
    this.name = name
  }
  public name: string

  run(): string {
    // 类里面使用
    return `${this.name}在运动`
  }
}

// 类外部使用
let p = new Person('李四')
alert(p.name) // 返回：'李四'

class Web extends Person {
  constructor(name: string) {
    super(name)
  }
  run(): string {
    // 子类中使用
    return `${this.name}在运动-子类`
  }
}
```

#### protected

```typescript
class Person {
  constructor(name: string) {
    this.name = name
  }
  protected name: string

  run(): string {
    // 类里面使用
    return `${this.name}在运动`
  }
}

// 类外部使用
let p = new Person('李四')
alert(p.name) // 报错

class Web extends Person {
  constructor(name: string) {
    super(name)
  }
  run(): string {
    // 子类中使用
    return `${this.name}在运动-子类`
  }
}
```

#### private

```typescript
class Person {
  constructor(name: string) {
    this.name = name
  }
  private name: string

  run(): string {
    // 类里面使用
    return `${this.name}在运动`
  }
}

// 类外部使用
let p = new Person('李四')
alert(p.name) // 报错

class Web extends Person {
  constructor(name: string) {
    super(name)
  }
  run(): string {
    // 报错
    return `${this.name}在运动-子类`
  }
}
```

### 静态属性和方法

- 使用 `static` 修饰

```typescript
class Person {
  constructor(name: string) {
    this.name = name
  }
  name: string
  // 静态属性
  static age: number = 20
  // 实例方法
  run(): string {
    return `${this.name}在运动`
  }
  // 静态方法
  static print() {
    // 调用静态属性
    alert(Person.age)
  }
}

let p = new Person('张三')
// 调用实例方法
p.run()
// 调用静态方法
Person.print()
```

### 多态

- 父类定义一个方法不去实现，让继承它的子类去实现，每一个子类有不同的表现
- 多态也是继承的一种表现，多态也是继承

```typescript
class Animal {
  constructor(name: string) {
    this.name = name
  }
  name: string
  // 具体吃什么不知道，具体吃什么让继承它的子类去实现，每一个子类的表现不一样，这叫多态
  eat(): void {
    console.log('吃的方法')
  }
}

class Dog extends Animal {
  constructor(name: string) {
    super(name)
  }
  eat() {
    return this.name + '吃肉'
  }
}

class Cat extends Animal {
  constructor(name: string) {
    super(name)
  }
  eat() {
    return this.name + '吃老鼠'
  }
}
```

### 抽象类

- typescript 中的抽象类，它是提供其他类继承的基类，不能直接被实例化
- 用 `abstract` 关键字定义抽象类和抽象方法，抽象类中的抽象方法不包含具体实现并且必须在派生类中实现。

- `abstract` 抽象方法只能放在抽象类里面
- 抽象类和抽象方法来定义标准

```typescript
// Animal 这个类要求它的子类必须包含 eat 方法
abstract class Animal {
  constructor(name: string) {
    this.name = name
  }
  name: string
  // 抽象方法在抽象类中不需要去实现，子类中必须实现
  abstract eat(): any
  // 非抽象方法，子类可以不去实现
  run() {
    return this.name + '在跑步'
  }
}

// 抽象类无法被实例化，报错
// let an = new Animal('猫')

// 抽象类的子类，必须实现抽象类里面的抽象方法
class Dog extends Animal {
  constructor(name: string) {
    super(name)
  }
  eat() {
    return this.name + '吃肉'
  }
}

let d = new Dog('小花')
alert(d.eat()) // 返回：'小花吃肉'
```

### 接口

- 接口的作用：在面向对象的编程中，接口是一种规范的定义，它定义了行为和动作的规范，在程序设计里面，接口起到一种限制和规范的作用。接口定义了某一批类所需要遵守的规范，接口不关心这些类的内部状态数据，也不关心这些类里方法的实现细节，它只规定这批类里必须提供某些方法，提供这些方法的类就可以满足实际需要。 typescrip 中的接口类似于 java，同时还增加了更灵活的接口类型，包括属性、函数、可索引和类等。

- 定义标准
- typesrcipt 中的接口分为：
  - 属性类接口
  - 函数类型接口
  - 可索引接口
  - 类类型接口
  - 接口扩展

#### 属性类型接口

```typescript
// 就是传入对象的约束，属性接口，可以批量
interface FullName {
  firstName: string
  secondName: string
}
function printName(name: FullName) {
  // 必须传入对象 firstName  secondName
  console.log(name.firstName + '--' + name.secondName)
}

// printName('123') // 错误
// printName({'123'}) // 错误
// 定义在外部的时候，只要对象中包含接口中必须的内容就可以
let obj = {
  age: 20,
  firstName: '张',
  secondName: '三',
}
printName(obj) // 返回：张--三
// 定义在内部，只能是接口中的内容
// printName({ firstName: '张', secondName: '三', age: 20 }) // 报错
printName({ firstName: '张', secondName: '三' }) // 返回：张--三

function printInfo(name: FullName) {
  // 无法调用接口以外的值
  // console.log(name.firstName + name.secondName + name.age) // 报错
  console.log(name.firstName + name.secondName)
}
printInfo(obj) // 返回：张三
```

- 可选属性

```typescript
interface FullName {
  firstName: string
  // 可选属性
  secondName?: string
}

function getName(name: FullName) {
  console.log(name)
}

// 传入接口时，顺序可以不与接口一致
getName({
  secondName: '四',
  firstName: '李',
})

getName({
  firstName: '张三',
})
```

- 案例：封装 ajax

```typescript
interface Config {
  type: string
  url: string
  data?: string
  dataType: string
}

//原生js封装的ajax
function ajax(config: Config) {
  var xhr = new XMLHttpRequest()

  xhr.open(config.type, config.url, true)

  xhr.send(config.data)

  xhr.onreadystatechange = function () {
    if (xhr.readyState == 4 && xhr.status == 200) {
      console.log('chengong')

      if (config.dataType == 'json') {
        console.log(JSON.parse(xhr.responseText))
      } else {
        console.log(xhr.responseText)
      }
    }
  }
}

ajax({
  type: 'get',
  data: 'name=zhangsan',
  url: 'http://a.itying.com/api/productlist', //api
  dataType: 'json',
})

```

#### 函数类型接口

- 对方法传入的参数以及返回值进行约束，批量约束

```typescript
// 加密的函数类型接口
interface encrypt {
  (key: string, value: string): string
}

var md5: encrypt = function (key: string, value: string): string {
  return key + value
}
// 函数形参可以不一致
// var md5: encrypt = function (a: string, value: string): string {
//   return a + value
// }
console.log(md5('name', 'zs')) // 返回：namezs
```

#### 可索引接口

- 数组、对象的约束（不常用）

```typescript
// 对数组的约束
interface UserArr {
  // 索引值是 number类型，数组的索引值是 number
  // 值是 string 类型
  [index: number]: string
}

var arr: UserArr = ['aaa', 'bbb']

console.log(arr[0])

// 对对象的约束
interface UsrObj {
  // 索引值是 string类型，对象的索引值是 string
  // 值是 string 类型
  [index: string]: string
}

var arr1: UsrObj = { name: 'zs', age: '20' }
```



#### 类类型接口

- 对类的约束和抽象类有点相似

```typescript
// 属性类型接口和函数接口的整合
interface Animal {
  name: string
  eat(food: string): void
}

class Dog implements Animal {
  constructor(name: string) {
    this.name = name
  }
  name: string
  eat(food: string): void {
    console.log(this.name + '吃' + food)
  }
}

let d = new Dog('小黑')
d.eat('粮食') // 小黑吃粮食
```



#### 接口扩展

- 接口可以继承接口

```typescript
interface Animal {
  eat(): void
}
// 人接口继承动物接口
interface Person extends Animal {
  work(): void
}

class Web implements Person {
  constructor(name: string) {
    this.name = name
  }
  name: string

  eat(): void {
    console.log(this.name + '吃饭')
  }
  work(): void {
    console.log(this.name + '工作')
  }
}

let web = new Web('张三')
web.eat() // 返回：'张三吃饭'
web.work() // 返回：'张三工作'
```

- 类可以同时继承接口和类

```typescript
interface Animal {
  eat(): void
}
// 人接口继承动物接口
interface Person extends Animal {
  work(): void
}

// 程序员类
class programmer {
  constructor(name: string) {
    this.name = name
  }
  name: string
  coding(): void {
    return console.log(this.name + '在敲代码')
  }
}

// 前端类，继承 programmer 类，实现 Person 接口
class Web extends programmer implements Person {
  constructor(name: string) {
    super(name)
  }

  eat(): void {
    console.log(this.name + '吃饭')
  }
  work(): void {
    console.log(this.name + '工作')
  }
}

let web = new Web('张三')
web.coding() // 返回：张三在敲代码
web.eat() // 返回：'张三吃饭'
web.work() // 返回：'张三工作'
```



