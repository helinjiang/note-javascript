原始表达式
===

最简单的表达式是”原始表达式”(primary expression)。原始表达式是表达式的最小单位——它们不再包含其他表达式。JavaScript中的原始表达式包含常量或直接量、关键字和变量。

## 1. 常量（直接量）

直接量是直接在程序中出现的常数值，包括数字直接量、字符串直接量和正则表达式直接量等。

```javascript
1.23 //数字直接量
"hello" //字符串直接量
/pattern/   //正则表达式直接量
```

## 2. 关键字（保留字）

JavaScript中的一些关键字（保留字）构成了原始表达式。

```javascript
true //返回一个布尔值：真
null //返回一个值：空
this //返回”当前“对象
```

## 3. 变量

当JavaScript代码中出现了标识符，JavaScript会将其当做变量而去查找它的值。如果变量名不存在，表达式运算结果为 `undefined` 。然而，在ECMAScript 5的严格模式中，对不存在的变量进行求值会抛出一个引用错误异常。

```javascript
i //返回变量i的值
sum //返回sum的值
undefined //undefined是全局变量，和null不同，它不是一个关键字
```