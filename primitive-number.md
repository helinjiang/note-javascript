原始类型之Number
===

和其他编程语言(例如C和Java)不同，JavaScript不区分整数值和浮点数值，所有的数字均用浮点数值表示。

*   浮点数范围：+-5*10^(-324) ~ +-1.8*10^308，采用IEEE754标准定义的64位浮点格式表示数字。
*   整数范围：-2^53 ~ 2^53，如果超过了此范围，则无法保证低位数字的精度。然而需要注意的是，JavaScript中实际的操作（比如数组索引和位操作符等）则是基于32位整数。

在Number对象中，用`Number.MAX_VALUE`表示最大值，用`Number.MIN_VALUE`表示最小值。

当一个数字直接出现在JavaScript中，我们称之为数字直接量(numeric literal)。JavaScript支持多种格式的数字直接量。

## 1.整型直接量

JavaScript能够识别十进制整数和十六进制值。

```javascript
0 //十进制整数
100000 //十进制整数
0xff //十六进制，转换为十进制值为15*16+15=255
```

在ECMAScript 6的严格模式下，八进制直接量是明令禁止的，但JavaScript中的某些实现可以允许采用八进制形式表示整数（例如：0377，转换成十进制就是3*64+7*8+7=255）。由于无法得知当前JavaScript的实现是否支持八进制的解析，因此最好不要使用以0为前缀的整型直接量。

【各种进制的相互转换】

## 2.浮点型直接量

浮点型直接量可以含有小数点，它们采用的是传统的实数写法，即由整数部分、小数点和小数部分组成。

此外，还可以使用指数记数法表示浮点型直接量，即`[digits][.digits][(E|e)[(+|-)]digits]`

```javascript
3.14
2345.6789
.3333
6.02e23 //6.02*10^23
1.47E-32 //1.47*10^(-32)
```

## 3.算术运算

基本运算符：包括加法运算符(+)、减法运算符(-)、乘法运算符(*)、除法运算符(/)、求余运算符(%)等，具体请看《xx》一节内容，那里会有详细介绍。

更复杂的算术运算：通过作为`Math`对象的属性定义的函数和常量来实现，具体请看《xx》一节内容，那里列出了JavaScript所支持的所有属性函数。

## 4.Infinity、-Infinity和isFinite()

JavaScript中的算术运算在溢出(overflow)、下溢(underflow)或被零整除时不会报错，而是会返回无穷大值`Infinity`或负无穷大值`-Infinity`，并且基于它们的加、减、乘、除等运算结果还是无穷大值（当然还保留它们的正负号）

特殊情况：零除以零是没有意义的，整除的结果是一个非数字值`NaN`。

Number对象中，`Number.POSITIVE_INFINITY`表示无穷大，`Number.NEGATIVE_INFINITY`表示负无穷大。而检查数值是否是无穷大则使用`isFinite(number)`函数。如果 `number` 是有限数字（或可转换为有限数字），那么返回 true。否则，如果` number` 是 `NaN`（非数字），或者是正、负无穷大的数，则返回 false。

```javascript
Number.POSITIVE_INFINITY===Infinity //true，无穷大
Number.NEGATIVE_INFINITY===-Infinity //true，负无穷大

isFinite(123); //true
isFinite(-1.23); //true
isFinite(5-2); //true
isFinite(0) //true;
isFinite("hello"); //false
isFinite(Infinity); //false
```

## 5.非数字值NaN和isNaN()

非数字值(not-a-number)用`NaN`表示。以下情况都返回`NaN`：

*   零除以零
*   无穷大除以无穷大
*   给任意负数开平方根
*   非数字或无法转换成数字的操作数与算术运算符一起使用

Number对象中，`Number.NaN`表示非数字值。 `NaN`有一点很特殊，它和任何值都不相等，包括自身。如果要判断某个值是否为非数字值`NaN`，则可以使用`isNaN()`来判断。

```javascript
var x="hello";
x==NaN; //false，按理说x的确为非数字值，但NaN和任何值都不相等
x!=NaN; //true, NaN和任何值都不相等，包括自身
NaN==NaN; //false, NaN和任何值都不相等，包括自身
NaN!=NaN; //true, NaN和任何值都不相等，包括自身
isNaN(x); //true，推荐用此方法来判断是否为非数字值NaN
isNaN(NaN); //true
isNaN(6); //false
isNaN("6"); //false
isNaN("6.2"); //false
isNaN("6a"); //true
isNaN({a:1}); //true
```

注意：`isNaN()`方法的参数不一定是数字值才返回false，只要该参数可以被转换成数字值，则该方法都返回false。例如：`isNaN(6)`和`isNaN("6")`都是false，即虽然"6"为字符串，但由于JavaScript是弱类型语言，而"6"是可以转换成数字值的，因此`isNaN("6")`是false

【x!=x，当x为NaN时，以此判断该x值。isNaN的判断依据】

## 6.负零值

当一个负数发送下溢(underflow，它是当运算结果无限接近于零但比JavaScript能表示的最小数还小时发生的一种情形)时，JavaScript返回一个特殊的值“负零”。JavaScript程序员很少用到负零。

负零和正零值是相等的，唯一区别在于作为除数时有差别。

```javascript
vr zero=0; //正常的零值
var negz=-0; //负零值
zero === negz; //true,负零和正零值是相等的
1/zero === 1/negz; //false,正无穷大和负无穷大不等
```

## 7.二进制浮点数和四舍五入错误

JavaScript使用的实数，常常只是真实数的一个近似表示。

JavaScript使用二进制表示法（IEEE-754浮点数表示法，几乎所有现代编程语言所采用），可以精确表示分数，比如1/2、1/8、1/1024，但并不能精确表示类似0.1这样简单的数字。

```javascript
var x = 0.3 - 0.2;
var y = 0.2 - 0.1;
x == y //false,两值不相等！
x == 0.1 //false，0.3-0.2=0.09999999999999998
y == 0.1
```

注意，在任何使用二进制浮点数的编程语言中都会出现上述问题，但四舍五入之后，计算结果还是可以胜任大多数的计算任务，只是尽量不要比较两个实数值（主要是指非整数）是否相等，这种相等比较并不可靠。另外一种解决办法是适当避免小数，使用整数。比如金融计算时，要将金额转换成“分”，而不要使用带小数的“元”进行基于货币单位的运算。

## 8.日期和时间

JavaScript语言核心包括Date()构造函数，用来创建表示日期和时间的兑现。这些日期对象的方法为日期计算提供了简单API，它不像数字那样是基本数据类型。【具体查看xxx】

```javascript
var then = new Dat(2011, 0, 1); //2011年1月1日
var later = new Date(2011, 0, 1, 17, 10, 30); //2011年1月1日，当地时间5:10:30pm
var now = new Date(); //当前日期和时间
var elapsed = now - then; //日期减法，计算时间间隔的毫秒数
later.getFullYear() //2011，年份
later.getMonth() //0，月份是从0开始计数
later.getDate() //1，天数是从1开始计数
later.getDay() //5，星期几，0代表星期日，5代表星期五
later.getHours() //17，小时，当地时间
```