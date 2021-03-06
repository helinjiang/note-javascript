全局对象
===

全局对象(global object)在JavaScript程序中可以直接使用。

## 1. 全局对象初始属性

当JavaScript解释器启动时(或者任何Web浏览器加载新页面的时候)，它将创建一个新的全局对象，并给它一组定义的初始属性：

*   全局属性，比如 `undefined` 、 `Infinity` 和 `NaN` 等
*   全局函数，比如 `isNaN()` 、 `parseInt()` 和 `eval()` 等
*   构造函数，比如 `Date()` 、 `RegExp()` 、 `String()` 、 `Object()` 和 `Array()` 等
*   全局对象，比如 `Math` 和 `JSON` 等

全局对象的初始属性并不是保留字，但它们应该当作保留字来对待。因此自定义变量或者方法时，避免使用它们作为变量或方法名。

在代码最顶级——不在任何函数或闭包内——可以使用JavaScript关键字 `this` 来引用全局对象。

```javascript
var global = this; //定义一个引用全局对象的全局变量
```

## 2. 客户端JavaScript中的全局对象

在客户端JavaScript中，Window对象定义了一些额外的全局属性，并且充当了全局对象。这个全局Window对象有一个属性 `window` 引用其自身，它可以替代 `this` 来引用全局对象。

Window对象定义了核心全局属性，但它也针对Web浏览器和客户端JavaScript定义了一少部分其他全局属性。详细请看xxx

## 3. 作用域

全局对象可以在JavaScript中的任何地方直接使用，包括在函数内部等。

当初次创建时，全局对象定义了JavaScript中所有的预定义全局值(详见《全局对象初始属性》，如果是客户端JavaScript，则还有其他全局属性)。如果代码中声明了一个全局变量，则这个全局变量就是全局对象的一个属性，《变量作用域》对此有详尽的解释。