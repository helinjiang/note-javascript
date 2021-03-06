其他语句类型
===

本节讨论剩下的三种JavaScript语句——`with`、`debugger`和`"use strict"`。

## 1. with语句

`with`语句用于临时扩展作用域链。

```javascript
with (object)
    statement
```

这条语句将`object`添加到作用域链的头部，然后执行`statement`，最后把作用域链恢复到原始状态。

在严格模式中是禁止使用`with`语句的，使用`with`语句的JavaScript代码非常难于优化，且运行更慢，不推荐使用。

## 2. debugger语句

`debugger`语句通常什么也不做。然而，当调试程序可用并运行的时候，JavaScript解释器将会（非必需）以调式模式运行。实际上，这条语句用来产生一个断点（breakpoint)，JavaScript代码的执行会停止在断点的位置，这时可以使用调试器输出变址的值、检查调用栈等。

在ECMAScript 5中，`debugger`语句正式加入到这门语言里，但主流浏览器厂商（chorme等）已经将其实现。

注意`debugger`语句不会启动调试器，只有调试器已经在运行中，这条语句才会真正产生一个断点。

## 3. "use strict"

`"use strict"`是ECMAScript 5引入的一条指令，它不是语句，但非常接近于语句。使用它的目的是说明（脚本或函数中）后续的代码将会解析为严格代码（strict code），此时会以严格模式执行。

ECMAScript 5中的严格模式是该语言的一个受限制的自己，它修正了语言的重要缺陷，并提供健壮的差错功能和增强的安全机制。具体详见XXX