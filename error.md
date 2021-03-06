JavaScript 错误处理机制
===

本章将对JavaScript中的错误处理机制进行讲解。

## 1. Error对象

一旦代码解析或运行时发生错误，JavaScript引擎就会自动产生并抛出一个`Error`对象的实例，然后整个程序就中断在发生错误的地方。`Error`对象的实例有三个最基本的属性：

*   `name`：错误名称
*   `message`：错误提示信息
*   `stack`：错误的堆栈（非标准属性，但是大多数平台支持）

```javascript
function throwError() {
  throw new Error('Hello,Error!');
}

function catchErrorTest() {
  try {
    throwError();
  } catch(e) {
    console.log(e.name + ":" + e.message);

    //尝试打印该错误的堆栈
    console.log(e.stack); 
  }
}

catchErrorTest(); //开始测试
```

## 2. JavaScript的原生错误类型

`Error`对象是最一般的错误类型，在它的基础上，JavaScript还定义了其他6种错误，也就是说，存在`Error`的6个派生对象。

### 2.1 SyntaxError

`SyntaxError`是解析代码时发生的语法错误。

```javascript
// 变量名错误
var 1a; //SyntaxError: Unexpected token ILLEGAL

// 缺少括号
console.log 'hello'); //SyntaxError: Unexpected string
```

### 2.2 ReferenceError

`ReferenceError`是引用一个不存在的变量时发生的错误。

```javascript
unknownVariable
// ReferenceError: unknownVariable is not defined
```

另一种触发场景是，将一个值分配给无法分配的对象，比如对函数的运行结果或者`this`赋值。

```javascript
console.log() = 1
// ReferenceError: Invalid left-hand side in assignment

this = 1
// ReferenceError: Invalid left-hand side in assignment
```

### 2.3 RangeError

`RangeError`是当一个值超出有效范围时发生的错误。主要有以下几种情况：

*   数组长度为负数
*   `Number`对象的方法参数超出范围
*   函数堆栈超过最大值

```javascript
new Array(-1)
// RangeError: Invalid array length

(1234).toExponential(21)
// RangeError: toExponential() argument must be between 0 and 20
```

### 2.4 TypeError

`TypeError`是变量或参数不是预期类型时发生的错误。比如，对字符串、布尔值、数值等原始类型的值使用`new`命令，就会抛出这种错误，因为`new`命令的参数应该是一个构造函数。调用对象不存在的方法时，也会抛出`TypeError`错误。

```javascript
new 123
//TypeError: number is not a function

var obj = {};
obj.unknownMethod()
// TypeError: undefined is not a function
```

### 2.5 URIError

`URIError`是URI相关函数的参数不正确时抛出的错误，主要涉及`encodeURI()`、`decodeURI()`、`encodeURIComponent()`、`decodeURIComponent()`、`escape()`和`unescape()`这六个函数。

```javascript
decodeURI('%2')  // URIError: URI malformed
```

### 2.6 EvalError

`eval`函数没有被正确执行时，会抛出`EvalError`错误。该错误类型已经不再在ES5中出现了，只是为了保证与以前代码兼容，才继续保留。

### 2.7 总结

以上这6种派生错误，连同原始的`Error`对象，都是构造函数。开发者可以使用它们，自定义生成错误对象的实例。

```javascript
new Error("出错了！");
new RangeError("出错了，变量超出有效范围！");
new TypeError("出错了，变量类型无效！");
```

上面代码表示新建错误对象的实例，实质就是手动抛出错误。可以看到，错误对象的构造函数接受一个参数，代表错误提示信息（message），`catch`住时，可以通过`Error.message`获得该错误提示。

## 3. 自定义错误

除了JavaScript内建的7种错误对象（`Error`对象和`Error`的六个派生对象），还可以定义自己的错误对象。

```javascript
 //自定义一个错误对象UserError 
function UserError(message) {
   this.message = message || "默认信息";
   this.name = "UserError";
}

//并让它继承Error对象
UserError.prototype = new Error();
UserError.prototype.constructor = UserError;

//生成这种自定义的错误
new UserError("这是自定义的错误！");
```

## 4. throw 语句

`throw`语句的作用是中断程序执行，抛出一个意外或错误。它接受一个表达式作为参数。

```javascript
throw "Error！"; 
throw 42;
throw true;
throw {toString: function() { return "Error!"; } };
```

上面代码表示，`throw`可以接受各种值作为参数。JavaScript引擎一旦遇到`throw`语句，就会停止执行后面的语句，并将`throw`语句的参数值，返回给用户。

最好的做法是使用`throw`语句手动抛出一个`Error`对象或者是`Error`的派生对象，甚至是自定义错误对象。

```javascript
throw new Error('出错了!'); 
throw new TypeError("出错了，变量类型无效！");
throw new UserError("这是自定义的错误！"); //该自定义错误对象在上面的例子中有定义
```

## 5. try...catch结构

为了对错误进行处理，需要使用`try...catch`结构。

`try`代码块用来运行某段可能出错的代码，一旦出错（包括用`throw`语句抛出错误），就被`catch`代码块捕获。`catch`接受一个参数，表示`try`代码块传入的错误对象。

```javascript
try {
    throw new Error('出错了!');
} catch (e) {
    console.log(e.name + ": " + e.message);  // Error: 出错了！
    console.log(e.stack);  // 不是标准属性，但是浏览器支持
}
```

`catch`代码块之中，还可以再抛出错误，甚至使用嵌套的`try...catch`结构。

```javascript
try {
   throw n; // 这里抛出一个整数
} catch (e) {
   if (e <= 50) {
      // 针对1-50的错误的处理
   } else {
      // 大于50的错误无法处理，再抛出一个错误
      throw e;
   }
}
```

为了捕捉不同类型的错误，`catch`代码块之中可以加入判断语句。

```javascript
try {
  foo.bar();
} catch (e) {
  if (e instanceof EvalError) {
    console.log(e.name + ": " + e.message);
  } else if (e instanceof RangeError) {
    console.log(e.name + ": " + e.message);
  }
  // ... 
}
```

`try...catch`结构是JavaScript语言受到Java语言影响的一个明显的例子。这种结构多多少少是对结构化编程原则一种破坏，处理不当就会变成类似`goto`语句的效果，应该谨慎使用。

## 6. finally代码块

`try...catch`结构允许在最后添加一个`finally`代码块，表示不管是否出现错误，都必需在最后运行的语句。

什么时候需要有这种场景？一个经典用法是写文件操作，不管写入是否出错，最后一定要关闭这个文件字节流，否则会造成内存泄漏。下面的伪代码说明了这个用法：

```javascript
openFile();
try {
   writeFile(Data);
} catch(e) {
    handleError(e);
} finally {
   closeFile();
}
```

下面的这个例子充分反应了`try...catch...finally`这三者之间的执行顺序。

```javascript
function f() {
    try {
        console.log(0);
        throw "bug";
    } catch(e) {
        console.log(1);
        return true; // 这句会延迟到finally代码块结束再执行
        console.log(2); // 不会运行
    } finally {
        console.log(3);
        return false; // 这句会覆盖掉前面那句return
        console.log(4); // 不会运行
    }

    console.log(5); // 不会运行
}

var result = f(); 
// 0
// 1
// 3

result   // false
```

## 参考资料
Jani Hartikainen, [JavaScript Errors and How to Fix Them](http://davidwalsh.name/fix-javascript-errors)
