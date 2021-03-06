转换成String类型
===

## 1. 其他原始值转换成字符串String
一般而言，转换成字符串有以下几种方法：

1.  通过 `String()` 函数
2.  除了 `null` 或 `undefined` 之外的任何值都具有的 `toString()` 方法
3.  数字转字符串时， `Number` 类提供了专门函数和方法
4.  隐式的类型转换(如果“`+`”运算符的一个操作数是字符串，它将会把另外一个操作数转换成字符串)

```javascript
String(false) //"false"
false.toString() //"false"
false + "" //"false"
```

尤其值得一提的是，JavaScript中的 `Number` 类提供了专门的函数和方法用来做更加精确的数字到字符串(number-to-string)的转换。

*   `toString()` 方法：可以接收表示转换基数(radix)的可选参数
*   `toFixed()` 方法：根据小数点后的指定位数将数字转换为字符串
*   `toExponential()` 方法：使用指数记数法将数字转换为指数形式的字符串
*   `toPrecision()` 方法：根据指定的有效数字位数将数字转换成字符串，如果有效数字的位数少于数字整数部分的位数，则转换成指数形式

```javascript
var x = 17;
var string = x.toString(); //"17"，默认是十进制，等效于x.toString(10)
var binary_string = x.toString(2); //"10001"，二进制
var octal_string = "0" + x.toString(8); //"021"，八进制
var hex_string = "0x" + x.toString(16); //"0x11"，十六进制

// 注意以下三种方法都会适当地进行四舍五入或填充0
var n = 123456.789;
n.toFixed(0); //"123457"
n.toFixed(2); //"123456.79"
n.toFixed(5); //"123456.78900"
n.toExponential(1); //"1.2e+5"
n.toExponential(3); //"1.235e+5"
n.toPrecision(4); //"1.235e+5"
n.toPrecision(7); //"123456.8"
n.toPrecision(10); //"123456.7890"
```

## 2. 对象类型转换成字符串String
对象到字符串(object-to-string)的转换是通过调用待转换对象的一个方法（ `toString()` 方法或者 `valueOf()` 方法）来完成的。

### 2.1 toString()方法

默认的 `toString()` 方法只会返回"[object Object]"，大多数时候这并非我们需要的，除非重写这个方法。

*   数组类(Array class)的 `toString()` 方法将每个数组元素转换为字符串，并在元素之间添加逗号合并成结果字符串。结果与调用了array.join(",")结果一致
*   函数类(Function class)的 `toString()` 方法返回这个函数的实现定义的表达式，也就是JavaScript源代码字符串
*   日期类(Date class)的 `toString()` 方法返回了一个可读日期和时间字符串
*   RegExp(RegExp class)的 `toString()` 方法将RegExp对象转换为表示正则表达式直接量的字符串

```javascript
({x:1,y:2}).toString() //"[object Object]"，默认
[1,2,3].toString() //"1,2,3"
(function(x){f(x);}).toString(); //"function(x){f(x);}"
/\d+/g.toString() //"/\\d+/g"
new Date(2015,3,24).toString() //"Fri Apr 24 2015 00:00:00 GMT+0800 (中国标准时间)"
```

### 2.2 valueOf()

默认的 `valueOf()` 方法只是简单的返回对象本身，而不是返回一个原始值(字符串)。

数组、函数和正则表达式简单地继承了这个默认方法，调用这些类型的实例的 `valueOf()` 方法只是简单返回对象本身。日期类定义的 `valueOf()` 方法则会返回它的一个内部表示，即1970年1月1日以来的毫秒数。

```javascript
new Date(2015,3,24).valueOf() //1429804800000
```

### 2.3 对象到字符串的转换步骤

1.  如果对象具有 `toString()` 方法，则调用这个方法。如果它返回一个原始值，JavaScript将这个值转换为字符串（如果本身不是字符串的话），并返回这个字符串结果。
2.  如果对象没有 `toString()` 方法，或者这个方法并不返回一个原始值，那么JavaScript会调用 `valueOf()` 方法。如果存在 `valueOf()` 方法，则调用它，如果返回值是原始值，则再将这个值转换为字符串（如果本身不是字符串的话），并返回这个字符串结果。
3.  否则，JavaScript无法从 `toString()` 或 `valueOf()` 获得一个原始值，此时它将抛出一个类型错误异常。