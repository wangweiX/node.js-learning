今天我们学习一下在JavaScript中如何声明变量和常量，以及`var`、`let`、`const`的区别。

## 变量

在ES6语法中，我们使用`let`关键字来声明变量。

```javascript
let user = 'John', age = 25, message = 'Hello';
```

或者

```javascript
let user = 'John';
let age = 25;
let message = 'Hello';
```



#### 命名规范

1. 名称必须仅包含字母，数字，符号$和_。
2. 第一个字符不能是数字。
3. 变量名称采用驼峰标记法。

例如：

```javascript
let userName = 'wangwei';
let test123 = 'hello world';
```



##  常量

使用`const`声明常量。声明为常量的变量不能再次被修改。

```javascript
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```



#### 大写常量

```javascript
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

let color = COLOR_ORANGE;
console.log(color); // #FF7F00
```



## Var vs Let

ES6中新增的 `let` 弥补了`var`中的一些不足。

#### 变量作用域

1. let 声明的变量，只在代码块中有效，var则声明了一个全局变量。

   ```javascript
   {
       var a = 10;
       let b = 1;
   }
   console.log(a); // 10
   console.log(b); // ReferenceError: b is not defined
   ```

2. 在for循环中，变量i是var声明的，在全局范围内都有效。所以每一次循环，新的i值都会覆盖旧值，导致最后输出的是最后一轮的i值。

   ```javascript
   let a = [];
   for (var i = 0; i < 10; i++) {
       a[i] = function () {
           console.log(i);
       };
   }
   a[6](); // 10
   ```

   改为let声明变量i，这样i只在循环体内有效。

   ```javascript
   let a = [];
   for (let i = 0; i < 10; i++) {
       a[i] = function () {
           console.log(i);
       };
   }
   a[6](); // 6
   ```



#### 不存在变量提升

let不像var那样会发生“变量提升”现象。所以，变量一定要在声明后使用，否则报错。

```javascript
console.log(x); // undefined
var x = 10; 
```

```javascript
console.log(x); // ReferenceError: x is not defined
let x = 10;
```



#### 暂时性死区(temporal dead zone, TDZ)

只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

ES6明确规定，如果区块中存在let和const命令，则这个区块对这些命令声明的变量从一开始就形成封闭作用域。只要在声明之前就使用这些变量，就会报错。

```javascript
var temp = 123;
if (true) {
    temp = 123; // ReferenceError: temp is not defined
    let temp;
}
```



#### 不允许重复声明

let不允许在相同作用域内重复声明同一个变量。

```javascript
(function () {
    let a = 1;
    let a = 2; // SyntaxError: Identifier 'a' has already been declared
})();
```



## 变量的解构赋值

本质上属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。例如：

```javascript
let [a, b, c] = [1, 2, 3];
```

对于初学者，这部分内容可以先大致了解一下，详情请查看：http://es6.ruanyifeng.com/#docs/destructuring



## 参考资料

- https://javascript.info/
- [《ES6标准入门》](http://es6.ruanyifeng.com/)