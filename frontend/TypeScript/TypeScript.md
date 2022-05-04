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



## 泛型

- 泛型：软件工程中，我们不仅要创建一致的定义良好的API，同时也要考虑可重用性。 组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。
- 在像 C# 和 Java 这样的语言中，可以使用泛型来创建可重用的组件，一个组件可以支持多种类型的数据。 这样用户就可以以自己的数据类型来使用组件。

- 通俗理解：泛型就是解决 类 接口 方法的复用性、以及对不特定数据类型的支持(类型校验)

### 泛型函数

```typescript
// T 表示泛型，具体什么类型是调用这个方法的时候决定的
function getData<T>(value: T): T {
  return value
}

console.log(getData<number>(123)) // 返回：123
console.log(getData<string>('123')) // 返回：'123'

```



### 泛型类

- 比如有个最小堆算法，需要同时支持返回数字和字符串 a  -  z两种类型。  通过类的泛型来实现

```typescript
class MinClas1<T> {
  public list: T[] = []

  add(value: T): void {
    this.list.push(value)
  }

  min(): T {
    var minNum = this.list[0]
    for (var i = 0; i < this.list.length; i++) {
      if (minNum > this.list[i]) {
        minNum = this.list[i]
      }
    }
    return minNum
  }
}

var m1 = new MinClas1<number>() /*实例化类 并且制定了类的T代表的类型是number*/
m1.add(11)
m1.add(3)
m1.add(2)
alert(m1.min())
var m2 = new MinClas1<string>() /*实例化类 并且制定了类的T代表的类型是string*/

m2.add('c')
m2.add('a')
m2.add('v')
alert(m2.min())

```

### 泛型接口

- 方式一：

```typescript
interface ConfigFn {
  <T>(value: T): T
}

var getData: ConfigFn = function <T>(value: T): T {
  return value
}

console.log(getData<string>('张三')) // 返回：'张三'

console.log(getData<number>(1234)) // 返回：1234

```

- 方式二：

```typescript
interface ConfigFn<T> {
  (value: T): T
}

function getData<T>(value: T): T {
  return value
}

var myGetData: ConfigFn<string> = getData

console.log(myGetData('20')) // 返回：'20'

// console.log(myGetData(20)) // 错误

```



### 把类作为参数类型的泛型类

1、定义个类

2、把类作为参数来约束数据传入的类型 



- 未使用泛型类，当传入不同类的时候，需要多次写 MysqlDb 这个类中 add 方法

```typescript
// 定义一个User的类这个类的作用就是映射数据库字段
// 然后定义一个 MysqlDb的类这个类用于操作数据库
// 然后把User类作为参数传入到MysqlDb中

class User {
  username: string | undefined
  pasword: string | undefined
}

class MysqlDb {
  add(user: User): boolean {
    console.log(user) // 返回：User 实例对象
    return true
  }
}
var u = new User()
u.username = '张三'
u.pasword = '123456'
var Db = new MysqlDb()
Db.add(u)

```

- 使用泛型类

```typescript
//定义操作数据库的泛型类
class MysqlDb<T> {
  add(info: T): boolean {
    console.log(info)
    return true
  }
  updated(info: T, id: number): boolean {
    console.log(info)

    console.log(id)

    return true
  }
}

//想给User表增加数据

// 1、定义一个User类 和数据库进行映射

class User {
  username: string | undefined
  pasword: string | undefined
}
var u = new User()
u.username = '张三'
u.pasword = '123456'
var Db = new MysqlDb<User>()
Db.add(u)

//2、相关ArticleCate增加数据  定义一个ArticleCate类 和数据库进行映射

class ArticleCate {
  title: string | undefined
  desc: string | undefined
  status: number | undefined
  constructor(params: {
    title: string | undefined
    desc: string | undefined
    status?: number | undefined
  }) {
    this.title = params.title
    this.desc = params.desc
    this.status = params.status
  }
}
//增加操作
var a = new ArticleCate({
  title: '分类',
  desc: '1111',
  status: 1,
})

//类当做参数的泛型类
var Db1 = new MysqlDb<ArticleCate>()
Db1.add(a)

//修改数据
var b = new ArticleCate({
  title: '分类111',
  desc: '2222',
})

b.status = 0
var Db2 = new MysqlDb<ArticleCate>()
Db2.updated(b, 12)

```





## 综合使用

