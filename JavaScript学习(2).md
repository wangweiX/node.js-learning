JavaScript中的运算符与其他语言中的一样，学起来难度不大。

## 算术运算符

| 运算符 | 描述 |
| ------ | ---- |
| +      | 加   |
| -      | 减   |
| *      | 乘   |
| /      | 除   |
| %      | 取模 |
| ++     | 加1  |
| --     | 减1  |



## 赋值运算符

| 运算符 | 例子   | 等同于    |
| ------ | ------ | --------- |
| =      | x = y  | x = y     |
| +=     | x += y | x = x + y |
| -=     | x -= y | x = x - y |
| *=     | x *= y | x = x * y |
| /=     | x /= y | x = x / y |
| %=     | x %= y | x = x % y |



## 比较操作符

| 运算符 | 描述                              |
| ------ | --------------------------------- |
| ==     | equal to                          |
| ===    | equal value and equal type        |
| !=     | not equal                         |
| !==    | not equal value or not equal type |
| >      | greater than                      |
| <      | less than                         |
| >=     | greater than or equal to          |
| <=     | less than or equal to             |
| ?      | ternary operator                  |



## 条件运算符

```javascript
let variable = boolean_expression ? true_value : false_value;
```



## 逻辑运算符

| 运算符 | 描述   |
| ------ | ------ |
| &&     | 逻辑与 |
| \|\|   | 逻辑或 |
| !      | 逻辑非 |



## 类型操作

| 运算符     | 描述                       |
| ---------- | -------------------------- |
| typeof     | 返回变量类型               |
| instanceof | 判断object是否为某一个类型 |



## 位运算符

| 运算符                                                       | 用法      | 描述                                                         |
| ------------------------------------------------------------ | --------- | ------------------------------------------------------------ |
| [按位与（ AND）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_AND) | `a & b`   | 对于每一个比特位，只有两个操作数相应的比特位都是1时，结果才为1，否则为0。 |
| [按位或（OR）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_OR) | `a | b`   | 对于每一个比特位，当两个操作数相应的比特位至少有一个1时，结果为1，否则为0。 |
| [按位异或（XOR）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_XOR) | `a ^ b`   | 对于每一个比特位，当两个操作数相应的比特位有且只有一个1时，结果为1，否则为0。 |
| [按位非（NOT）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_NOT) | `~ a`     | 反转操作数的比特位，即0变成1，1变成0。                       |
| [左移（L](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Left_shift)[eft shift）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Left_shift) | `a << b`  | 将 `a` 的二进制形式向左移 `b` (< 32) 比特位，右边用0填充。   |
| [有符号右移](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Right_shift) | `a >> b`  | 将 a 的二进制表示向右移` b `(< 32) 位，丢弃被移出的位。      |
| [无符号右移](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Unsigned_right_shift) | `a >>> b` | 将 a 的二进制表示向右移` b `(< 32) 位，丢弃被移出的位，并使用 0 在左侧填充。 |



## == 与 === 区别

> 在javascript中比较时，建议使用 `===` 与 `!==` 。

### === 比较

强相等比较，意味着我们所比较的数值和类型必须相同。我们来看几个例子。

```javascript
5 === 5
// true

'hello world' === 'hello world'
// true (Both Strings, equal values)

true === true
// true (Both Booleans, equal values)

77 === '77'
// false (Number v. String)

'cat' === 'dog'
// false (Both are Strings, but have different values)

false === 0
// false (Different type and different value)
```



### == 比较

弱相等比较，同时它也会执行类型强制比较。类型强制意味着只有在尝试将它们转换为公共类型后才会比较两个值。例如：

```javascript
77 == '77'
// true

false == 0
// true
```



### Falsy Values

在javascript中你应该注意6个虚假值：

- `false` — boolean false
- `0` — number zero
- `""` — empty string
- `null`
- `undefined`
- `NaN` — Not A Number



### Falsy Value Comparison

1. `false`, `""` and `0`

   ```javascript
   false == 0
   // true
   
   0 == ""
   // true
   
   "" == false
   // true
   ```

   

2. `null` and `undefined`

   ```javascript
   null == null
   // true
   
   undefined == undefined
   // true
   
   null == undefined
   // true
   
   null == false
   // false
   ```

   

3. `NaN`

   `NaN` 不等于任何值，甚至不等于它自己。

   ```javascript
   NaN == null
   // false
   
   NaN == undefined
   // false
   
   NaN == NaN
   // false
   ```

   

## 参考资料

- https://www.w3schools.com/jS/js_operators.asp
- https://codeburst.io/javascript-double-equals-vs-triple-equals-61d4ce5a121a
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators