---
title: JavaScript学习(7) | Data Type —— Array
tags:
  - JavaScript
categories: coding
abbrlink: a1e7623d
date: 2018-01-07 22:43:00
---

本篇文章重点介绍JavaScript中数组的特性。

<!--more-->

## 声明

### 创建

```javascript
let arr = new Array();
let arr = []; // 这种方式更为常见

// e.g: 
let fruits = ["Apple", "Orange", "Plum"];
```

与java这种强类型不同的是，javascript中的数组可以存储任意类型的数据。

```javascript
let arr = [ 'Apple', { name: 'John' }, true, function() { alert('hello'); } ];
```

### 数组判断

> Array.isArray()

```javascript
console.log(Array.isArray({})); // false

console.log(Array.isArray([])); // true
```



## 添加/移除元素

> javascript中的数组，头部和尾部均支持元素的添加和移除，可以用来实现stack（栈）、quene（队列）、deque（双端队列）特性。

#### unshift and shift

- `unshift`：数组头部插入一个元素
- `shift`：数组头部移除一个元素

```javascript
let nums2 = [ 1, 2, 3, 5, 8 ];
nums2.unshift(1); // insert 1 to the first of an array
console.log(nums2); // [ 1, 1, 2, 3, 5, 8 ];

nums2.shift(); // delete 1 to the first of an array
console.log(nums2); // [ 1, 2, 3, 5, 8 ];
```

#### push & pop

> 栈：LIFO（后进先出）

- push：数组尾部添加一个元素
- pop：数组尾部移除一个元素

```javascript
let nums = [1, 2, 3, 4, 5, 6];
nums.push(8);
console.log(nums); // [ 1, 2, 3, 4, 5, 6, 8 ]

nums.pop();
console.log(nums); // [ 1, 2, 3, 4, 5, 6 ]
```

> 性能比较：尾部 `push/pop` 的操作速度比头部的 `shift/unshift` 操作要快，因为头部插入/删除元素，都会影响到数组中所有元素下标的变化，元素越多，速度越慢。

#### splice

> `splice(pos, deleteCount, ...items)` ：删除索引为 `pos` ，数量为`deleteCount`的元素，并且插入元素  items

```javascript
let arr3 = ['cat', 'rat', 'bat', 'dog', 'pig', 'horse'];
arr3.splice(2, 2, 'chicken'); // delete item
console.log(arr3); // [ 'cat', 'rat', 'chicken', 'pig', 'horse' ]


```

#### concat

> `concat(...items)`：拼接多个数组，并返回一个新的数组

```javascript
let arr1 = ['cat', 'rat', 'bat'];
let arr2 = ['dog', 'pig', 'horse'];

let arr3 = arr1.concat(arr2);
console.log(arr3);
```

#### slice

> `slice(start,end)`：复制数组元素

```javascript
let vegetables = ['Cabbage', 'Turnip', 'Radish', 'Carrot'];
console.log(vegetables.slice());
// [ 'Cabbage', 'Turnip', 'Radish', 'Carrot' ]
```



## 搜索

#### filter

语法：

```javascript
let results = arr.filter(function(item, index, array) {
  // should return true if the item passes the filter
});
```

例子：

```javascript
let users = [
    {id: 1, name: "John"},
    {id: 2, name: "Pete"},
    {id: 3, name: "Mary"}
];

let someUsers = users.filter(item => item.id <= 2);
console.log(someUsers);
```

#### indexOf & lastIndexOf & includes

- `arr.indexOf(item, from)`：从索引 `from` 位置开始搜索 `item`，存在则返回对应的索引，不存在则返回 `-1`。
- `arr.lastIndexOf(item, from)`：与`indexof`类似，只是方向为从右向左进行搜索。
- `arr.includes(item, from)` ：从索引 `from` 位置开始搜索 `item`，存在则返回 `true` ，反之返回 `false`。

```javascript
let arr = ["Apple", "Orange", "Pear"];

console.log(arr.indexOf('Apple'));
console.log(arr.lastIndexOf('Orange'));
console.log(arr.includes('Pear'));
```

#### find

语法：

```javascript
let result = arr.find(function(item, index, array) {
  // should return true if the item is what we are looking for
});
```

例子：

```javascript
let users = [
    {id: 1, name: "John"},
    {id: 2, name: "Pete"},
    {id: 3, name: "Mary"}
];

let user = users.find(item => item.id === 1);

console.log(user.name); // John
```

#### findIndex

与 `find` 类似，只不过返回的是元素的下标。

````javascript
let users = [
    {id: 1, name: "John"},
    {id: 2, name: "Pete"},
    {id: 3, name: "Mary"}
];

let userIndex = users.findIndex(item => item.id === 2);

console.log(userIndex); // John
````



## 数组转换

#### arr.map

语法：

```javascript
let result = arr.map(function(item, index, array) {
  // returns the new value instead of item
})
```

例子：

```javascript
let users = [
    {id: 1, name: "John"},
    {id: 2, name: "Pete"},
    {id: 3, name: "Mary"}
];

let userIds = users.map(item => item.id);
console.log(userIds); // [ 1, 2, 3 ]
```

#### reverse

```javascript
let arr = ["Apple", "Orange", "Pear"];
console.log(arr.reverse()); // [ 'Pear', 'Orange', 'Apple' ]
```

#### split & join

```javascript
// split
let str = 'Apple Orange Pear';
console.log(str.split(' ')); // [ 'Apple', 'Orange', 'Pear' ]

// join
let arr = [ 'Apple', 'Orange', 'Pear' ];
console.log(arr.join(',')); // Apple,Orange,Pear
```

#### sort(fn)

```javascript
let nums = [2, 5, 3, 6, 2 - 1, -6, -1, 0, 7];
console.log(nums.sort((a, b) => a - b)); // [ -6, -1, 0, 1, 2, 3, 5, 6, 7 ]
```

#### reduce

`reduce(func, initial)`：对数组中的数值进行累计运算（例如：累加、累乘等等），前一个元素的运算结果将会带到下一个元素的运算中去。

```javascript
const array1 = [1, 2, 3, 4];
const addReducer = (accumulator, currentValue) => accumulator + currentValue;
// 1 + 2 + 3 + 4
console.log(array1.reduce(addReducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(addReducer, 5));
// expected output: 15

const multipReducer = (accumulator, currentValue) => accumulator * currentValue;
// 1 * 2 * 3 * 4
console.log(array1.reduce(multipReducer));
// expected output: 24

// 5 * 1 * 2 * 3 * 4
console.log(array1.reduce(multipReducer, 5));
// expected output: 120
```



## 遍历

#### 方式一

```javascript
let arr = ["Apple", "Orange", "Pear"];

for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
// Apple
// Orange
// Pear
```

#### 方式二

```javascript
let arr = ["Apple", "Orange", "Pear"];

for (let fruit of arr) {
    console.log(fruit);
}
// Apple
// Orange
// Pear
```

#### 方式三

```javascript
let arr = ["Apple", "Orange", "Pear"];

arr.forEach(function (item) {
   console.log(item);
});
// Apple
// Orange
// Pear
```



## 参考资料

- https://javascript.info/array
- https://javascript.info/array-methods
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array