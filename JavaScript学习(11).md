---
title: JavaScript学习(11) | Date and time
tags:
  - JavaScript
categories: coding
abbrlink: b4757a13
date: 2018-01-11 22:43:00
---

本篇文章来介绍一下JavaScript中的另一个内建对象—— [Date](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date)，其用法与java中的 `Date` 颇为相似。

<!--more-->

## 创建

```javascript
// new Date()
let now = new Date();
console.log(now);

// new Date(milliseconds)
let date1 = new Date(24 * 3600 * 3600);
console.log(date1);

// new Date(datestring)
let date2 = new Date('2017-03-07');
console.log(date2);

// new Date(year, month, date, hours, minutes, seconds, ms)
let date3 = new Date(2017, 3, 7, 0, 0);
console.log(date3);
```



## 查询日期组件

[getFullYear()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/getFullYear)：根据当地时间，返回一个对应于给定日期的年份数字。

[getMonth()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/getMonth)：根据本地时间，返回一个指定的日期对象的月份，为基于0的值（0表示一年中的第一月）。

[getDate()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/getDate)：根据本地时间，返回一个指定的日期对象为一个月中的第几天。

[getHours()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getHours)：根据本地时间，返回一个指定的日期对象的小时。

[getMinutes()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/getMinutes)：根据本地时间，返回一个指定的日期对象的分钟。

[getSeconds()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/getSeconds)：根据本地时间，返回一个指定的日期对象的秒数。

[getMilliseconds()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/getMilliseconds)：根据本地时间，返回一个指定的日期对象的毫秒数。

````javascript
let now = new Date();
console.log(now.getFullYear());
console.log(now.getMonth());
console.log(now.getDay());
console.log(now.getHours());
console.log(now.getMinutes());
console.log(now.getSeconds());
console.log(now.getMilliseconds());
````



## 设置日期组件

- [setFullYear(year [, month, date])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setFullYear)
- [setMonth(month [, date])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setMonth)
- [setDate(date)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setDate)
- [setHours(hour [, min, sec, ms])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setHours)
- [setMinutes(min [, sec, ms])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setMinutes)
- [setSeconds(sec [, ms])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setSeconds)
- [setMilliseconds(ms)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setMilliseconds)
- [setTime(milliseconds)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setTime)



## Date.now()

获取当前时间戳，`Date.now()`  比  `new Date().getTime()`  更快，因为不需要创建对象，所以不需要进行垃圾回收。



## Date.parse 

解析日期字符串，并返回对应的时间戳

```javascript
console.log(Date.parse('2017/03/09'));
// 1488988800000
```



## 日期库

- 推荐非常不错的日期库：http://momentjs.com/



## 参考资料

- https://javascript.info/date
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date

