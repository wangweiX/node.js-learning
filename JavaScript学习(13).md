---
title: JavaScript学习(13) | Property getters and setters
tags:
  - JavaScript
categories: coding
abbrlink: 57ede93d
date: 2018-01-13 22:43:00
---

JavaScript中有两种属性，一种是我们前面一直在介绍的数据属性（*data properties*），另外一种就是访问者属性（*accessor properties*）。

<!--more-->

## Getters and setters

在对象中，访问者属性使用 `get` 和 `set` 方法标示，形如：

```javascript
let obj = {
  get propName() {
    // getter, the code executed on getting obj.propName
  },

  set propName(value) {
    // setter, the code executed on setting obj.propName = value
  }
};
```

例如，我们有个如下的 user 对象：

```javascript
let user = {
  name: "John",
  surname: "Smith"
};
```

现在想要增加一个 `fullName` 属性，我们不想复制原有的name信息，这里我们可以使用访问者属性的方式来实现，使用 getter 方法：

```javascript
let user = {
  name: "John",
  surname: "Smith",

  get fullName() {
    return `${this.name} ${this.surname}`;
  }
};

console.log(user.fullName); // John Smith
```

如果我们想要给 `fullName` 属性赋值，那么就需要 setter 方法：

```javascript
let user = {
    name: "John",
    surname: "Smith",

    get fullName() {
        return `${this.name} ${this.surname}`;
    },

    set fullName(value) {
        [this.name, this.surname] = value.split(" ");
    }
};

// set fullName is executed with the given value.
user.fullName = "Alice Cooper";

console.log(user.name); // Alice
console.log(user.surname); // Cooper
```

`fullName` 其实是一个虚拟的属性，它实际上并不存在于对象之中。

> 访问者属性只能通过 get/set 方法来进行访问。一个属性不能即是访问者属性，又是数据属性，二者只能选其一。



## Accessor descriptors

访问者属性的描述与数据属性的描述有所不同。它没有 `value` 和 `writable` 值，取而代之的是 `get` 与 `set` 函数，因此访问者属性的描述包含如下几个值：

- **get**：查询属性时会被调用的方法；
- **set**：设置属性时会被调用的方法；
- **enumerable**：同数据属性一样；
- **configurable**：同数据属性一样；

例如：

```javascript
function Circle(radius) {
    this.radius = radius;
}

Object.defineProperty(Circle.prototype, 'circumference', {
    get: function () {
        return 2 * Math.PI * this.radius;
    }
});

Object.defineProperty(Circle.prototype, 'area', {
    get: function () {
        return Math.PI * this.radius * this.radius;
    }
});

let c = new Circle(10);
console.log(c.area); // 314.1592653589793
console.log(c.circumference); // 62.83185307179586
```



## Smarter Getters/Setters

对于 getter/setter 的属性，我们可以使用下划线“_” 来进行修饰，例如：

```javascript
let user = {
    age: '25',

    get name() {
        return this._name;
    },

    set name(value) {
        if (value.length < 4) {
            console.log('Name is too short, need at least 4 characters');
            return;
        }
        this._name = value;
    }
};

user.name = 'John';
console.log(user.name); // John
```

从技术上讲，外部代码仍然可以使用 `user._name` 直接访问该名称。 但是有一个众所周知的协议，即以下划线“_”开头的属性是内部的，不应该从对象外部触及。



## 参考资料

- http://javascript.info/property-accessors

- https://javascriptplayground.com/es5-getters-setters/

  

