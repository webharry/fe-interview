### ES7
#### ES7 - Array.prototype.includes
Array.prototype.includes() 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回 false。

```js
const arr = ['es6', 'es7', 'es8']
console.log(arr.includes('es6')) // true
console.log(arr.includes('es9')) // false
console.log(arr.indexOf('es6') > -1) // true

'aaabbbccc'.includes('bbb'); // true

[1, 2, NaN].indexOf(NaN); // -1
[1, 2, NaN].incldes(NaN); // true

const arr = [1, [2, 3], 4]
console.log(arr.includes([2, 3])) // false
console.log(arr.indexOf([2, 3]))  // -1
```

可以看到，与 indexOf 的优缺点比较：
两者都是采用 === 的操作符来作比较的，不同之处在于：对于 NaN 的处理结果不同。在 js 中 NaN === NaN 的结果是 false，indexOf() 就是这样处理的，但是 includes() 不是这样的。

如果只想知道某个值是否在数组中存在，而并不关心它的索引位置，建议使用 includes()。如果想获取一个值在数组中的位置，那么只能使用 indexOf() 方法。

#### ES7 - 幂指运算
```js
// ES5
console.log(Math.pow(2, 10)) // 1024

// ES7
console.log(2 ** 10) // 1024
```

Math.pow() 函数返回基数（base）的指数（exponent）次幂。

求幂运算符（**）返回将第一个操作数加到第二个操作数的幂的结果。它等效于 Math.pow()，不同之处在于它也接受 BigInt 作为操作数。

### ES8
#### ES8 - Async/Await
async 和 await 是一种更加优雅的异步编程解决方案，是 Promise 的拓展。

前面添加了 async 的函数在执行后都会自动返回一个 Promise 对象：
```js
async function foo() {
  return 'hello'
}
console.log(foo()) // Promise
foo()

// 等价与
function foo() {
  return Promise.resolve('hello')
}
console.log(foo()) // Promise
foo()
```

await 后面需要跟异步操作，不然就没有意义，而且 await 后面的 Promise 对象不必写 then，因为 await 的作用之一就是获取后面 Promise 对象成功状态传递出来的参数。
```js
function timeout() {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log(1)
      resolve('success')
    }, 1000)
  })
}

// 不加 async 和 await 是 2、1, 加了是 1、2
async function foo() {
  let res = await timeout()
  console.log(2)
  console.log(res)
}
foo()
```

注意：await 只能在 async 标记的函数内部使用，单独使用会触发 Syntax error。

#### ES8 - 其他 API
- Object.values/Object.entries/Object.getOwnPropertyDescriptors
```js
// Object.values() 返回一个数组，其元素是在对象上找到的可枚举属性值。
const obj = {
  name: 'zhangsan',
  age: 13,
  gender: 'male'
}

console.log(Object.values(obj)) // ['zhangsan', 13, 'male']

// Object.entries() 方法返回一个给定对象自身可枚举属性的键值对数组。
for (let [k, v] of Object.entries(obj)) {
  console.log(k, v)
  // name zhangsan
  // age 13
  // gender male
}

// Object.getOwnPropertyDescriptors() 用来返回一个对象的所有自身属性/方法的描述符,如果没有任何自身属性，则返回空对象。

console.log(Object.getOwnPropertyDescriptors(obj)) // {name: {…}, age: {…}, gender: {…}}
```

- String.prototype.padStart()/String.prototype.padEnd(), 允许将空字符串或其他字符串添加到原始字符串的开头或结尾。
```js
const str = 'hello'
console.log(str.padStart(8, '.'))     // ...hello
console.log(str.padStart(8))          //    hello
console.log(str.padStart(8, 'world')) // worhello

console.log(str.padEnd(8, '.'))       // hello...
console.log(str.padEnd(8))            // hello   (前面有三个空格)
console.log(str.padEnd(8, 'world'))   // hellowor
```

### ES9
#### ES9 - for-await-of
- 异步迭代器（for-await-of）：循环等待每个 Promise 对象变为 resolved 状态才进入下一步。
```js
function Gen(time) {
  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      resolve(time)
    }, time)
  })
}

async function test() {
  let arr = [Gen(2000), Gen(100), Gen(3000)]
  for await (let item of arr) {
    console.log(Date.now(), item)
  }
}

test()
// 1643788502772 2000
// 1643788502772 100
// 1643788503775 3000
```

#### ES9 - Promise.prototype.finally()
Promise.prototype.finally() 方法返回一个 Promise，在 promise 执行结束时，无论结果是 fulfilled 或者是 rejected，在执行 then() 和 catch() 后，都会执行 finally() 指定的回调函数。

这为指定执行完 promise 后，无论结果是 fulfilled 还是 rejected 都需要执行的代码提供了一种方式，避免同样的语句需要在 then() 和 catch () 中各写一次的情况。

```js
new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('success')
    // reject('fail')
  }, 1000)
}).then(res => {
  console.log(res)
}).catch(err => {
  console.log(err)
}).finally(() => {
  console.log('finally')
})
```

#### ES9 - Rest/Spread 对象扩展运算
ES6 出现了扩展运算符，但是只是给数组准备的，而扩展运算符非常好用，ES9 因此就扩展到了对象，现在对象也可以使用扩展运算来进行便捷操作。
```js
let obj = {
    name: 'aaa',
    email: 'luffyzh@163.com'
}

let obj2 = {...obj}
console.log(obj2) // {name: 'aaa', email: 'luffyzh@163.com'}
console.log(obj2 !== obj) // true

let obj3 = { age: 20, ...obj2 }
console.log(obj3) // {age: 20, name: 'aaa', email: 'luffyzh@163.com'}
```

### ES10
#### ES10 - Object.fromEntries()
方法 Object.fromEntries() 把键值对列表转换为一个对象，这个方法是和 Object.entries() 相对的。

```js
Object.fromEntries([
  ['foo', 1],
  ['bar', 2]
])
// {foo: 1, bar: 2}
```

#### ES10 - String.prototype.trimStart()/String.prototype.trimEnd()
trimStart() 方法从字符串的开头删除空格，trimLeft() 是此方法的别名。
trimEnd() 方法从一个字符串的右端移除空白字符，trimRight 是 trimEnd 的别名。

```js
let str = '   foo  '
console.log(str.length) // 8
str = str.trimStart()
console.log(str.length) // 5

let str2 = '   foo  '
console.log(str2.length) // 8
str = str.trimEnd()
console.log(str2.length) // 6
```

#### ES10 - Array.prototype.flat()/Array.prototype.flatMap()
flat() 方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。
const newArray = arr.flat(depth) // depth 指定要提取嵌套数组的结构深度，默认值为 1.
```js
const numbers = [1, 2, [3, 4, [5, 6]]]
console.log(numbers.flat())
// [1, 2, 3, 4, [5, 6]]

console.log(numbers.flat(2))
// [1, 2, 3, 4, 5, 6]
```

flatMap() 方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。从方法的名字上也可以看出来它包含两部分功能一个是 map，一个是 flat（深度为 1）。
```js
const numbers = [1, 2, 3]
numbers.map(x => [x * 2])     // [[2], [4], [6]]
numbers.flatMap(x => [x * 2]) // [2, 4, 6]
```