- 功能：定义一个操作数据库的库  支持 Mysql Mssql  MongoDb
- 要求1：Mysql MsSql  MongoDb功能一样  都有 add  update  delete  get方法   
- 注意：约束统一的规范、以及代码重用
- 解决方案：需要约束规范所以要定义接口 ，需要代码重用所以用到泛型
  - 接口：在面向对象的编程中，接口是一种规范的定义，它定义了行为和动作的规范
  - 泛型 通俗理解：泛型就是解决 类 接口 方法的复用性

```typescript
/*

功能：定义一个操作数据库的库  支持 Mysql Mssql  MongoDb

要求1：Mysql MsSql  MongoDb功能一样  都有 add  update  delete  get方法    

注意：约束统一的规范、以及代码重用

解决方案：需要约束规范所以要定义接口 ，需要代码重用所以用到泛型

    1、接口：在面向对象的编程中，接口是一种规范的定义，它定义了行为和动作的规范

    2、泛型 通俗理解：泛型就是解决 类 接口 方法的复用性、


*/

interface DBI<T> {
  add(info: T): boolean;
  update(info: T, id: number): boolean;
  delete(id: number): boolean;
  get(id: number): any[];
}

//定义一个操作mysql数据库的类       注意：要实现泛型接口 这个类也应该是一个泛型类

class MysqlDb<T> implements DBI<T> {
  constructor() {
    console.log("数据库建立连接");
  }
  add(info: T): boolean {
    console.log(info);

    return true;
  }

  update(info: T, id: number): boolean {
    throw new Error("Method not implemented.");
  }
  delete(id: number): boolean {
    throw new Error("Method not implemented.");
  }
  get(id: number): any[] {
    var list = [
      {
        title: "xxxx",
        desc: "xxxxxxxxxx",
      },
      {
        title: "xxxx",
        desc: "xxxxxxxxxx",
      },
    ];

    return list;
  }
}

//定义一个操作mssql数据库的类

class MsSqlDb<T> implements DBI<T> {
  constructor() {
    console.log("数据库建立连接");
  }
  add(info: T): boolean {
    console.log(info);
    return true;
  }
  update(info: T, id: number): boolean {
    throw new Error("Method not implemented.");
  }
  delete(id: number): boolean {
    throw new Error("Method not implemented.");
  }
  get(id: number): any[] {
    var list = [
      {
        title: "xxxx",
        desc: "xxxxxxxxxx",
      },
      {
        title: "xxxx",
        desc: "xxxxxxxxxx",
      },
    ];

    return list;
  }
}

//操作用户表   定义一个User类和数据表做映射

/*

class User{
    username:string | undefined;
    password:string | undefined;
}


var u=new User();
u.username='张三111';
u.password='123456';


var oMysql=new MysqlDb<User>(); //类作为参数来约束数据传入的类型 
oMysql.add(u);

*/

class User {
  username: string | undefined;
  password: string | undefined;
}

var u = new User();
u.username = "张三2222";
u.password = "123456";

var oMssql = new MsSqlDb<User>();
oMssql.add(u);

//获取User表 ID=4的数据
var data = oMssql.get(4);
console.log(data);

```



## 模块

- 关于术语的一点说明： 请务必注意一点，TypeScript 1.5 里术语名已经发生了变化。 “内部模块”现在称做“命名空间”。 “外部模块”现在则简称为“模块” 模块在其自身的作用域里执行，而不是在全局作用域里；这意味着定义在一个模块里的变量，函数，类等等在模块外部是不可见的，除非你明确地使用 export 形式之一导出它们。 相反，如果想使用其它模块导出的变量，函数，类，接口等的时候，你必须要导入它们，可以使用 import 形式之一。
- 我们可以把一些公共的功能单独抽离成一个文件作为一个模块。模块里面的变量 函数 类等默认是私有的，如果我们要在外部访问模块里面的数据（变量、函数、类），我们需要通过 export 暴露模块里面的数据（变量、函数、类...）。暴露后我们通过 import 引入模块就可以使用模块里面暴露的数据（变量、函数、类...）。

### export 直接输出

- 使用 export 直接暴露模块里面的数据

```typescript
// modules/db.ts
var dbUrl = "xxxxxx";

export function getData(): any[] {
  console.log("获取数据库的数据111");

  return [
    {
      title: "121312",
    },
    {
      title: "121312",
    },
  ];
}

export function save() {
  console.log("保存数据成功");
}

```



- 使用 import…from 引入模块里面的暴露的数据，需解构

```typescript
// idnex.ts
import { getData,save } from './modules/db';

getData();

save();
```







### 先定义再 export 输出

- 暴露的第二种方式

```typescript
var dbUrl = "xxxxxx";

function getData(): any[] {
  console.log("获取数据库的数据111");

  return [
    {
      title: "121312",
    },
    {
      title: "121312",
    },
  ];
}

function save() {
  console.log("保存数据成功");
}

export { dbUrl, getData, save };

```



