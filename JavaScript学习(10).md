本篇介绍一下JavaScript中有关JSON的用法。

## JSON.stringify

#### 基本用法

```javascript
let value = JSON.stringify(value[, replacer [, space]]);
```

> `value`：将要序列化成 一个JSON 字符串的值。
>
> `replacer` 可选：如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为null或者未提供，则对象所有的属性都会被序列化；关于该参数更详细的解释和示例，请参考[使用原生的 JSON 对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_native_JSON#The_replacer_parameter)一文。
>
> `space` 可选：指定缩进用的空白字符串，用于美化输出（pretty-print）；如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格；如果该参数为字符串(字符串的前十个字母)，该字符串将被作为空格；如果该参数没有提供（或者为null）将没有空格。 

例1：

```javascript
let student = {
    name: 'John',
    age: 30,
    isAdmin: false,
    courses: ['html', 'css', 'js'],
    wife: null
};

let json = JSON.stringify(student);

console.log(typeof json); // string!

console.log(json); // {"name":"John","age":30,"isAdmin":false,"courses":["html","css","js"],"wife":null}
```

例2：

```javascript
let foo = {foundation: "Mozilla", model: "box", week: 45, transport: "car", month: 7};

let replacer = function (key, value) {
    if (typeof value === "string") {
        return undefined;
    }
    return value;
};

console.log(JSON.stringify(foo, replacer)); 
// {"week":45,"month":7}

console.log(JSON.stringify(foo, ['foundation', 'transport'])); 
// {"foundation":"Mozilla","transport":"car"}
```



#### 自定义toJSON

在对象中自定义一个`toJSON`函数，类似于java中的重写。

```javascript
let room = {
    number: 23
};

let meetup = {
    title: "Conference",
    date: new Date(Date.UTC(2017, 0, 1)),
    room
};

console.log(JSON.stringify(meetup));
// {"title":"Conference","date":"2017-01-01T00:00:00.000Z","room":{"number":23}}
```

改写 `room` 序列话之后的结果，自定义一个 `toJSON` 函数

```javascript
let room = {
    number: 23,
    toJSON() {
        return this.number;
    }
};

let meetup = {
    title: "Conference",
    date: new Date(Date.UTC(2017, 0, 1)),
    room
};

console.log(JSON.stringify(meetup));
// {"title":"Conference","date":"2017-01-01T00:00:00.000Z","room":23}
```



## JSON.parse

#### 基本用法

```javascript
let value = JSON.parse(str[, reviver]);
```

> - `str`：要转化的字符串
> - `revier`：转化函数

例1：

```javascript
let user = '{ "name": "John", "age": 35, "isAdmin": false, "friends": [0,1,2,3] }';

console.log(JSON.parse(user));
// { name: 'John', age: 35, isAdmin: false, friends: [ 0, 1, 2, 3 ] }
```

例2：

```javascript
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str);

console.log( meetup.date.getDate() ); 
// Error! meetup.date.getDate is not a function
```

`meetup.date` 是字符串，不是object，需要我们手动转化一下：

```javascript
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str, function (key, value) {
    if (key === 'date') return new Date(value);
    return value;
});

console.log(meetup.date.getDate()); // works
// 30
```

对内嵌对象也适用：

```javascript
let schedule = `{
  "meetups": [
    {"title":"Conference","date":"2017-11-30T12:00:00.000Z"},
    {"title":"Birthday","date":"2017-04-18T12:00:00.000Z"}
  ]
}`;

schedule = JSON.parse(schedule, function (key, value) {
    if (key === 'date') return new Date(value);
    return value;
});

console.log(schedule.meetups[1].date.getDate()); // works!
// 18
```



## 参考资料

- https://javascript.info/json
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/