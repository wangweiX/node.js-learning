Javascript 是一种函数式编程语言，函数是完全类型化的对象，可以作为数据进行操作、扩展和传递。

## 概述

### 函数声明

#### funcation命令

`function`命令声明的代码区块，就是一个函数。`function`命令后面是函数名，函数名后面是一对圆括号，里面是传入函数的参数。函数体放在大括号里面。

```javascript
function showMessage() {
  console.log( 'Hello everyone!' );
}
```

#### 函数表达式

将一个匿名函数赋值给变量。这时，这个匿名函数又称函数表达式（Function Expression），因为赋值语句的等号右侧只能放表达式。

```javascript
let sayHi = function() {
    console.log( "Hello" );
};
console.log(sayHi); // [Function: sayHi]
```

### 重复声明

如果同一个函数被多次声明，后面的声明就会覆盖前面的声明。

```javascript
function showMessage() {
    console.log( 'Hello everyone!' );
}

showMessage();

function showMessage() {
    console.log( 'Hello wangwei!' );
}

showMessage();
```



### return 语句和递归

函数体内部的`return`语句，表示返回。JavaScript 引擎遇到`return`语句，就直接返回`return`后面的那个表达式的值，后面即使还有语句，也不会得到执行。也就是说，`return`语句所带的那个表达式，就是函数的返回值。`return`语句不是必需的，如果没有的话，该函数就不返回任何值，或者说返回`undefined`。

```javascript
function fib(num) {
    if (num === 0) return 0;
    if (num === 1) return 1;
    return fib(num - 2) + fib(num - 1);
}

console.log(fib(6)); // 8
```



### 第一等公民

JavaScript 语言将函数看作一种值，与其它值（数值、字符串、布尔值等等）地位相同。凡是可以使用值的地方，就能使用函数。比如，可以把函数赋值给变量和对象的属性，也可以当作参数传入其他函数，或者作为函数的结果返回。函数只是一个可以执行的值，此外并无特殊之处。

由于函数与其他数据类型地位平等，所以在 JavaScript 语言中又称函数为第一等公民。

```javascript
function add(x, y) {
    return x + y;
}

// 将函数赋值给一个变量
let operator = add;

// 将函数作为参数和返回值
function a(op) {
    return op;
}

console.log(a(add)(1, 1));// 2
```



### 函数名提升

JavaScript 引擎将函数名视同变量名，所以采用`function`命令声明函数时，整个函数会像变量声明一样，被提升到代码头部。所以，下面的代码不会报错。

```javascript
showMessage(); // Hello, I'm JavaScript!

function showMessage() {
    let message = "Hello, I'm JavaScript!"; // local variable
    console.log(message);
}
```



### 不能在条件语句中声明函数

根据 ES5 的规范，不得在非函数的代码块中声明函数，最常见的情况就是`if`和`try`语句。 下面代码在`if`代码块中声明了两个函数 `welcome` ，按照语言规范，这是不合法的。但是，实际情况是各家浏览器往往并不报错，能够运行。

但是由于存在函数名的提升，所以在条件语句中声明函数，可能是无效的，这是非常容易出错的地方。

```javascript
let age = 19;

// conditionally declare a function
if (age < 18) {
    function welcome() {
        console.log("Hello!");
    }
} else {
    function welcome() {
        console.log("Greetings!");
    }
}

// ...use it later
welcome(); // Greetings
```



## 函数的属性和方法

### name属性

```javascript
// 函数
function f1() {
}
console.log(f1.name);// "f1"

// 函数表达式
let f2 = function () {
};
console.log(f2.name);// "f2"
```



### length 属性

函数的`length`属性返回函数预期传入的参数个数，即函数定义之中的参数个数。 

```javascript
function f(a, b) {
    
}
console.log(f.length);// 2
```



### toString() 

函数的`toString`方法返回一个字符串，内容是函数的源码。 

```javascript
function f() {
    a();
    b();
    c();
}
console.log(f.toString());
// function f() {
//     a();
//     b();
//     c();
// }
```



## 函数作用域

### 定义

作用域（scope）指的是变量存在的范围。