- 使用 import…from 引入模块里面的暴露的数据，需解构

```typescript
// idnex.ts
import { getData,save } from './modules/db';

getData();

save();
```



### 导入取别名

```typescript
// idnex.ts
import { dbUrl, getData as get, save } from "./modules/db";

console.log(dbUrl);

get();
```



### export default 默认导出

- export default 用于规定模块的默认对外接口
- 很显然默认对外接口只能有一个，所以 export default 在同一个模块中只能出现一次
- export default只能直接输出，不能先定义再输出。
- 其在 import 方式上也和 export 存在一定区别



- 当导出单个函数或变量的时候

```typescript
// /modules/db.ts
function getData(): any[] {
  console.log("获取数据库的数据111");

  return [
    {
      title: "121312",
    },
    {
      title: "121312",
    },
  ];
}

export default getData;

```



- 使用 import…from 引入模块里面的暴露的数据，直接导入，无需解构

```typescript
// idnex.ts
import getData from "./modules/db";
getData();

```



- 当以对象形式导出的时候

```typescript
var dbUrl = "xxxxxx";

function getData(): any[] {
  console.log("获取数据库的数据111");

  return [
    {
      title: "121312",
    },
    {
      title: "121312",
    },
  ];
}

function save() {
  console.log("保存数据成功");
}

export default { dbUrl, getData, save };

```



- 使用 import…from 引入模块里面的暴露的数据，导入使用对象接收，使用则使用对象的属性或者方法

```typescript
// idnex.ts
import db from "./modules/db";
console.log(db.dbUrl);

db.getData();
```



### 使用模块封装数据库类

- 定义数据库类

```typescript
interface DBI<T> {
  add(info: T): boolean;
  update(info: T, id: number): boolean;
  delete(id: number): boolean;
  get(id: number): any[];
}

//定义一个操作mysql数据库的类       注意：要实现泛型接口 这个类也应该是一个泛型类

export class MysqlDb<T> implements DBI<T> {
  constructor() {
    console.log("数据库建立连接");
  }
  add(info: T): boolean {
    console.log(info);

    return true;
  }

  update(info: T, id: number): boolean {
    throw new Error("Method not implemented.");
  }
  delete(id: number): boolean {
    throw new Error("Method not implemented.");
  }
  get(id: number): any[] {
    var list = [
      {
        title: "xxxx",
        desc: "xxxxxxxxxx",
      },
      {
        title: "xxxx",
        desc: "xxxxxxxxxx",
      },
    ];

    return list;
  }
}

//定义一个操作mssql数据库的类

export class MsSqlDb<T> implements DBI<T> {
  constructor() {
    console.log("数据库建立连接");
  }
  add(info: T): boolean {
    console.log(info);
    return true;
  }
  update(info: T, id: number): boolean {
    throw new Error("Method not implemented.");
  }
  delete(id: number): boolean {
    throw new Error("Method not implemented.");
  }
  get(id: number): any[] {
    var list = [
      {
        title: "xxxx",
        desc: "xxxxxxxxxx",
      },
      {
        title: "xxxx",
        desc: "xxxxxxxxxx",
      },
    ];

    return list;
  }
}

```



- 定义数据模型

```typescript
// /model/user.ts
import { MsSqlDb } from "../modules/db";

//定义数据库的映射
class UserClass {
  username: string | undefined;
  password: string | undefined;
}

var UserModel = new MsSqlDb<UserClass>();
export { UserClass, UserModel };

```

- 使用

```typescript
// /index.ts
import {UserClass,UserModel} from './model/user';

//增加数据
var u=new UserClass();
u.username='张三';
u.password='12345655654757';
UserModel.add(u);
//获取user表数据
var res=UserModel.get(123);
console.log(res);

```



## 命名空间

- 在代码量较大的情况下，为了避免各种变量命名相冲突，可将相似功能的函数、类、接口等放置到命名空间内同 Java 的包、.Net的命名空间一样，TypeScrip 的命名空间可以将代码包裹起来，只对外暴露需要在外部访问的对象。命名空间内的对象通过 export 关键字对外暴露。

- 命名空间和模块的区别：
  - 命名空间：内部模块，主要用于组织代码，避免命名冲突。
  - 模块：ts 的外部模块的简称，侧重代码的复用，一个模块里可能会有多个命名空间。

### 内部使用

