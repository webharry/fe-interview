### ES6
#### ES6 - Class
对于面向对象编程而言，主要关注类的声明、属性、方法、静态方法、继承、多态、私有属性。ES6 之前类是通过构造函数来实现的,在 ES6 中把类的声明专业化了，通过 class 语法来代替 function 的方式:
```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  say() {
    const str = `Hello, my name is ${this.name}, ${this.age} years old!`;
    console.log(str);
  }
}

class Chinese extends Person {
  constructor(name, age) {
    super(name, age);
    this.country = 'Chinese';
  }

  say() {
    const str = `Hello, my name is ${this.name}, ${this.age} years old! I'm ${this.country} Person`;
    console.log(str);
  }
}

/* ES6 class */
const person = new Person('lusy', 25);
const chinesePerson = new Chinese('王', 35);

person.say();
chinesePerson.say();
```

这里有个注意点就是，如果是子类继承父类，那么子类的constructor 内部必须有 super()，否则会报错。

从上面代码可以看出：
- 类里面有一个 constructor() 方法，这就是构造方法。
- this 关键字指向实例对象。
- 给类增加自定义方法的时候，前面不需要加上 function 关键字，直接把函数定义放进去了就可以了。另外，方法与方法之间不需要逗号分隔，加了会报错。
- 类的所有方法（constructor() 和自定义方法）都定义在类的 prototype 属性上面，因此在类的实例上面调用方法，其实就是调用原型上的方法。

#### ES6 - 箭头函数
- 几种箭头函数写法：

如果只有一个参数，可以省略括号；如果大于一个参数或没有参数，一定要带括号。
```js
// 只有一个参数
let hello1 = name => {
  console.log('say hello', name)
}

// 没有参数
let hello2 = () => {
  console.log('say hello')
}

// 多个参数
let hello3 = (name, age) => {
  console.log('say hello', name, age)
}
```

- this 指向
箭头函数中 this 指向函数定义时所在的外层作用域的 this，即包裹箭头函数的函数。

如果包裹箭头函数的，依旧是个箭头函数，则继续往外层找，直到 window（浏览器环境下非严格模式）或 undefined（严格模式）。
```js
var scope = 'window'
var obj = {
  scope: 'obj',
  funcScope: function() {
    console.log('当前作用域：', this.scope)
  },
  arrayFuncScope: () => console.log('当前作用域：', this.scope)
}
var obj2 = {
  scope: 'obj2'
}
obj.funcScope()                 // obj
obj.arrayFuncScope()           // window
obj.funcScope.call(obj2)       // obj2 
obj.arrayFuncScope.call(obj2)  // window
```

注意点
- 箭头函数不可以当作构造函数
- 箭头函数不可以使用 arguments 对象