在 ES5 的规范中，Javascript 只有两种作用域：一种是全局作用域，变量在整个程序中一直存在，所有地方都可以读取；另一种是函数作用域，变量只在函数内部存在。

在ES6 规范中，新增了块级作用域。详见 [let vs var](https://wangwei.one/posts/92c3001f.html) 。

####全局变量

函数外部声明的变量就是全局变量（global variable），它可以在函数内部读取。 

```javascript
let v = 1;

function f() {
    console.log(v);
}

f();// 1
```

#### 局部变量

在函数内部定义的变量，外部无法读取，称为“局部变量”（local variable）。

```javascript
function f(){
    let v = 1;
}

v // ReferenceError: v is not defined
```

函数内部定义的变量，会在该作用域内覆盖同名全局变量。 

```javascript
let v = 1;

function f(){
    let v = 2;
    console.log(v);
}

f(); // 2
console.log(v);// 1
```



### 函数内部的变量提升

这种现象只会发生在 `var` 生命的变量上，`let` 则不会。

```javascript
function foo(x) {
    if (x > 100) {
        var tmp = x - 100;
    }
    console.log(tmp);
}

foo(1000);
```



### 函数本身的作用域

函数本身也是一个值，也有自己的作用域。它的作用域与变量一样，就是其声明时所在的作用域，与其运行时所在的作用域无关。 

```javascript
let a = 1;
let x = function () {
    console.log(a);
};

function f() {
    let a = 2;
    x();
}

f();// 1
```

上面代码中，函数`x`是在函数`f`的外部声明的，所以它的作用域绑定外层，内部变量`a`不会到函数`f`体内取值，所以输出`1`，而不是`2`。

总之，函数执行时所在的作用域，是定义时的作用域，而不是调用时所在的作用域。

```javascript
let x = function () {
    console.log(a);
};

function y(f) {
    let a = 2;
    f();
}

y(x)
// ReferenceError: a is not defined
```

上面代码将函数`x`作为参数，传入函数`y`。但是，函数`x`是在函数`y`体外声明的，作用域绑定外层，因此找不到函数`y`的内部变量`a`，导致报错。

同样的，函数体内部声明的函数，作用域绑定函数体内部。



## 闭包

闭包（closure）是 Javascript 语言的一个难点，也是它的特色，很多高级应用都要依靠闭包实现。

理解闭包，首先必须理解变量作用域。前面提到，JavaScript 有两种作用域：全局作用域和函数作用域。函数内部可以直接读取全局变量。

```javascript
let n = 999;

function f1() {
    console.log(n);
}
f1();// 999
```

上面代码中，函数`f1`可以读取全局变量`n`。

但是，函数外部无法读取函数内部声明的变量。

```javascript
function f1() {
    let n = 999;
}
console.log(n); // ReferenceError: n is not defined
```

上面代码中，函数`f1`内部声明的变量`n`，函数外是无法读取的。

如果出于种种原因，需要得到函数内的局部变量。正常情况下，这是办不到的，只有通过变通方法才能实现。那就是在函数的内部，再定义一个函数。

```javascript
function f1() {
  let n = 999;
  function f2() {
　　console.log(n); // 999
  }
}
```

上面代码中，函数`f2`就在函数`f1`内部，这时`f1`内部的所有局部变量，对`f2`都是可见的。但是反过来就不行，`f2`内部的局部变量，对`f1`就是不可见的。这就是 JavaScript 语言特有的”链式作用域”结构（chain scope），子对象会一级一级地向上寻找所有父对象的变量。所以，父对象的所有变量，对子对象都是可见的，反之则不成立。

既然`f2`可以读取`f1`的局部变量，那么只要把`f2`作为返回值，我们不就可以在`f1`外部读取它的内部变量了吗！

```javascript
function f1() {
    let n = 999;

    function f2() {
        console.log(n);
    }
    return f2;
}

let result = f1();
result(); // 999
```

上面代码中，函数`f1`的返回值就是函数`f2`，由于`f2`可以读取`f1`的内部变量，所以就可以在外部获得`f1`的内部变量了。

闭包就是函数`f2`，即能够读取其他函数内部变量的函数。由于在 JavaScript 语言中，只有函数内部的子函数才能读取内部变量，因此可以把闭包简单理解成“定义在一个函数内部的函数”。闭包最大的特点，就是它可以“记住”诞生的环境，比如`f2`记住了它诞生的环境`f1`，所以从`f2`可以得到`f1`的内部变量。在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

闭包的最大用处有两个，一个是可以**读取函数内部的变量**，另一个就是**让这些变量始终保持在内存中**，即闭包可以使得它诞生环境一直存在。请看下面的例子，闭包使得内部变量记住上一次调用时的运算结果。

```javascript
function createIncrementor(start) {
    return function () {
        return start++;
    };
}

let inc = createIncrementor(5);

console.log(inc()); // 5
console.log(inc()); // 6
console.log(inc()); // 7
```

上面代码中，`start`是函数`createIncrementor`的内部变量。通过闭包，`start`的状态被保留了，每一次调用都是在上一次调用的基础上进行计算。从中可以看到，闭包`inc`使得函数`createIncrementor`的内部环境，一直存在。所以，闭包可以看作是函数内部作用域的一个接口。

为什么会这样呢？原因就在于`inc`始终在内存中，而`inc`的存在依赖于`createIncrementor`，因此也始终在内存中，不会在调用结束后，被垃圾回收机制回收。

闭包的另一个用处，**是封装对象的私有属性和私有方法**。

```javascript
function Person(name) {
    let _age;
    function setAge(n) {
        _age = n;
    }
    function getAge() {
        return _age;
    }

    return {
        name: name,
        getAge: getAge,
        setAge: setAge
    };
}

let p1 = Person('张三');
p1.setAge(25);
console.log(p1.getAge()); // 25
```

上面代码中，函数`Person`的内部变量`_age`，通过闭包`getAge`和`setAge`，变成了返回对象`p1`的私有变量。

注意，外层函数每次运行，都会生成一个新的闭包，而这个闭包又会保留外层函数的内部变量，所以内存消耗很大。因此不能滥用闭包，否则会造成网页的性能问题。



## 立即调用的函数表达式（IIFE）

> Immediately-Invoked Function Expression

在 Javascript 中，圆括号`()`是一种运算符，跟在函数名之后，表示调用该函数。比如，`print()`就表示调用`print`函数。

通常情况下，只对匿名函数使用这种“立即执行的函数表达式”。它的目的有两个：

- 一是不必为函数命名，避免了污染全局变量；
- 二是 IIFE 内部形成了一个单独的作用域，可以封装一些外部无法读取的私有变量。

```javascript
(function () {
    console.log("Hello world");
})();
```

```javascript
// 写法一
var tmp = newData;
processData(tmp);
storeData(tmp);

// 写法二
(function () {
    var tmp = newData;
    processData(tmp);
    storeData(tmp);
}());
```

上面代码中，写法二比写法一更好，因为完全避免了污染全局变量。 



## 箭头函数（Arrow functions）

还有一个非常简单和简洁的语法用于创建函数，这通常比函数表达式更好。 它被称为“箭头函数”，因为它看起来像这样：

```javascript
let func = (arg1, arg2, ...argN) => expression
```

等同于：

```javascript
let func = function(arg1, arg2, ...argN) {
  return expression;
}
```

来看几个例子：

```javascript
let sum = (a, b) => a + b;

/* The arrow function is a shorter form of:

let sum = function(a, b) {
  return a + b;
};
*/

console.log( sum(1, 2) ); // 3
```

```javascript
// same as
// let double = function(n) { return n * 2 }
let double = n => n * 2;

console.log( double(3) ); // 6
```

```javascript
let sayHi = () => console.log("Hello!");

sayHi();
```

```javascript
let age = 19;

let welcome = (age < 18) ?
    () => console.log('Hello') :
    () => console.log("Greetings!");

welcome(); // ok now
```



## 参考资料

- https://javascript.info/function-expressions-arrows
- http://javascript.ruanyifeng.com/grammar/function.html
