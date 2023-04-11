### ES6
#### ES6 - Generator
ES6 的 Generator 也是一种异步编程解决方案,Generator 是一个迭代器生成函数，它被调用并不会立即执行，而是返回一个迭代器，然后可以进行异步调用，同时还可以挂起操作，非常的牛X但是使用起来也相对复杂。它有两个特性：
- `function` 关键字与函数名之间有一个星号`*`
- 函数体内部使用 `yield` 表达式，定义不同的内部状态。

```js
function* myGenerator() {
    yield 'a'
    yield 'b'
    return 'c'
  }
var me = myGenerator()
console.log(me) // 输出：myGenerator {<suspended>} ，是一个迭代器对象

//使用 next() 方法调用:
me.next() // {value: 'a', done: false}
me.next() // {value: 'b', done: false}
me.next() // {value: 'c', done: true}
me.next() // {value: undefined, done: true}
```

从代码中我们可以看出：
调用 Generator 函数它返回的是一个迭代器对象，然后通过调用此对象的方法`.next()`来一步一步执行函数内部的状态，每一个 `yield` 关键字对应着一个状态，而 `yield` 关键字则是表示在此处暂停执行的意思
（直到使用 next 调用），每个状态是一个对象有两个属性`{value: 此状态的值, done: 迭代器函数是否结束}`.

#### ES6 - Set
Set 对象是 ES6 为我们提供的一个新的数据结构，它是以键值对儿的形式存在，类似于 Map，但是区别在于 Set 对象具有自动去重的功能。
```js
var oo = new Set([1, 1, 2, 2, 3, 4]);
console.log(oo); // {1, 2, 3, 4}
oo.add(1);     // {1, 2, 3, 4}
oo.add(5);   // {1, 2, 3, 4, 5}
oo.keys(); // {1, 2, 3, 4, 5}
```

应用：一行代码实现数组去重
```js
var arr = [1, 3, 3, 4, 5];
function uniqueArr(arr) {
    return [...new Set(arr)];
    // return Array.from(new Set(arr));
}
```
从上面可以看出来如下几点：

1.Set 对象的构造函数可以接收一个数组，然后主动去重。

2.Set 对象返回的是一个对象，可以通过Array.from方法转换成数组。

#### ES6 - Symbol
Symbol 是用来创建唯一性变量的，使用 Symbol 可以为程序创建唯一性的 ID，在创建的时候可以为其新增参数描述该变量，即使参数相同两个 Symbol 也是不同的。
```js
var s1 = Symbol()
var s2 = Symbol('aa')
var s3 = Symbol('aa')

s1 === s2 // false
s2 === s3 // false
```
具体来说它的应用有如下几种：

- 用作对象的 key 值
- 用来定义系统常量
- 可以使用 Symbol 定义类的私有属性/方法

#### ES6 - 扩展运算符
ES6 扩展运算符可以将数组对象转化成逗号分隔的参数序列，这同样也是非常便捷的 API。
```js
var arr = [1, 2, 3];
// ES5
var arrCopy = JSON.parse(JSON.stringify(arr));
console.log(arrCopy2 !== arr); // true
// ES6
var arrCopy2 = [...arr];
console.log(arrCopy2 !== arr); // true
```
