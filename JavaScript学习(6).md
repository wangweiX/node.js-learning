ES5 的对象属性名都是字符串，这容易造成属性名的冲突。比如，你使用了一个他人提供的对象，但又想为这个对象添加新的方法（mixin 模式），新方法的名字就有可能与现有方法产生冲突。如果有一种机制，保证每个属性的名字都是独一无二的就好了，这样就从根本上防止属性名的冲突。这就是 ES6 引入`Symbol`的原因。

ES6 引入了一种新的原始数据类型`Symbol`，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：`undefined`、`null`、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

Symbol 值通过`Symbol`函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。



## 声明

 声明方式：

```javascript
// id is a new symbol
let id = Symbol();
```

我们也可以为其添加名称：

```javascript
// id is a symbol with the description "id"
let id = Symbol("id");
```

由于 `Symbol` 对象代表着唯一标识，即使名称一样，其对象也不相同：

```javascript
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 == id2); // false
```

如果想要创建相同的`Symbol`，可以使用 `Symbol.for` ：

```javascript
let id1 = Symbol.for("id");
let id2 = Symbol.for("id");

console.log(id1 == id2); // false
```



## 对象属性

使用 `Symbol` 作为一个对象的属性，方式如下：

```javascript
let id = Symbol("id");

let user = {
    name: "John",
    age: 30,
    [id]: 123 // not just "id: 123"
};

console.log(user[id]);
```



### 对 for...in 隐藏

Symbol 的属性不会参与 for...in 循环。

```javascript
let id = Symbol("id");
let user = {
    name: "John",
    age: 30,
    [id]: 123
};

for (let key in user) console.log(key); // name, age (no symbols)

// the direct access by the symbol works
console.log( "Direct: " + user[id] );
```

不过，`Object.assign` 可以对 Symbol 属性进行复制

```javascript
let id = Symbol("id");
let user = {
    [id]: 123
};

let clone = Object.assign({}, user);

console.log( clone[id] ); // 123
```



## 参考资料

- https://javascript.info/symbol#system-symbols
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol

