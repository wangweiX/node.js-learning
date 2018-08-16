---
title: JavaScript学习(3) | Primitive Data Type
tags:
  - JavaScript
categories: coding
abbrlink: f88dc8a9
date: 2018-01-03 22:43:00
---

JavaScript中有7种基本的数据类型：`undefined`、`null`、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）、Symbol。本篇文章先来简要介绍一下他们的特性，后面的文章会分别对它们做详细的说明介绍。

<!--more-->

javascript 中的变量可以包含任何类型的数据。 一个变量可以在某一时刻是字符串类型，过会就可能变成数值类型，所以说javascript是一门动态类型语言。

```javascript
// no error
let message = "hello";
console.log(message); // hello

message = 123456;
console.log(message); // 123456
```



## number

JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。

```javascript
let n = 123;
n = 12.345;
```

除常规数字外，还有所谓的“特殊数值”，它们也属于这种类型：`Infinity`，`-Infinity`和`NaN`。

##### Infinity

```javascript
console.log(1/0); // Infinity

console.log(-1/0); // -Infinity
```

##### NaN

```javascript
console.log( "not a number" / 2 ); // NaN, such division is erroneous
```

对`NaN`的任何算术操作都只会得到 `NaN` 结果。

```javascript
console.log( "not a number" / 2 + 5 ); // NaN
```

> 更多有关 number 的用法与介绍，请查看：
>
> http://javascript.ruanyifeng.com/grammar/number.html
>
> http://es6.ruanyifeng.com/#docs/number



## string

使用单引号、双引号或者反引号表示，其中反引号用于表达式替换。

```javascript
let str = "Hello";
console.log(str); // Hello

let str2 = 'Single quotes are ok too';
console.log(str2); // Single quotes are ok too

let phrase = `can embed ${str}`;
console.log(phrase,'hello'); // can embed Hello hello
```

> javascript中没有 `char` 的概念。
>
> 更多有关 string 的用法与介绍，请查看：
>
> http://es6.ruanyifeng.com/#docs/string
>
> http://javascript.ruanyifeng.com/grammar/string.html



## boolean

```javascript
let isGreater = 4 > 1;

console.log( isGreater ); // true (the comparison result is "yes")
```



## null

在JavaScript中，`null`不是“对不存在的对象的引用”或者像其他语言中的“null pointer”。它只是一个特殊的值，表示“nothing”，“empty”或“value unknown”的意思。

```javascript
let x = null;
console.log(x); // null
```



## undefined

`undefined` 表示变量未被赋值，如果声明了变量但未被赋值，则其值完全未定义：

```javascript
let x = 123;

x = undefined;

console.log(x); // "undefined"
```

通常，我们使用`null`将“empty”或“unkown”值赋予变量，`undefined`仅用于检查，以查看变量是否已分配。



## Objects and Symbols

##### Objects

```javascript
let usr = {
    name : "wangwei",
    age : 23,
};
console.log(typeof usr); // object
```

> 详细介绍：https://wangwei.one/posts/b5949fa3.html



##### Symbols

`symbol` 类型用于创建对象的唯一标示，这个后面部分详细说明，这里暂且略过。

```javascript
let s = Symbol();

typeof s // "symbol"
```

> 详细介绍：https://wangwei.one/posts/f8560033.html



## typeof

`typeof` 可以返回变量的类型。

```javascript
console.log(typeof undefined);// "undefined"

console.log(typeof 0); // "number"

console.log(typeof true); // "boolean"

console.log(typeof "foo"); // "string"

console.log(typeof Symbol("id")); // "symbol"

console.log(typeof Math);// "object"

console.log(typeof null);// "object"

console.log(typeof function () {

}); // "function"
```



## 参考资料

- https://javascript.info/types

- http://es6.ruanyifeng.com/?search=Symbols&x=0&y=0#docs/symbol

  