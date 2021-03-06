关系表达式
===

关系运算符用于测试两个值之间的关系（比如“相等”,“小于”，或“是…的属性”)，根据关系是否存在而返同`true`或`false`。关系表达式总是返回一个布尔值，通常在`if`、`while`或者`for`语句中使用关系表达式，用以控制程序的执行流程。

## 1. 相等和不等运算符

#### 1.1 含义

”`==`“和”`===`“运算符用于比较两个值是否相等。两个运算符允许任意类型的操作数，如果操作数相等则返回`true`，否则返回`false`

*   ”`==`“运算符称为相等运算符（equality operator），用来检测两个操作数是否相等，这里”相等“的定义非常宽松，可以允许进行类型转换。
*   ”`===`“运算符称为严格相等运算符（strict equality），有时也称做恒等运算符（identity operator），用来检测两个操作数是否严格相等。

”`!=`“和”`!==`“运算符的检测规则分别是”`==`“和”`===`“运算符的求反。

#### 1.2 ”===“的比较

严格相等运算符”`===`“首先计算其操作数的值，然后比较这连个值，比较过程没有任何类型转换。

*   如果两个值类型不相同，则它们不相等。
*   如果两个值都是`null`或者都是`undefined`，则它们不相等。
*   如果两个值都是布尔值`true`或都是布尔值`false`，则它们相等。
*   如果其中一个值是`NaN`，或者两个值都是`NaN`，则它们不相等。`NaN`和其他任何值都是不相等的，包括它本身！
*   如果两个值为数字且数值相等，则它们相等。特殊情况：`0===-0`。
*   如果两个值为字符串，且包含的对应位上的16位数完全相等，则它们相等。如果它们的长度或内容不同，则它们不等。
*   如果两个引用值指向同一个对象、数组或函数，则它们是相等的。如果指向不同的对象，则它们是不等的，尽管两个对象可能具有完全一样的属性。

#### 1.3 ”==“的比较

相等运算符”`==`“和恒等运算符相似，但相等运算符的比较并不严格。如果两个操作数不是同一类型，那么相等运算符会尝试进行一些类型转换，然后进行比较。

*   如果两个操作数的类型相同，则和《[4.8.1.2 ”===“的比较](http://helinjiang.com/note/javascript/expression.html#h_equal_equal_equal)》所述的严格相等的比较规则一样。如果严格相等，那么比较结果为相等；如果它们不严格相等，则比较结果为不相等。
*   如果两个操作数类型不同，”`==`“相等操作符也可能会认为它们相等。检测相等将会遵守如下规则和类型转换：
    *   如果一个值是`null`，另一个是`undefined`，则它们相等。
    *   如果一个值是数字，另一个是字符串，则先将字符串转换位数字，然后使用转换之后的值进行比较。
    *   如果其中一个值是`true`，则将其转换为1再进行比较。如果其中一个值是`false`，则将其转换为0再进行比较。
    *   如果一个值是对象，另一个值是数字或字符串，则使用《4.4 对象转换为原始值》中提到的转换规则将对象转换为原始值，然后再进行比较。
    *   其他不同类型之间的比较均不相等。

举例说明，`"1"==true`：布尔值`true`首先转换为数字1，字符串"1"也转换为了数字1，因为两个数字的值相等，因此其比较结果为`true`。

#### 1.4 对象和数组的比较

在《[2.3.4 对象的比较是引用的比较](http://helinjiang.com/note/javascript/type-and-value.html#h_object_compare)》中我们提到，JavaScript对象的比较是引用的比较，不是值的比较。

对象和其本身是相等的，但和其他任何对象都不相等。如果两个不同的对象具有相同数量的属性、相同的属性名和值，它们依然是不相等的。相同位置的数组元素是相等的两个数组也是不相等的。

## 2. 比较运算符

比较运算符用来检测两个操作数的大小关系（数值大小或者字母表的顺序），包括小于（`<`）、大于（`>`）、小于等于（`<=`）、大于等于（`>=`）

比较操作符的操作数可能是任意类型，然后只有数字和字符串才能真正执行比较操作，因此那些不是数字和字符串的操作数都将进行类型转换，类型转换规则如下。

*   如果操作数是对象，那么这个对象将按照《[2.4.5 对象转换为原始值](http://helinjiang.com/note/javascript/type-and-value.html#h_object_to_primitive)》提到的转换规则转换为原始值。
*   在对象转换为原始值之后，如果两个操作数都是字符串，那么将按照字母表的顺序对两个字符串进行比较。
*   在对象转换为原始值之后，如果至少有一个操作数不是字符串，那么两个操作数都将转换为数字进行数值比较。
    *   `0`和`-0`是相等的。
    *   `Infinity`比其他任何数字都大（除了`Infinity`本身）。
    *   `-Infinity`比其他任何数字都小（除了`-Infinity`本身）。
    *   如果其中一个操作数是（或转换后是）`NaN`，那么比较操作符总是返回`false`。

注意，字符串比较是区分大小写的，所有大写的ASCII字母都”小于“小写的ASCII字母，比如"Zoo"<"aardvark"结果为true。同时也可以使用`String.localCompare()`方法，会更加健壮可靠。必要时，也可以通过`String.toLowerCase()`和`String.toUpperCase()`做大小写转换后再比较。

## 3. in运算符

`in`运算符希望它的左操作数是一个字符串或可以转换为字符串，希望它的右操作数是一个对象。如果右侧的对象拥有一个名为左操作数值的属性名，那么表达式返回`true`。

```javascript
var point = {x:1, y:1}; //定义一个对象
"x" in point //true，对象有一个名为"x"的属性
"z" in point //false，对象中不存在名为"z"的属性
"toString" in point //true，对象继承了toString()方法

var data=[7,8,9]; //拥有三个元素的数组
"0" in data //true，data["0"]存在，因此为true
1 in data //true，data[1]存在，因此为true
3 in data //false，data[3]不存在，因此为false
```

## 4. instanceof 运算符

`instanceof`运算符希望它的左操作数是一个对象，右操作数标识对象的类。如果左侧的对象是右侧类的实例，则表达式返回`true`，否则返回`false`。

```javascript
var d=new Date(); //通过Date()构造函数来创建一个新对象
d instanceof Date; //true，d是由Date()创建的
d instanceof Object; //true，所有的对象都是Object的实例
d instanceof Number; //false，d不是Number对象

var a=[1,2,3]; //通过数组直接量的写法创建一个数组
a instanceof Array; //true，a是一个数组
a instanceof Object; //true，所有数组都是对象
a instanceof RegExp; //false，数组不是正则表达式
```

如果`instanceof`的左操作数不是对象的话，`instanceof`返回`false`;如果右操作数不是函数（在后续会讲到，JavaScript中对象的类是通过初始化它们的构造函数来定义的，如此说来，`instanceof`的右操作数应当是一个函数），则抛出一个类型错误异常。