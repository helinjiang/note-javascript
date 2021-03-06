声明语句
===

`var`和`function`都是声明语句，它们声明或定义变量或函数。声明语句本身什么也不做，但它有一个重要的意义，就是通过创建变量和函数，可以更好地组织代码的语义。

## 1. var

`var`语句用来声明一个或多个变量，它的语法如下：

```javascript
var name_1 [=value_1][,..., name_n[=value_n]]   
```

关键字`var`之后跟随的是要声明的变量列表，列表中的每个变量都可以带有初始化表达式，用于指定它的初始值。

```javascript
var i; //一个简单的变量
var j=0; //一个带有初始值的变量
var p,q; //两个变量
var greeeting="hello" + j; //更复杂的初始化表达式
var x = 2.34, y=Math.cos(0.75), r, theta; //很多变量
var x=2, y=x*x; //第二个变量使用了第一个变量

//更多变量，并且每个变量都独占一行
var x=2, 
    f = function(x){return x*x},
    y = f(x);
```

关于 `var`语句的更多细节，我们在《[3.1 变量声明](http://helinjiang.com/note/javascript/variable.html#h_variable_declaration)》一章已经说得比较清楚，此处对部分重点再做一个说明：

*   如果`var`语句出现在函数体内，那么它定义的是一个局部变量，其作用城就是这个函数。如果在顶层代码中使用`var`语句，它声明的是全局变量，在整个Javascript程序中都是可见的。正如在《[3.2.1 全局变量和局部变量](http://helinjiang.com/note/javascript/variable.html#h_global_local_variable)》提到的，全局变量是全局对象的属性。然而和其他全局对象属性不同的是，`var`声明的变量是无法通过`delete`删除的。
*   如果`var`语句中的变量没有指定初始化表达式，那么这个变量的值初始为`undefined`。《[3.2.3 声明提前](http://helinjiang.com/note/javascript/variable.html#h_hoisting)》已经提到，变量在声明它们的脚本或函数中都是有定义的，变量声明语句会被“提前“至脚本或者函数的顶部。但是初始化的操作则还在原来`var`语句的位置执行，在声明语句之前变量的值是`undefined`。
*   需要注意的是，`var`语句同样可以作为`for`循环或者`for/in`循环的组成部分（和在循环之外声明的变量声明一样，这里声明的变量也会“提前”）。
*   注意，多次声明同一个变量是无所谓的。

## 2. function

关键字`function`用来定义函数。在《[4.3 函数定义表达式](http://helinjiang.com/note/javascript/expression.html#h_function_definition_expressions)》中我们已经见过函数定义表达式，函数定义也可以写成语句的形式。

```javascript
var f = function(x){return x+1;} //函数定义表达式
function f(x){return x+1;} //函数声明语句
```

函数声明语句的语法如下，`funcname`是要声明的函数的名称的标识符。函数名之后的圆括号中是参数列表，参数之间用逗号分隔。当调用函数时，这些标识符则指代传入函数的实参。

```javascript
function funcname([arg1[,arg2[...,argn]]]){
    statements
}
```

和`var`语句一样，函数声明语句创建的变量也是无法删除，但这些变量是可以重写的。

【函数声明语句和函数定义表达式的区别】