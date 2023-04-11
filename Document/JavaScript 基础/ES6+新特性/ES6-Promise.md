### ES6
#### ES6 - Promise
##### Promise知识点复习

- Promise是一种实现异步代码的手段，存储着将来会发生的某种结果。Promise方法接收一个函数参数handler，new一个Promise实例会立即执行这个handler。其中函数handler接收两个方法参数，resolve和reject方法，分别代表执行成功和执行失败的回调函数。用法如下：
```js
const p = new Promise((resolve,reject) => {
    setTimeout(function(){
        resolve('成功')
    },200);
});
p.then(res => console.log(res)); // 成功
```

- Promise的then方法，返回一个新的promise实例，因此可以支持链式调用。用法如下：
```js
const p = new Promise((resolve,reject) => {
    setTimeout(function(){
        resolve('成功')
    },200);
});
p.then(res => {
    return res+1;
}).then(data => console.log(data)); // 成功1
```

- 如果then方法返回一个新的promise实例，then后的链式调用将等待这个新promise执行完毕后，以这个新promise的返回结果作为参数传入下一个then方法的回调函数中。比如：
```js
const p = new Promise((resolve,reject) => {
    setTimeout(function(){
        resolve('成功')
    },200);
});
p.then(res => {
    return new Promise((resolve,reject)=>{
        resolve(123);
    });
}).then(data => console.log(data)); // 123
```

例子中p的第一个then方法返回一个新的promise实例，新promise实例执行完毕将123传入下一个then方法的回调函数中，打印出123。

以上是Promise的基本功能，我们手写实现一个Promise，方便理解Promise原理。

##### 手写Promise
1、通过类实现 promise：（推荐！）
```js
const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';
class myPromise{
    constructor(handle) {
        this.resolveCallCack = []; // 存储成功时的回调函数
        this.rejectCallCack = []; // 存储失败时的回调函数
        this.value = undefined;
        this.err = undefined;
        this.status = PENDING; // promise的状态

        let resolve = (data) => {
            if(this.status !== PENDING) return;
            this.status = FULFILLED;
            this.value = data;
            this.resolveCallCack.forEach(fn => {
                fn(this.value);
            });
        }

        let reject = (err) => {
            if(this.status !== PENDING) return;
            this.status = REJECTED;
            this.err = err;
            this.rejectCallCack.forEach(fn => {
                fn(tthis.err);
            })
        }

        if(handle instanceof Function){
            handle(resolve,reject);
        }
    }

    then(resolveNext,rejectNext) {
        let that = this;
        return new Promise((resolve,reject) =>{
            switch(this.status){
                case PENDING:
                    this.resolveCallCack.push(resolveNext);
                    this.rejectCallCack.push(resolveNext);
                    break;
                case FULFILLED:
                    resolveNext(this.value);
                    break;
                case REJECTED:
                    rejectNext(this.err);
                    break;
            }
        })
    }
}

var a = new myPromise(function(resolve,rejected) {
    setTimeout(function(){
        resolve("成功");
    },2000);
}).then(data => {
    console.log(data);
})const PENDING = 'pending';
```
总结：

缺陷：手写的myPromise的then方法中返回一个新promise实例时，执行结果和ES6的Promise存在差异，待完善。

2、通过定义myPromise函数实现promise功能：
```js
const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';
function myPromise(handle){
    var self = this; // 先保存一份this,防止后面方法this错乱！！！
    self.status = PENDING;
    self.value = '';
    self.reson = '';
    self.resolvedCallback = [];
    self.rejectedCallback = [];

    function resolve(data){
        if(self.status !== PENDING) return;
        self.status = FULFILLED;
        self.value = data;
        self.resolvedCallback.forEach(fn => {
            fn(self.value);
        });
    }
    function reject(data){
        if(self.status !== PENDING) return;
        self.status = REJECTED;
        self.reson = data;
        self.rejectedCallback.forEach(fn => {
            fn(self.reson);
        });
    }

    try{
        handle(resolve,reject);
    }catch(e){
        reject(e)
    }
}

myPromise.prototype.then = function(resolveNext,rejectNext){
    var that = this;
    return new myPromise((resolve,reject) => {
        switch(that.status){
            case PENDING:
                that.resolvedCallback.push(resolveNext);
                that.rejectedCallback.push(rejectNext);
                break;
            case FULFILLED:
                resolveNext(that.value);
                break;
            case REJECTED:
                rejectNext(that.reson);
                break;
        }
    });
}

myPromise.all = function(arr){
    return new myPromise((resolve,reject)=>{
        var res = [];
        arr.forEach(item => {
            item.then(data => {
                res.push(data);
                if(res.length === arr.length){
                    resolve(res);
                }
            },err=> {
                reject(err);
            })
        });
    });
}

//// 测试myPromise方法
var obj = new myPromise(function(resolve,reject){
     setTimeout(function(){
         resolve(2);
     },0);
}).then((data)=>{
     console.log(data);
})

var obj2 = new myPromise(function(resolve,reject){
     setTimeout(function(){
         resolve(3);
     },0);
}).then((data)=>{
     console.log(data);
})

// 测试myPromise.all方法
var obj = new myPromise(function(resolve,reject){
    setTimeout(function(){
        resolve(2);
    },0);
})

var obj2 = new myPromise(function(resolve,reject){
    setTimeout(function(){
        resolve(3);
    },0);
})
var myall = myPromise.all([obj,obj2]).then(data => {
    console.log("resolve", data);
},err => {
    console.log(err);
});
console.log(myall);
```
总结：推荐通过类实现promise，如果使用函数实现promise，记得保存一份this防止后边方法访问this错乱。