```typescript
namespace A {
  interface Animal {
    name: string;
    eat(): void;
  }
  export class Dog implements Animal {
    name: string;
    constructor(theName: string) {
      this.name = theName;
    }

    eat() {
      console.log(`${this.name} 在吃狗粮。`);
    }
  }

  export class Cat implements Animal {
    name: string;
    constructor(theName: string) {
      this.name = theName;
    }

    eat() {
      console.log(`${this.name} 吃猫粮。`);
    }
  }
}

namespace B {
  interface Animal {
    name: string;
    eat(): void;
  }
  export class Dog implements Animal {
    name: string;
    constructor(theName: string) {
      this.name = theName;
    }

    eat() {
      console.log(`${this.name} 在吃狗粮。`);
    }
  }

  export class Cat implements Animal {
    name: string;
    constructor(theName: string) {
      this.name = theName;
    }

    eat() {
      console.log(`${this.name} 在吃猫粮。`);
    }
  }
}
// 命名空间外使用，需要使用 命名空间.类名 使用
var c = new B.Cat("小花");

c.eat();

```

### 外部使用

```typescript
// /module/animal.ts
export namespace A {
  interface Animal {
    name: string;
    eat(): void;
  }
  export class Dog implements Animal {
    name: string;
    constructor(theName: string) {
      this.name = theName;
    }

    eat() {
      console.log(`${this.name} 在吃狗粮。`);
    }
  }

  export class Cat implements Animal {
    name: string;
    constructor(theName: string) {
      this.name = theName;
    }

    eat() {
      console.log(`${this.name} 吃猫粮。`);
    }
  }
}

export namespace B {
  interface Animal {
    name: string;
    eat(): void;
  }
  export class Dog implements Animal {
    name: string;
    constructor(theName: string) {
      this.name = theName;
    }

    eat() {
      console.log(`${this.name} 在吃狗粮。`);
    }
  }

  export class Cat implements Animal {
    name: string;
    constructor(theName: string) {
      this.name = theName;
    }

    eat() {
      console.log(`${this.name} 在吃猫粮。`);
    }
  }
}

```



```typescript
// /index.ts
import { A, B } from "./modules/animal";

var d = new A.Dog("小黑");
d.eat();

var dog = new B.Dog("小花");
dog.eat();
```





## 装饰器

- 装饰器是一种特殊类型的声明，它能够被附加到类声明，方法，属性或参数上，可以修改类的行为。
- 通俗的讲装饰器就是一个方法，可以注入到类、方法、属性参数上来扩展类、属性、方法、参数的功能。
- 常见的装饰器有：类装饰器、属性装饰器、方法装饰器、参数装饰器
- 装饰器的写法：普通装饰器（无法传参） 、装饰器工厂（可传参）
- 装饰器是过去几年中 js 最大的成就之一，已是 Es7 的标准特性之一



### 类装饰器

- 类装饰器在类声明之前被声明（紧靠着类声明）。类装饰器应用于类构造函数，可以用来监视，修改或替换类定义或者传入一个参数
- 普通装饰器（无法传参）

```typescript
function logClass(params: any) {
  console.log(params);
  // params 就是当前类
  params.prototype.apiUrl = "动态扩展的属性";
  params.prototype.run = function () {
    console.log("我是一个run方法");
  };
}

// 使用 @方法 表示添加一个类装饰器来拓展类
@logClass
class HttpClient {
  constructor() {}
  getData() {}
}
var http: any = new HttpClient();
console.log(http.apiUrl); // 返回：动态扩展的属性
http.run(); // 返回：我是一个run方法

```



- 装饰器工厂（可传参）

```typescript
function logClass(params: string) {
  return function (target: any) {
    // 类 当前类
    console.log(target);
    // params 传入的参数
    console.log(params);
    target.prototype.apiUrl = params;
  };
}

@logClass("hello")
class HttpClient {
  constructor() {}

  getData() {}
}

var http: any = new HttpClient();
console.log(http.apiUrl); // 返回：'hello'

```



- 可以用来重载构造函数
- 类装饰器表达式会在运行时当作函数被调用，类的构造函数作为其唯一的参数。
- 如果类装饰器返回一个值，它会使用提供的构造函数来替换类的声明。

```typescript
function logClass(target: any) {
  console.log(target);
  // 类似利用继承，重写类
  return class extends target {
    apiUrl: any = "我是修改后的数据";
    getData() {
      this.apiUrl = this.apiUrl + "----";
      console.log(this.apiUrl);
    }
  };
}

@logClass
class HttpClient {
  public apiUrl: string | undefined;
  constructor() {
    this.apiUrl = "我是构造函数里面的apiUrl";
  }
  getData() {
    console.log(this.apiUrl);
  }
}

var http = new HttpClient();
http.getData(); // 返回：'我是修改后的数据----'

```



