## ES6+ 新特性

我们把 ES6(也叫 ES2015) 以后更新的所有 JavaScript 标准规范新增的 API 叫做 ES6+ 新特性。

最新的 ES6 到 ES12 语法引入的很多新特性，能让很多依赖第三方库才能做到的事用原生 JS 寥寥几行代码就可迎刃而解。

本文只列举常用的特性和最基础的使用场景，详细介绍的话内容量将十分巨大，不妨通过 Google 搜索国外开发者的文档以及参阅 [ECMA 官方发布的标准](https://github.com/tc39/ecma262)。

### ES6
#### ES61 - let/const
这两个关键字是 ES6 新增的声明变量方式，与 var 的区别：

- var 有变量提升，值可变。允许重复声明。
- let 不存在变量提升，值可变。不允许重复声明。
- const 不存在变量提升，值不可变，但如果是定义对象，则属性可变。不允许重复声明。

`let`

let 声明的全局变量不是全局对象 window 的属性，不可以通过 window.变量名 的方式访问这些变量。

let 声明的变量拥有`块级作用域`。

> 函数作用域含义：属于这个函数的全部变量都可以在整个函数的范围内使用及复用（在嵌套的作用域中也可以使用）。

> 块级作用域就是使用一对大括号包裹的一段代码，比如函数、判断语句、循环语句，甚至单独的一个{}都可以被看作是一个块级作用域。

暂时性死区:对于 let，不存在变量提升，所以变量的调用不能先于声明。
> ES6 明确规定，如果区块中存在 let 和 const 命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错（该区域不受外部影响，哪怕外部声明过同名变量）。

```js
var a = 5
console.log(window.a) // 5

let b = 5
console.log(window.b) // undefined

for(var i = 0; i < 5; i++) {
  setTimeout(() => {
    console.log(i);
  })
}
// 5 5 5 5 5


for(let i = 0; i < 5; i++) {
  setTimeout(() => {
    console.log(i);
  })
}
// 0 1 2 3 4

var a = 5;
if (true) {
  a = 6;
  let a;
}
// ReferenceError: Cannot access 'a' before initialization
```

`const`

和 let 一样，具有`块级作用域`，`不会变量提升`，有`暂时性死区`。

const 定义的是常量，值不能被改变：
- const 声明的变量必须进行初始化。
- const 实际上保证的并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。因此它定义的对象的属性可变。
- 让对象或者数组这种引用数据类型也不被改变，需要使用 Object.freeze(obj)（浅层冻结，将最近一层的对象进行冻结）。

#### ES6 - 解构赋值

解构赋值也是 ES6 新特性中被使用非常频繁的一个，并且在实际开发过程中用处很大。

```js
// 数组的解构赋值
let [a, b, c] = [1, 2, 3]; // 1, 2, 3

let [aa, bb, cc] = [1, [2 , 3], [4, 5, 6]]; // 1 [2, 3] [4, 5, 6]
let [a, b, c] = "abc"                       // ["a", "b", "c"]

// 对象的解构赋值
let options = {
  title: '标题',
  width: 100,
  height: 200
}

let {title, width, height} = options

console.log(title)  // 标题
console.log(width)  // 100
console.log(height) // 200

// 字符串解构赋值
let str = 'hello'

let [a, b, c, d, e] = str

console.log(a, b, c, d, e) // h e l l o
```
