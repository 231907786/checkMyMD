# ES6规范

## 术语说明

- `Array.prototype.slice` 简写为 Array#slice,其他同理

## 引用

- 对所有的不可变引用使用`const`,可变引用或不能申明时赋值的使用`let`,尽量不使用`var`

```javascript
  // 大多数情况的用法
  const obj = {}
  const num = 1

  // 比如计数器
  let mutableNum = 0

  // 不能在声明时赋值的
  let toBeDefined
```

## 对象

- 对象的属性方法使用简写,但不推荐使用箭头函数

```javascript
  // 建议使用
  const obj = {
    fn() {

    }
  }

  // 不推荐
  const obj = {
    fn: () => {

    }
  }
```

- 对象属性值使用简写

```javascript
  const str = 'Hello World'
  const obj = {
    str
  }

  // 等价于之前的语法
  const obj = {
    str: str
  }
```

- 接上条,对象有多个属性值时,简写属性值写在前,方便阅读

```javascript
  const obj = {
    a,
    b,
    c,
    d: 1,
    e: 2,
  }
```

## 数组

- 使用拓展运算符`...`复制数组

```javascript
  const arr = [1, 2, 3]
  const arrCopy = [...arr]

  arr.join('') === arrCopy.join('')
  arr !== arrCopy
```

- 使用 Array#from 把类数组对象转换成数组

```javascript
  const divs = document.getElementsByTagName('div')
  const nodes = Array.from(divs)

  // 之前的做法是使用slice,ES6简化了语法
  const nodes = Array.prototype.slice.call(divs, 0)
```

## 解构

- 使用对象解构

```javascript
  const user = {
    firstName: 'ye',
    lastName: 'shanqi',
  }

  // 如果函数参数是对象,可以直接使用对象解构得到变量
  function getFullName({firstName, lastName}){
    return firstName + lastName
  }

  // 一般情况
  const {firstName, lastName} = user

  // 函数返回多变量时用对象,方便使用对象解构取值
  function getObj(input) {
    // ...
    return {left, right, top, bottom}
  }

  const {left, right} = getObj(input)
```

## 字符串

- 字符串使用单引号

```javascript
  const name = 'yeshanqi'
```

- 拼接字符串使用ES6模板字符串

```javascript
  const name = 'yeshanqi'
  function hello(name) {
    return `my name is ${name}, how r u ?`
  }
```

## 函数

- 不要使用函数的隐藏变量arguments,改用ES6 rest 语法`...`

```javascript
  function concatAll(...args) {
    return args.join('')
  }
```

- 使用ES6语法给函数的参数指定默认值

```javascript
  function fn(arg1 = 5) {
    typeof arg1 === 'number'
  }
```

## 箭头函数

- 匿名函数尽量使用箭头函数,因为它会自动绑定外层的this,这在setTimeout中有明显作用

```javascript
  [1,2,3].map(x => x * x)
```

## 模块

- 在babel编译器环境内总是使用import/export模块语法

- 不要使用import通配符语法,因为对象解构可读性更高

```javascript
  // bad
  import * as obj from './obj'
  const {a, b, c} = obj

  // good
  import {a, b, c} from './obj'
```

## if/else的花括号问题

- 如果代码换行,就用花括号包裹

```javascript
  // 以下2种写法都可以
  if(true) return true

  if(true) {
    return true
  }
```

## 注释

- 方法注释规范

```javascript
  /**
  * 开头写方法的用途,代码的思路等等
  *
  * @param {String} tag
  * @return {Element} element
  */
  function make(tag) {

  // ...stuff...

  return element;
  }
```

- 单行注释写在代码上方,并与上一行代码之间用空格隔开.

```javascript
  function fn() {
    const a = 1

    // 这是下一行代码的注释
    const b = 2
  }
```

## 缩进

- tab = 2个空格

- 参数列表、 对象属性、 数组成员 写在同一行时，在分隔符后空一格

```javascript
  function fn(a, b, c){

  }
```

- 长链式调用时,每次方法调用都换行,便于阅读

```javascript
  $('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount()
```

## 逗号

- 对象、数组、参数列表，如果换行排列,则结尾都加逗号

> 虽然语法上来说数组和参数列表结尾不能加逗号,但预编译器会自动忽略.而好处是vcs合并代码时减少错误和冲突
```javascript
  const obj = {
    a: 1,
    b: 2,
    c: 3,
+   d: 4
  }

  const arr = [
    1,
    2,
    3,
+   4,
  ]

  function fn(
    arg1,
    arg2,
    arg3,
  ) {

  }
```

## 命名

- 驼峰命名对象、函数和实例

- 帕斯卡式（首字母大写的驼峰）命名构造函数或类

- 如果你的文件只输出一个类，那你的文件名必须和类名完全保持一致

- 当你导出默认的函数时使用驼峰式命名。你的文件名必须和函数名完全保持一致

- 当你导出单例、函数库、空对象时使用帕斯卡式命名
