本篇文章我们来学习一下 JavaScript 中的集合对象 `Map` 和 `Set` 。

## Map

`map` 键值对，和 java 中的 map集合特性一致，只是语法上稍微有些差别。

### 基本用法

主要方法如下：

- `new Map()` – 创建Map.
- `map.set(key, value)` – 存储key-value键值对
- `map.get(key)` – 查询`key`对应的value值,如果不存在，则返回 `undefined`.
- `map.has(key)` – 判断 `key` 否则存在，有则返回 `true`，反之返回 `false`.
- `map.delete(key)` – 删除 key 对应的键值对。
- `map.clear()` – 清空map。
- `map.size` – 返回map对应的元素数量。

```javascript
let map = new Map();

let john = {name: "John"};

map.set('1', 'str1') // a string key
    .set(1, 'num1') // a numeric key
    .set(true, 'bool1') // a boolean key
    .set(john, 123) // a object key
    .set(NaN, 'hello')
    .set(NaN, 'World');

console.log(map.size); // 4

console.log(map.has(john)); // true

console.log(map.delete(john)); // true

console.log(map.get(1)); // 'num1'
console.log(map.get('1')); // 'str1'
console.log(map.get(NaN)); // world

map.clear();
console.log(map.size); // 0
```

> map.set 会返回 map自身，所以我们可以链式调用set接口



### key 唯一性

