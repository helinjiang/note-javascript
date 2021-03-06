原始类型之Undefined
===

Undefined类型也用来表示值的空缺，是更深层次的“空值”。

## 1.Undefined类型只有一个值：undefined

`undefined`是预定义的全局变量(它和`null`不一样，它不是关键字)。如果使用`typeof`运算符去获得其类型，则返回“undefined”，表明这个`undefined`值是Undefined类型的唯一成员。

## 2."未初始化"、"未定义"、"无返回"

在以下情况下能够获得`undefined`

*   针对变量：如果变量定义了但没有初始化，则该变量的值为`undefined`。
*   针对对象或数组：如果对象的某属性或者数组的某元素不存在，则查询的结果返回`undefined`
*   针对函数：如果函数没有返回值，则返回`undefined`

## 3.如何区分未初始化变量和未声明变量

通过`typeof`无法判断某个变量是声明了但没初始化，还是压根就没声明过，因为他们`typeof`的结果都是"undefined"。此时需要将其和`undefined`做比较，如果对比时程序报错，则说明该变量从来没被申明过。(对未声明的只能使用`typeof`运算符，否则会引起错误，因为其他运算符(包括==)只能用于已声明的变量上)

```javascript
var a; //定义了变量但未初始化
typeof a //返回"undefined"
typeof b //返回"undefined"，但b压根就没声明过
a == undefined //true
b == undefined //此句报错
```