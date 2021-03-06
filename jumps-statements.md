跳转语句
===

跳转语句（jump statement），可以使JavaScript的执行从一个位置跳转到另一个位置。

## 1. break语句

单独使用`break`语句的作用是立即退出最内层的循环或`switch`语句。

```javascript
//退出循环
var a=[1,2,3,4,5,6]
for(var i=0; i < a.length; i++){
    if(a[i] == 3){
        break;
    }
    console.log(i + ":" + a[i]);
}

//退出switch
var x = 2;
switch(x){
    case 1:
        console.log("x is 1");
        break;
    case 2:
        console.log("x is 2");
        break;
    default:
        console.log("x is other:" + x);
        break;
}
```

## 2. continue语句

`continue`语句和`break`语句非常类似，但它不是退出循环，而是转而执行下一个循环。

在不同类型的循环中，`continue`的行为也有所区别：

*   在`while`循环中，在循环开始处指定的`expression`会重复检测，如果检测结果为`true`，循环体会从头开始执行。
*   在`do/while`循环中，程序的执行直接跳转到循环结尾处，这时会重新判断循环条件，之后才会继续下一次循环。
*   在`for`循环中，首先计算自增表达式，然后再次检测`test`表达式，用以判断是否执行循环体。
*   在`for/in`循环中，循环开始遍历下一个属性名，这个属性名赋给了指定的变量。

```javascript
//计算数组a中所有元素的和，结果为8，注意数组中有可能有undefined元素。
var a = [1,,3,4], total=0;
for(i=0;i<a.length;i++){
    if(!a[i]){
        continue;//如果不符合要求则继续下一次循环
    }
    total += a[i];
}
```

## 3. return语句

`return`语句只能在函数体内出现。当执行到`return`语句时，函数即终止执行，并返回函数调用后的值给调用程序。

如果函数没有`return`语句，则调用表达式的结果是`undefined`;存在`return`语句，但单独使用，返回结果也是`undefined`。

```javascript
function square(x){
    return x*x; //一个包含return语句的函数
} 
var result = square(2); //调用结果为4

function display(obj){
    if(!obj){
        return; //单独使用，如果参数是null或undefined则立即返回
    }

    //其他逻辑
}
```

## 4. throw语句

使用`throw`语句可以显式抛出异常。

```javascript
throw expression;
```

`expression`的值可以是任意类型。一般我们也可以使用`Error`类型和其子类型。

当抛出异常时，JavaScript解释器会立即停止当前正在执行的逻辑，并跳转至最近的异常处理程序。异常会向上传播到调用该函数的代码，直至遇到处理它的`try/catch/finally`语句。

## 5. try/catch/finally语句

`try/catch/finally`语句是JavaScript的异常处理机制。

所谓异常（exception）是当发生了某种异常情况或错误时产生的一个信号。抛出异常，就是用信号通知发生了错误或异常状况。捕获异常是指处理这个信号，即采取必要的手段从异常中恢复。在JavaScript中，当产生运行时错误或者程序使用`throw`语句时就会显式地抛出异常。使用`try/catch/finally`语句可以捕获异常。

```javascript
try{
    //通常来讲，这里的代码会从头执行到尾而不会产生任何问题，
    //但有时会抛出一个异常，要么是由throw语句直接抛出异常，
    //要么是通过调用一个方法间接抛出异常
}catch(e){
    //当且仅当try语句块跑出了异常，才会执行这里的代码
    //这里可以通过局部变量e来获得对Error对象或者抛出的其他值的引用
    //这里的代码块可以基于某种原因处理这个异常，也可以忽略这个异常，
    //还可以通过throw语句重新抛出异常
}finally{
    //不管try语句块是否抛出了异常，这里的逻辑总是会执行，终止try语句块的方式有：
    // 1) 正常终止，执行完语句块的最后一条语句
    // 2) 通过break、continue或return语句终止
    // 3) 抛出一个异常，异常被catche从句捕获
    // 4) 抛出一个异常，异常未被捕获，继续向上传播
}
```

更多内容请看《[第10章 错误处理机制](http://helinjiang.com/note/javascript/error.html)》