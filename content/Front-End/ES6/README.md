# 目录

* [class](#class)
* [箭头函数](#箭头函数)
* [Promise](#Promise)
* [模块化](#模块化)
* [Object.assign(target, ...sources)](#objectassigntarget-sources)
* [Symbol](#symbol)

## [阮一峰：ECMAScript 6入门](http://es6.ruanyifeng.com/)
## [学习ES2015](https://babel.docschina.org/docs/en/learn)


# <p align="center">class</p>
###### [<p align="right">back to top ▲</p>](#目录)





# <p align="center">箭头函数</p>
###### [<p align="right">back to top ▲</p>](#目录)

**ES6允许使用“箭头”（=>）定义函数。**

* 如果箭头函数不需要参数或需要多个参数，就使用一个圆括号代表参数部分；

    ```javascript
    var f = () => 5;
    // 等同于
    var f = function () { return 5 };

    var sum = (num1, num2) => num1 + num2;
    // 等同于
    var sum = function(num1, num2) {
        return num1 + num2;
    };
    ```

* 如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回；

    ```javascript
    var sum = (num1, num2) => { return num1 + num2; };
    ```

* 大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号，否则会报错；

    ```javascript
    // 报错
    let getTempItem = id => { id: id, name: "Temp" };

    // 不报错
    let getTempItem = id => ({ id: id, name: "Temp" });
    ```

* 如果箭头函数只有一行语句，且不需要返回值，可以采用下面的写法，就不用写大括号了；

    ```javascript
    let fn = () => void doesNotReturn();
    ```

* 箭头函数可以与变量解构结合使用；

    ```javascript
    const full = ({ first, last }) => first + ' ' + last;
    // 等同于
    function full(person) {
        return person.first + ' ' + person.last;
    }
    ```

* 箭头函数表达更加简洁，可以简化回调函数。

    ```javascript
    // 正常函数写法
    [1,2,3].map(function (x) {
        return x * x;
    });
    // 箭头函数写法
    [1,2,3].map(x => x * x);

    // 正常函数写法
    var result = values.sort(function (a, b) {
        return a - b;
    });
    // 箭头函数写法
    var result = values.sort((a, b) => a - b);
    ```

#### 注意

1. 函数体内的this对象，是定义时所在的对象，而不是使用时所在的对象；
    * this对象的指向是可变的，但是在箭头函数中，它是固定的：

    ```javascript
    function foo() {
        setTimeout(() => {
            console.log('id:', this.id);
        }, 100);
    }

    var id = 21;

    foo.call({ id: 42 });
    // id: 42
    ```
    
2. 不可以当作构造函数，即不可以使用new命令，否则会抛出一个错误；
3. 不可以使用arguments对象，该对象在函数体内不存在，如果要用，可以用rest参数代替；
    ```javascript
    const numbers = (...nums) => nums;
    numbers(1, 2, 3, 4, 5)
    // [1,2,3,4,5]

    const headAndTail = (head, ...tail) => [head, tail];
    headAndTail(1, 2, 3, 4, 5)
    // [1,[2,3,4,5]]
    ```
4. 不可以使用yield命令，因此箭头函数不能用作Generator函数。



# <p align="center">Promise</p>
###### [<p align="right">back to top ▲</p>](#目录)

* Promise例子：

    ```javascript
    // 执行代码
    function test(resolve, reject){
        var timeOut = Math.random() * 2;
        console.log('set timeout to:', timeOut, 'seconds.');
        setTimeout(function(){
            if(timeOut < 1){
                console.log('call resolve()...');
                resolve('200 OK');
            }else{
                console.log('call reject()...');
                reject('timeout in' + timeOut + 'seconds.');
            }
        }, timeOut * 1000);
    }

    var p1 = new Promise(test);
    // 处理结果的代码
    var p2 = p1.then(function(result){
        console.log('成功：', result);
    });
    var p3 = p2.catch(function(reason){
        console.log('失败：', reason);
    });

    // ↓↓↓ 可简化为 ↓↓↓
    new Promese(test).then(function(result){
        console.log('成功：', result);
    }).catch(function(reason){
        console.log('失败：', reason);
    });

    // Promise最大的好处可以把“执行代码”和“处理结果的代码”清晰的分离开来。
    ```

* 有若干个异步任务，需要先做任务1，1成功后再做任务2，2成功后再做任务3，任何任务失败则不再继续并执行错误处理函数：

    ```javascript
    // job1、job2、job3都是Promise对象
    job1.then(job2).then(job3).catch(handleError);
    ```

* Promise还可以并行执行异步任务：

    ```javascript
    var p1 = new Promise(function(resolve, reject){
        setTimeout(resolve, 800, 'P1');
    })
    var p2 = new Promise(function(resolve, reject){
        setTimeout(resolve, 600, 'P2');
    })
    // 同时执行p1和p2，当它们都完成后执行then:
    Promise.all([p1, p2]).then(function(results){
        console.log(results);   // 获得一个数组['P1', 'P2']
    })
    ```

    ```javascript
    var p1 = new Promise(function(resolve, reject){
        setTimeout(resolve, 800, 'P1');
    })
    var p2 = new Promise(function(resolve, reject){
        setTimeout(resolve, 600, 'P2');
    })
    // 同时执行p1和p2，
    // p2执行较快，Promise的then()将获得结果'P2'，
    // p1仍在继续执行，但执行结果将被丢弃:
    Promise.race([p1, p2]).then(function(result){
        console.log(result);    // 'P2'
    })
    ```




# <p align="center">模块化</p>
###### [<p align="right">back to top ▲</p>](#目录)





# <p align="center">Object.assign(target, ...sources)</p>
###### [<p align="right">back to top ▲</p>](#目录)


* 用于将所有***可枚举属性***的值从一个或多个源对象sources复制到目标对象target
* 它将返回目标对象target

```js
const object1 = {
    a: 1,
    b: 2,
    c: 3
};

const object2 = Object.assign({c: 4, d: 5}, object1);

console.log(object2.c, object2.d);
// expected output: 3 5

// 合并对象
var o1 = { a: 1 };
var o2 = { b: 2 };
var o3 = { c: 3 };
var obj = Object.assign(o1, o2, o3);
console.log(obj);
// { a: 1, b: 2, c: 3 }
console.log(o1);  
// { a: 1, b: 2, c: 3 }, 注意目标对象自身也会改变。
```

---

> 如果目标对象中的属性具有相同的键，则属性将被源中的属性覆盖。后来的源的属性将类似地覆盖早先的属性。

```js
var o1 = { a: 1, b: 1, c: 1 };
var o2 = { b: 2, c: 2 };
var o3 = { c: 3 };

var obj = Object.assign({}, o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 }
```

---

> Object.assign()拷贝的是属性值。假如源对象的属性值是一个指向对象的引用，它也只拷贝那个引用值。

```js
function test() {
    'use strict';

    let obj1 = { a: 0 , b: { c: 0}};
    let obj2 = Object.assign({}, obj1);
    console.log(JSON.stringify(obj2)); // { a: 0, b: { c: 0}}
    
    obj1.a = 1;
    console.log(JSON.stringify(obj1)); // { a: 1, b: { c: 0}}
    console.log(JSON.stringify(obj2)); // { a: 0, b: { c: 0}}
    
    obj2.a = 2;
    console.log(JSON.stringify(obj1)); // { a: 1, b: { c: 0}}
    console.log(JSON.stringify(obj2)); // { a: 2, b: { c: 0}}
    
    obj2.b.c = 3;
    console.log(JSON.stringify(obj1)); // { a: 1, b: { c: 3}}
    console.log(JSON.stringify(obj2)); // { a: 2, b: { c: 3}}
    
    // Deep Clone
    obj1 = { a: 0 , b: { c: 0}};
    let obj3 = JSON.parse(JSON.stringify(obj1));
    obj1.a = 4;
    obj1.b.c = 4;
    console.log(JSON.stringify(obj3)); // { a: 0, b: { c: 0}}
}

test();
```

---

* 拷贝symbol类型的属性

```js
var o1 = { a: 1 };
var o2 = { [Symbol('foo')]: 2 };

var obj = Object.assign({}, o1, o2);
console.log(obj);
// { a : 1, [Symbol("foo")]: 2 } (cf. bug 1207182 on Firefox)
Object.getOwnPropertySymbols(obj);
// [Symbol(foo)]
```

---

* 继承属性和不可枚举属性是不能拷贝的

```js
var obj = Object.create({foo: 1}, { // foo 是个继承属性。
    bar: {
        value: 2  // bar 是个不可枚举属性。
    },
    baz: {
        value: 3,
        enumerable: true  // baz 是个自身可枚举属性。
    }
});

var copy = Object.assign({}, obj);
console.log(copy); // { baz: 3 }
```

---

* 异常会打断后续拷贝任务

```js
var target = Object.defineProperty({}, "foo", {
    value: 1,
    writable: false
}); // target 的 foo 属性是个只读属性。

Object.assign(target, {bar: 2}, {foo2: 3, foo: 3, foo3: 3}, {baz: 4});
// TypeError: "foo" is read-only
// 注意这个异常是在拷贝第二个源对象的第二个属性时发生的。

console.log(target.bar);
// 2，说明第一个源对象拷贝成功了。
console.log(target.foo2);
// 3，说明第二个源对象的第一个属性也拷贝成功了。
console.log(target.foo);
// 1，只读属性不能被覆盖，所以第二个源对象的第二个属性拷贝失败了。
console.log(target.foo3);
// undefined，异常之后 assign 方法就退出了，第三个属性是不会被拷贝到的。
console.log(target.baz);
// undefined，第三个源对象更是不会被拷贝到的。
```

---

* 原始类型会被包装为对象

```js
var v1 = "abc";
var v2 = true;
var v3 = 10;
var v4 = Symbol("foo");

var obj = Object.assign({}, v1, null, v2, undefined, v3, v4); 
// 原始类型会被包装，null 和 undefined 会被忽略。
// 注意，只有字符串的包装对象才可能有自身可枚举属性。
console.log(obj);
// { "0": "a", "1": "b", "2": "c" }
```

---

* 拷贝访问器

```js
var obj = {
    foo: 1,
    get bar() {
        return 2;
    }
};

var copy = Object.assign({}, obj); 
// { foo: 1, bar: 2 }
// copy.bar的值来自obj.bar的getter函数的返回值 
console.log(copy); 

// 下面这个函数会拷贝所有自有属性的属性描述符
function completeAssign(target, ...sources) {
    sources.forEach(source => {
        let descriptors = Object.keys(source).reduce((descriptors, key) => {
            descriptors[key] = Object.getOwnPropertyDescriptor(source, key);
            return descriptors;
        }, {});

        // Object.assign 默认也会拷贝可枚举的Symbols
        Object.getOwnPropertySymbols(source).forEach(sym => {
            let descriptor = Object.getOwnPropertyDescriptor(source, sym);
            if (descriptor.enumerable) {
                descriptors[sym] = descriptor;
            }
        });
        Object.defineProperties(target, descriptors);
    });
    return target;
}

var copy = completeAssign({}, obj);
console.log(copy);
// { foo: 1, get bar() { return 2 } }
```

# <p align="center">Symbol</p>
###### [<p align="right">back to top ▲</p>](#目录)

最初JS定义了6种基本类型：

* null
* undefined
* boolean
* number
* string
* object（array和function都是属于object的子类）

### ***前五个都是有限集，Object是一个无限集，每一个Object都是独一无二的。***

ES6中，新增了一种数据类型symbol：

```js
// 判断
typeof Symbol() === 'symbol' //true

// 特点
Symbol('key') !== Symbol('key') //true
```

### ***symbol类型的对象永远不相等，即便创建它们的时候传入了相同的值。***

因此，可借助此特性解决属性名的冲突问题（比如适用于多人编码的时候），这也是该数据类型存在的主要用途，意为标记。

```js
var sym = Symbol('foo');
var obj = {[sym] : 1};
obj[sym] === 1 //true
```