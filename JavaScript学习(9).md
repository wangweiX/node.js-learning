Iterator 接口的目的，就是为所有数据结构，提供了一种统一的访问机制，即`for...of`循环）。当使用`for...of`循环遍历某种数据结构时，该循环会自动去寻找 Iterator 接口。

ES6 规定，一个数据结构只要具有`Symbol.iterator`属性，就可以认为是“可遍历的”（iterable）。

## Symbol.iterator

为了便于理解 `Symbol.iterator`  ，我们先来造个轮子。

先创建一个对象 `rang`，我们希望能够遍历出 `from` 到 `to` 之间的数字。

```javascript
let rang = {
    from: 1,
    to: 5
};
```

为了能够实现这个效果，我们需要为 rang 创建一个名为 `Symbol.iterator` 的方法。

- 当 rang 执行 for ... of 循环时，其中的 `Symbol.iterator` 方法将会被调用，如果没有则会报错。
- 这个方法必须返回一个替代器 —— 含有 `next()` 方法的对象。
- 当 `for ... of` 想要获取下一个值时，`next()` 方法将会被调用。
- `next()` 方法必须返回形如 `{done: Boolean, value: any}` 的对象，当 `done = true` 时表示迭代完成，否则 `value` 必须为新的值。

```javascript
let rang = {
    from: 1,
    to: 5,

    [Symbol.iterator]() {
        return {
            current: this.from,
            last: this.to,

            next() {
                if (this.current <= this.last) {
                    return {done: false, value: this.current++}
                } else {
                    return {done: true}
                }
            }
        }
    }
};

for (let num of rang) {
    console.log(num);
}
// 1
// 2
// 3
// 4
// 5
```



ES6 的有些数据结构原生具备 Iterator 接口（比如数组），即不用任何处理，就可以被`for...of`循环遍历。原因在于，这些数据结构原生部署了`Symbol.iterator`属性，另外一些数据结构没有（比如对象）。凡是部署了`Symbol.iterator`属性的数据结构，就称为部署了遍历器接口。调用这个接口，就会返回一个遍历器对象。

原生具备 Iterator 接口的数据结构如下：

- Array
- Map
- Set
- String
- TypedArray
- 函数的 arguments 对象
- NodeList 对象



## 字符串迭代器

`string` 是可迭代，可以循环遍历出每个字节，对于包含特殊的表情符号的字符串也适用。

```javascript
for (let char of 'test') {
    console.log(char);
}
// t
// e
// s
// t

let str = '𝒳😂';
for (let char of str) {
    console.log( char ); // 𝒳, and then 😂
}
```



## 参考资料

- http://es6.ruanyifeng.com/#docs/iterator
- https://javascript.info/iterable

