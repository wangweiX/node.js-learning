在 [前面](https://wangwei.one/posts/b5949fa3.html) 我们学习了JavaScript中如何创建对象以及对象属性的操作，本篇将深入学习 Object 属性的一些特性：**Enumerable**、**Writable**、**Configurable**.

## Property flags

我们先来看下下面这段代码：

```javascript
// My beloved object ob
let ob = {a: 1};

// Accessing to a property
console.log(ob.a); // => 1

// Modifying the value of a property
ob.a = 0;
console.log(ob.a); // => 0;

// Creating a new property
ob.b = 2;
console.log(ob.b); // => 2

// Deleting a property
delete ob.b;
console.log(ob.b); // => undefined
```



### Object.getOwnPropertyDescriptor

获取对象属性的描述，语法：

```javascript
let descriptor = Object.getOwnPropertyDescriptor(obj, propertyName);
```

查看上面的例子中对象 `ob` 属性 `a` ：

```javascript
let descriptor = Object.getOwnPropertyDescriptor(ob, 'a');
console.log(descriptor);
// { value: 0, writable: true, enumerable: true, configurable: true }
```

对象 `ob` 的属性是 enumerable、writable、configurable，什么意思呢？

- enumerable（可枚举）：可以使用 `for...in` 方法遍历对象的所有属性。也能通过 `Object.keys` 返回一个对象的所有的属性。
- writable（可修改）：可以修改对象的属性值。
- configurable（可配置）：可以修改属性的行为，可以将属性改为non-enumerable、non-writable 甚至是 non-configurable。可配置的属性是唯一能够通过 `delete` 操作删除的属性。



### Object.getOwnPropertyDescriptors

获取对象所有属性的描述，语法：

```javascript
let descriptors = Object.getOwnPropertyDescriptor(obj);
```

例如：

```javascript
let user = {
    name: 'John',
    surname: 'Smith'
};

console.log(Object.getOwnPropertyDescriptors(user));
{ name:
// { value: 'John',
//     writable: true,
//     enumerable: true,
//     configurable: true },
//     surname:
//     { value: 'Smith',
//         writable: true,
//         enumerable: true,
//         configurable: true } }
```



### Object.defineProperty

一次性定义对象的所有属性，语法：

```javascript
Object.defineProperty(obj, propertyName, descriptor)
```

例如：

```javascript
let user = {};
Object.defineProperties(user, {
    name: {value: "John", writable: false},
    surname: {value: "Smith", writable: false},
});
```

与 `Object.getOwnPropertyDescriptors` 配合使用可以克隆对象所有的属性：

```
let clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj));
```

例子：

```javascript
let user = {
    name: 'John',
    surname: 'Smith'
};

let user1 = {};

Object.defineProperties(user1, Object.getOwnPropertyDescriptors(user));
console.log(Object.getOwnPropertyDescriptors(user1));
// { name:
// { value: 'John',
//     writable: true,
//     enumerable: true,
//     configurable: true },
//     surname:
//     { value: 'Smith',
//         writable: true,
//         enumerable: true,
//         configurable: true } } 
```



## 参考资料

- http://javascript.info/property-descriptors
- http://arqex.com/967/javascript-properties-enumerable-writable-configurable