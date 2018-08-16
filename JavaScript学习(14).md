JavaScript中没有"子类"和"父类"的概念，也没有"类"（class）和"实例"（instance）的区分，全靠一种很奇特的"原型链"（prototype chain）模式，来实现继承。

## [[Prototype]]

在 JavaScript 中，对象有一个隐藏的属性 `[[Prototype]]` ，该属性的值要么为`null` ，要么指向一个对象，这个所指向的对象就被称为`原型`。

![object-prototype-empty](https://img.i7years.com/blog/object-prototype-empty@2x.png)



通过 `[[Prototype]]` 我们继承一个对象的属性与方法，例如：

```javascript
let animal = {
    eats: true,
    walk() {
        console.log("Animal walk");
    }
};

let rabbit = {
    jumps: true,
    __proto__: animal
};

let longEar = {
    earLength: 10,
    __proto__: rabbit
};

// we can find both properties in rabbit now:
console.log(longEar.eats); // true (**)
console.log(longEar.jumps); // true
console.log(longEar.earLength); // true

longEar.walk(); // Animal walk
```

在上面的例子中，这三个对象的关系如下：`longEar` --> `rabbit` --> `animal`。我们可以这样表述：`animal` 是 `rabbit` 的原型，或者 `rabbit` 原型继承自 `animal` 。

**注意**

1. 对象的之间的继承关系，不能形成一个环型，类似于： A --> B --> --> A。
2. 对象的 `__proto__` 属性，只能null或者对象，不能为其他数据类型。



## 读写规则

原型只适用于属性的读取，但是对于数据属性的删除与修改操作，只能对子类产生影响，对原型没有影响。

```javascript
let animal = {
    eats: true,
    walk() {
        /* this method won't be used by rabbit */
    }
};

let rabbit = {
    __proto__: animal
};

rabbit.walk = function() {
    console.log("Rabbit! Bounce-bounce!");
};

rabbit.walk(); // Rabbit! Bounce-bounce!

console.log(rabbit.eats); // true

delete rabbit.eats;

console.log(rabbit.eats); // true
console.log(animal.eats); // true
```

对于 `getters/setters` 方法，在调用时会向上调用到原型里面的方法上去。例如:

```javascript
let user = {
    name: "John",
    surname: "Smith",

    set fullName(value) {
        [this.name, this.surname] = value.split(" ");
    },

    get fullName() {
        return `${this.name} ${this.surname}`;
    }
};

let admin = {
    __proto__: user,
    isAdmin: true
};

console.log(admin.fullName); // John Smith (*)

// setter triggers!
admin.fullName = "Alice Cooper"; // (**)

console.log(user.name); // John
console.log(admin.name); // Alice
```



## this 

函数中的 `this`值通常是由函数的调用方来定义。因此，每次执行函数，函数内的 `this`值可能都不一样。

在上面的这个例子中，this 指向的是哪个对象？答案是： `admin` 。

`this` 不受原型的影响。无论在哪里调用，不管是对象中还是在原型中，一个方法里面的 `this` 总是表示 `.` 号前面的对象。例如：

```javascript
// animal has methods
let animal = {
    walk() {
        if (!this.isSleeping) {
            alert(`I walk`);
        }
    },
    sleep() {
        this.isSleeping = true;
    }
};

let rabbit = {
    name: "White Rabbit",
    __proto__: animal
};

// modifies rabbit.isSleeping
rabbit.sleep();

console.log(rabbit.isSleeping); // true
console.log(animal.isSleeping); // undefined (no such property in the prototype)
```



## 参考资料

- http://javascript.info/prototype-inheritance
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
- https://juejin.im/post/5b6676e6f265da0fa00a3a12
- http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html