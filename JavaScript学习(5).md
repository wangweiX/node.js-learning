[前面](https://wangwei.one/posts/f88dc8a9.html) 我们介绍了JavaScript中的6种原生的数据类型，

## 创建

### 初始化

```javascript
let o1 = new Object();
let o2 = {}; // 推荐这种方式

let user = { 		    // an object
   name: "John",	    // by key "name" store value "John"
   age: 30,			    // by key "age" store value 30
   "likes birds": true   // multiword property name must be quoted
};
```



### 创建复杂对象

```javascript
let myData = {
    myValue: 123,
    bas: [{
        myItem: 1
    },
        {
            myItem: 2
        },
        {
            myItem: 3
        }]
};
console.log(myData.myValue); // 123
console.log(myData.bas[0].myItem); // 1
console.log(myData.bas[2].myItem); // 2
```



### 构造器函数

但我们需要创建大量类似的对象时，使用 `{...}` 语法不便于代码复用，这里需要使用 `constructor funcation（构造器函数）` 。例如：

```javascript
function User(name) {
    this.name = name;
    this.isAdmin = false;
}

let user = new User("Jack");

console.log(user.name); // Jack
console.log(user.isAdmin); // false
```

可以简写为：

```javascript
let user = new function () {
    this.name = 'Jack';
    this.isAdmin = false;
};

console.log(user.name); // Jack
console.log(user.isAdmin); // false
```



## 属性操作

#### 初始化属性

```javascript
let user = { 		    // an object
   name: "John",	    // by key "name" store value "John"
   age: 30,			    // by key "age" store value 30
   "likes birds": true   // multiword property name must be quoted
};
```



#### 添加属性

点运算符和方括号运算符，不仅可以用来读取值，还可以用来赋值。 

```javascript
// add field
user.isAdmin = true;
user["hobby"] = 'reading';
```



#### 删除属性

`delete`命令用于删除对象的属性，删除成功后返回`true`。

```javascript
// delete field
delete user.age;
delete user["likes birds"];
```



#### 查询属性

```javascript
// get fields of the object:
console.log(user.name);
console.log(user["likes birds"]); // true
```



### 查询所有属性

```javascript
console.log(Object.keys(user));
[ 'name', 'age', 'likes birds' ]
```



### in 运算符

`in`运算符用于检查对象是否包含某个属性（注意，检查的是键名，不是键值），如果包含就返回`true`，否则返回`false`。

```javascript
var obj = { p: 1 };
console.log('p' in obj);
 // true
```

`in`运算符的一个问题是，它不能识别哪些属性是对象自身的，哪些属性是继承的。 

```javascript
var obj = { p: 1 };
console.log('toString' in obj);
 // true
```



### for...in循环

`for...in`循环用来遍历一个对象的全部属性。 

```javascript
let obj = {a: 1, b: 2, c: 3};

for (let i in obj) {
    console.log(obj[i]);
}
```

`for...in`循环有两个使用注意点。

> - 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。
> - 它不仅遍历对象自身的属性，还遍历继承的属性。

举例来说，对象都继承了`toString`属性，但是`for...in`循环不会遍历到这个属性。 

```javascript
let obj = {};
// toString 属性是存在的
obj.toString;// toString() { [native code] }

for (let p in obj) {
    console.log(p);
} // 没有任何输出
```

如果继承的属性是可遍历的，那么就会被`for...in`循环遍历到。但是，一般情况下，都是只想遍历对象自身的属性，所以使用`for...in`的时候，应该结合使用`hasOwnProperty`方法，在循环内部判断一下，某个属性是否为对象自身的属性。 

```javascript
let person = {name: '老张'};

for (let key in person) {
    if (person.hasOwnProperty(key)) {
        console.log(key);
    }
}
// name
```



## Object克隆与合并

如果我们想要深度复制一个对象，可以有以下两种方式：

1）属性遍历，这种方法不是很优雅

```javascript
let user = {
    name: "John",
    age: 30,
    "likes birds": true
};

let clone = {};

for (let key in user) {
    clone[key] = user[key];
}

console.log(Object.keys(clone));
// [ 'name', 'age', 'likes birds' ]
```



2）使用 `Object.assign` ，语法如下：

```javascript
Object.assign(dest, src1, src2, src3... srcN)

// 将 src1 ~ srcN 中的属性copy 到 dest 中
```

例如：

```javascript
let user = {
    name: "John",
    age: 30,
    "likes birds": true
};

let user1 = {
    hobby: "reading"
};

let clone = {};

Object.assign(clone, user, user1);

console.log(Object.keys(clone)); 
// [ 'name', 'age', 'likes birds', 'hobby' ]
```



## 方法

现实世界中，一个对象除了拥有属性特征外，还有一定的行为特征， 例如一个人除了身高、年龄外，还会唱歌、阅读、弹吉他等等。当我们用一个对象来代表某一个实体时，这就是一个面向对象的编程思想。OOP

例如，`user` 拥有一个 `sayHi` 的功能：

```javascript
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
  console.log("Hello!");
};

user.sayHi(); // Hello!
```

可以更简单地声明为：

```javascript
// these objects do the same

let user = {
    sayHi: function() {
        console.log("Hello");
    }
};

// method shorthand looks better, right?
let user = {
    sayHi() { // same as "sayHi: function()"
        console.log("Hello");
    }
};
```

我们可以把 `sayHi` 放到 user 的构造器中去：

```javascript
function User(name, age) {
    this.name = name;
    this.age = age;

    this.sayHi = function () {
        console.log("Hello")
    }
}

let user = new User('Jack', 25);
user.sayHi();
```



## this

在 javascript 中，`this` 不像其他编程语言中的一样，首先，它能够被用在任何方法中。

```javascript
function sayHi() {
    console.log( this.name ); // 没有语法错误
}

sayHi();
```

`this` 的值，需要在运行的时候才能被确定，它有可能代表任何事情。例如下面 `sayHi()` 中的 `this` 在运行时，分别代表着 `user`、`admin`。

````javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
    console.log( this.name );
}

// use the same functions in two objects
user.f = sayHi;
admin.f = sayHi;

// these calls have different this
// "this" inside the function is the object "before the dot"
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (dot or square brackets access the method – doesn't matter)
````



## Object.keys, values, entries

- [Object.keys(obj)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) – 返回对象的属性数组。
- [Object.values(obj)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/values) – 返回对象的属性值数组。
- [Object.entries(obj)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) – 返回对象属性及值的数组。

```javascript
let user = {
    name: 'wangwei',
    age: 25,
    hobby: 'reading book'
};

console.log(Object.keys(user));
// [ 'name', 'age', 'hobby' ]

console.log(Object.values(user));
// [ 'wangwei', 25, 'reading book' ]

console.log(Object.entries(user));
// [ [ 'name', 'wangwei' ],
//   [ 'age', 25 ],
//   [ 'hobby', 'reading book' ] ]
```



## 参考资料

- https://javascript.info/object#literals-and-properties
- http://javascript.ruanyifeng.com/grammar/object.html
- https://javascript.info/object-methods#this-is-not-bound