### 属性装饰器

- 属性装饰器表达式会在运行时当作函数被调用，传入下列2个参数：

  1. 对于静态成员来说是类的构造函数，对于实例成员是类的原型对象。

  2. 成员的名字。

```typescript
//属性装饰器
function logProperty(params: any) {
  return function (target: any, attr: any) {
    console.log(target);
    console.log(attr);
    target[attr] = params;
  };
}

class HttpClient {
  @logProperty("http://itying.com")
  public url: any | undefined;
  constructor() {}
  getData() {
    console.log(this.url);
  }
}
var http = new HttpClient();
http.getData();
```



### 方法装饰器

- 它会被应用到方法的 属性描述符上，可以用来监视，修改或者替换方法定义。
- 方法装饰会在运行时传入下列3个参数：
  1. 对于静态成员来说是类的构造函数，对于实例成员是类的原型对象。
  2. 成员的名字。
  3. 成员的属性描述符。
- 可以用来拓展类的属性和方法

```typescript
//方法装饰器一

function get(params: any) {
  return function (target: any, methodName: any, desc: any) {
    console.log(target);
    console.log(methodName);
    console.log(desc);
    // 拓展类的属性
    target.apiUrl = "xxxx";
    // 拓展类的方法
    target.run = function () {
      console.log("run");
    };
  };
}

class HttpClient {
  public url: any | undefined;
  constructor() {}
  @get("http://www.itying,com")
  getData() {
    console.log(this.url);
  }
}

var http: any = new HttpClient();
console.log(http.apiUrl); // 返回：'xxxx'
http.run(); // 返回：'run'

```

- 覆盖原来的方法

```typescript
function get(params: any) {
  return function (target: any, methodName: any, desc: any) {
    console.log(target);
    console.log(methodName);
    // 这个打印的就是方法的内容
    console.log(desc.value);

    //修改装饰器的方法  把装饰器方法里面传入的所有参数改为string类型

    //1、保存当前的方法
    // 覆盖原来的方法
    desc.value = function (...args: any[]) {
      args = args.map((value) => {
        return String(value);
      });
    };
  };
}

class HttpClient {
  public url: any | undefined;
  constructor() {}
  @get("http://www.itying,com")
  getData(...args: any[]) {
    console.log(args);
    console.log("我是getData里面的方法");
  }
}

var http = new HttpClient();
http.getData(123, "xxx");

```

- 拓展原来的方法

```typescript
function get(params: any) {
  return function (target: any, methodName: any, desc: any) {
    console.log(target);
    console.log(methodName);
    // 这个打印的就是方法的内容
    console.log(desc.value);

    //修改装饰器的方法  把装饰器方法里面传入的所有参数改为string类型

    //1、保存当前的方法
	// 拓展方法，先执行装饰器中的内容
    var oMethod = desc.value;
    desc.value = function (...args: any[]) {
      args = args.map((value) => {
        return String(value);
      });
      oMethod.apply(this, args);
    };
  };
}

class HttpClient {
  public url: any | undefined;
  constructor() {}
  @get("http://www.itying,com")
  getData(...args: any[]) {
    console.log(args);
    console.log("我是getData里面的方法");
  }
}

var http = new HttpClient();
http.getData(123, "xxx");

```



### 方法参数装饰器

- 参数装饰器表达式会在运行时当作函数被调用，可以使用参数装饰器为类的原型增加一些元素数据 ，传入下列3个参数：
  1. 对于静态成员来说是类的构造函数，对于实例成员是类的原型对象。
  2. 方法的名字。
  3. 参数在函数参数列表中的索引。

- 用的比较少，功能可以被类装饰器替代

```typescript
function logParams(params: any) {
  return function (target: any, methodName: any, paramsIndex: any) {
    console.log(params);

    console.log(target);

    console.log(methodName);

    console.log(paramsIndex);

    target.apiUrl = params;
  };
}

class HttpClient {
  public url: any | undefined;
  constructor() {}
  getData(@logParams("xxxxx") uuid: any) {
    console.log(uuid);
  }
}

var http: any = new HttpClient();
http.getData(123456);
console.log(http.apiUrl);

```



### 执行顺序

- 装饰器执行顺序
  - 非类修饰器（按照代码书写顺序：从上到下，从左到右）> 类修饰器。
  - 属性和方法没有区别，看代码写的先后顺序，参数装饰器也是。而且同一个方法中的有多个参数使用，则从左往右，同一个参数上有多个也是从左往右









