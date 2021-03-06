条件语句
===

条件语句是通过判断表达式的值来决定执行还是跳过某些语句。这些语句是代码的“决策点”，有时称为“分支”。

## 1. if/else语句

`if`语句是一种基本的控制语句，它让JavaScript程序可以选择执行路径，有条件的执行语句。

```javascript
//形式一：单if
if (expression)
    statement

//形式二：if/else
if (expression)
    statement1
else
    statement2
```

*   `if`语句中括住`expression`的圆括号在语法上是必需的，不能省略。
*   `statement`必须是一条语句，或者使用多条语句合并的语句块。
*   引入`else`从句之后，当`expression`的值是`false`时才执行`else`中的逻辑。

JavaScript中的`if`、`else`匹配规则是：`else`总是和就近的if语句匹配。

```javascript
var i=1,j=1,k=2;
if(i==j)
    if(j == k)
        console.log("i equals k");
else
    console.log("i doesn't equal j"); //错误

/*有时候为了简便省略了花括号，而使用缩进来表明含义，但缩进是不靠谱的，容易出问题，
比如上面的示例，其被JavaScript解释器解析为：*/
var i=1,j=1,k=2;
if(i==j){
    if(j == k)
        console.log("i equals k");
    else
        console.log("i doesn't equal j"); //错误
}

/*建议养成if和else语句主体用花括号括起来的习惯，
这个可读性更强、更易理解、更方便维护和调试*/
var i=1,j=1,k=2;
if(i==j){
    if(j == k){
        console.log("i equals k");
    }
}else{
    console.log("i doesn't equal j"); //花括号让代码结构更加清晰
}
```

## 2. else if 语句

`else if`语句并不是真正的JavaScript语句，它只不过是多条`if/else`语句连在一起时的一种惯用写法。

```javascript
if (n == 1){
    //执行代码块1
}else if (n == 2){
    //执行代码块2
}else if (n == 3){
    //执行代码块3
}else{
    //之前的条件都为false时执行代码块4
}
```

## 3. switch

当所有的分支都依赖于同一个表达式的值时，`else if`并不是最佳解决方案，`switch`语句正适合处理这种情况。`switch`语句首先计算`switch`关键字后的表达式，然后按照从上到下的顺序计算每个`case`后的表达式，直到执行到`case`的表达式的值与`switch`的表达式的值相等时为止。

```javascript
//定义
switch(expression){
    statements
}

//举例
switch(n) {
    case 1: //如果 n===1，从这里开始执行
        //执行代码块1
        break; //停止执行switch语句
    case 2: //如果 n===2，从这里开始执行
        //执行代码块2
        break; //停止执行switch语句
    case 3: //如果 n===3，从这里开始执行
        //执行代码块3
        break; //停止执行switch语句
    default: //所有条件都不匹配
        //执行代码块4
        break; //停止执行switch语句
}
```

*   ECMAScript标准允许每个`case`关键字后跟随任意的表达式，最常见是数字和字符串直接量。
*   `case`的表达式的值和`switch`的表达式的值匹配是“`===`”恒等运算，因此两者都不会做任何类型转换再比较。
*   使用`break`语句来跳出`switch`语句，防止一个`case`语句块执行完后继续执行下一个`case`语句块。
*   如果`switch`表达式与所有`case`表达式都不匹配，则执行标记为“`default:`”的语句块，如果没有“`default:`”标签，则`switch`的整个语句块都将跳过。
*   “`default:`”标签可以放置在`switch`语句内的任何地方，但最合理也最常见的是出现在`switch`的末尾，位于所有`case`标签之后。

更多内容请看xxx