键的比较是基于 [SameValueZero](https://tc39.github.io/ecma262/#sec-samevaluezero) 算法：`NaN` 是与 `NaN` 相同的（虽然 `NaN !== NaN`），剩下所有其它的值是根据 === 运算符的结果判断是否相等。在目前的ECMAScript规范中，`-0`和`+0`被认为是相等的，尽管这在早期的草案中并不是这样。有关详细信息，请参阅[浏览器兼容性](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map#%E6%B5%8F%E8%A7%88%E5%99%A8%E5%85%BC%E5%AE%B9%E6%80%A7) 表中的“value equality for -0 and 0”。



### 遍历

- `keys()`：返回键名的遍历器。
- `values()`：返回键值的遍历器。
- `entries()`：返回所有成员的遍历器。
- `forEach()`：遍历 Map 的所有成员。

```javascript
let map = new Map();

map.set('a', 1)
    .set('b', 2)
    .set('c', 3);

for (let key of map.keys()) {
    console.log(key);
}

for (let value of map.values()) {
    console.log(value);
}

for (let entry of map.entries()) {
    console.log(entry[0], entry[1]);
}

for (let [key, value] of map) {
    console.log(key, value);
}

map.forEach(function (value, key) {
    console.log(key, value);
});
```

> 更多有关Map的使用介绍请查看：http://es6.ruanyifeng.com/#docs/set-map#Map



### 与其他数据类型之间的转换

#### Map ===> Array

```javascript
let map = new Map();
map.set('a', 1)
    .set('b', 2)
    .set('c', 3);

console.log(Array.from(map)); 
// [ [ 'a', 1 ], [ 'b', 2 ], [ 'c', 3 ] ]

console.log([...map]); 
// [ [ 'a', 1 ], [ 'b', 2 ], [ 'c', 3 ] ]
```

####Array ===> Map

```javascript
let array = [ [ 'a', 1 ], [ 'b', 2 ], [ 'c', 3 ] ];
let map = new Map(array);
console.log(map);
// Map { 'a' => 1, 'b' => 2, 'c' => 3 }
```

#### Map ===> Object

> 如果有非字符串的键名，那么这个键名会被转成字符串，再作为对象的键名。

```javascript
const map = new Map();
map.set("a", 1);
map.set("b", 2);
map.set("c", 3);
map.set('keyString', "value associated with 'a string'");
map.set('keyObj', 'value associated with keyObj');
map.set('keyFunc', 'value associated with keyFunc');
map.set(0, 'zero');
map.set(1, 'one');
map.set('contra', {description: 'Asynchronous flow control'});
map.set('dragula', {description: 'Drag and drop'});
map.set('woofmark', {description: 'Markdown and WYSIWYG editor'});

// 此种方法更快 635 ms
const strMapToObj = (map) => {
    let obj = {};
    for(let prop of map){
        obj[prop[0]] = prop[1];
    }
    return obj;
};
console.log(strMapToObj(map));

// 此种方法慢 4704 ms
const strMapToObj2 = (map) => {
    let obj = Array.from(map).reduce((obj, [key, value]) => (
        Object.assign(obj, { [key]: value }) // Be careful! Maps can have non-String keys; object literals can't.
    ), {});
    return obj;
};

console.log(strMapToObj2(map)); 

// { '0': 'zero',
//     '1': 'one',
//     a: 1,
//     b: 2,
//     c: 3,
//     keyString: 'value associated with \'a string\'',
//     keyObj: 'value associated with keyObj',
//     keyFunc: 'value associated with keyFunc',
//     contra: { description: 'Asynchronous flow control' },
//     dragula: { description: 'Drag and drop' },
//     woofmark: { description: 'Markdown and WYSIWYG editor' } }
```

#### Object ===> Map

```javascript
let user = {
    name: 'wangwei',
    age: 25
};
let map = new Map(Object.entries(user));
console.log(map);
// Map { 'name' => 'wangwei', 'age' => 25 }
```

#### Map ===> JSON

如果map里面的key名都是字符串，可以选择直接转为 json 对象

```javascript
const map = new Map();
map.set("a", 1);
map.set("b", 2);
map.set("c", 3);
map.set('contra', {description: 'Asynchronous flow control'});
map.set('dragula', {description: 'Drag and drop'});
map.set('woofmark', {description: 'Markdown and WYSIWYG editor'});

const strMapToObj = (map) => {
    let obj = {};
    for(let prop of map){
        obj[prop[0]] = prop[1];
    }
    return obj;
};

function strMapToJson(strMap) {
    return JSON.stringify(strMapToObj(strMap));
}

console.log(strMapToJson(map));
```

另一种情况是，Map 的键名有非字符串，这时可以选择转为数组 JSON。

```javascript
const map = new Map();
map.set("a", 1);
map.set("b", 2);
map.set("c", 3);
map.set('contra', {description: 'Asynchronous flow control'});
map.set('dragula', {description: 'Drag and drop'});
map.set('woofmark', {description: 'Markdown and WYSIWYG editor'});

function mapToArrayJson(map) {
  return JSON.stringify([...map]);
}

mapToArrayJson(map)
// '[[true,7],[{"foo":3},["abc"]]]'
```

#### JSON ===> Map

JSON 转为 Map，正常情况下，所有键名都是字符串。

```javascript
function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes": true, "no": false}')
// Map {'yes' => true, 'no' => false}
```

但是，有一种特殊情况，整个 JSON 就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时，它可以一一对应地转为 Map。这往往是 Map 转为数组 JSON 的逆操作。

 ```javascript
function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
 ```

## WeakMap

`WeakMap` 的用法与 `Map` 大致类似，主要的区别在于：

1. Map可以使用任意类型的数据作为 Key，而 WeakMap 只能使用对象作为 Key。它的键名所引用的对象都是弱引用，即垃圾回收机制不将该引用考虑在内。因此，只要所引用的对象的其他引用都被清除，垃圾回收机制就会释放该对象所占用的内存。也就是说，一旦不再需要，WeakMap 里面的键名对象和所对应的键值对会自动消失，不用手动删除引用。总之，`WeakMap`的专用场合就是，它的键所对应的对象，可能会在将来消失。`WeakMap`结构有助于防止内存泄漏。
2. `WeakMap` 只有这四个方法：`get()`、`set()`、`has()`、`delete()`。
   - 没有遍历操作（即没有`keys()`、`values()`和`entries()`方法），也没有`size`属性。因为没有办法列出所有键名，某个键名是否存在完全不可预测，跟垃圾回收机制是否运行相关。这一刻可以取到键名，下一刻垃圾回收机制突然运行了，这个键名就没了，为了防止出现不确定性，就统一规定不能取到键名。
   - 无法清空，即不支持`clear`方法。

> 更多有关WeakMap的使用介绍请查看：http://es6.ruanyifeng.com/#docs/set-map#WeakMap



#### 内存示例

```shell
// 打开 Node 命令行
$ node --expose-gc

// 手动执行一次垃圾回收，保证获取的内存使用状态准确
> global.gc();
undefined

// 查看内存占用的初始状态，heapUsed 为 5M 左右
> process.memoryUsage();
{ rss: 18923520,
  heapTotal: 7110656,
  heapUsed: 5164056,
  external: 8731 }

> let wm = new WeakMap();
undefined

// 新建一个变量 key，指向一个 5*1024*1024 的数组
> let key = new Array(5 * 1024 * 1024);
undefined

// 设置 WeakMap 实例的键名，也指向 key 数组
// 这时，key 数组实际被引用了两次，
// 变量 key 引用一次，WeakMap 的键名引用了第二次
// 但是，WeakMap 是弱引用，对于引擎来说，引用计数还是1
> wm.set(key, 1);
WeakMap {}

> global.gc();
undefined

// 这时内存占用 heapUsed 增加到 44M 了
> process.memoryUsage();
{ rss: 62652416,
  heapTotal: 50638848,
  heapUsed: 47035976,
  external: 8707 }

// 清除变量 key 对数组的引用，
// 但没有手动清除 WeakMap 实例的键名对数组的引用
> key = null;
null

// 再次执行垃圾回收
> global.gc();
undefined

// 内存占用 heapUsed 变回 5M 左右，
// 可以看到 WeakMap 的键名引用没有阻止 gc 对内存的回收
> process.memoryUsage();
{ rss: 20955136,
  heapTotal: 8683520,
  heapUsed: 5073920,
  external: 8703 }
```



## Set

`Set` 集合与java中的 `Set` 类似，所有的元素都是唯一的，没有重复的值。

### 基本用法

- `add(value)`：添加某个值，返回 Set 结构本身。
- `delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
- `has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
- `clear()`：清除所有成员，没有返回值。

```javascript
let set = new Set([1, 2, 3, 4, 5, 4, 3, 1]);
console.log(set);
// Set { 1, 2, 3, 4, 5 }

set.add(1).add(2);
console.log(set);
// Set { 1, 2, 3, 4, 5 }

set.delete(1);
console.log(set);
// Set { 2, 3, 4, 5 }

console.log(set.has(5));
// true

set.clear();
console.log(set.size);
// 0
```

### 元素唯一性

同 Map  中的 key 一样，也是采用的  [SameValueZero](https://tc39.github.io/ecma262/#sec-samevaluezero) 算法。

### 遍历

- `keys()`：返回键名的遍历器
- `values()`：返回键值的遍历器
- `entries()`：返回键值对的遍历器
- `forEach()`：使用回调函数遍历每个成员

### 与其他数据类型之间的转换

#### set ===> array

```javascript
const items = new Set([1, 2, 3, 4, 5]);
const array = Array.from(items);
```

## WeakSet

`WeakSet` 的特性与前面 `WeakMap` 中存放 Key 的特性类似，这里不多做介绍。



## 参考资料

- http://es6.ruanyifeng.com/#docs/set-map
- https://javascript.info/map-set-weakmap-weakset