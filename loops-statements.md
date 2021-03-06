循环语句
===

循环语句（looping statement）可以让一部分代码重复执行。

## 1. while

`while`语句是一个基本循环语句。

```javascript
while (expression)
    statement
```

当表达式`expression`是真值时则循环执行`statement`，注意，使用`while(true)`则会创建一个死循环。

```javascript
//输出0~9
var count = 0;
while(count<10){
    console.log(count);
    count++;
}
```

## 2. do/while

`do/while`循环和`while`循环非常相似，只不过它是在循环的尾部俄不是顶部检测循环表达式，这也意味着循环体至少会执行一次。

```javascript
do
    statement
while (expression);
```

`do/while`循环并不像`while`循环那么常用，两者有两点不同。

*   `do`循环要求必须使用关键字`do`来标识循环的开始，用`while`来标识循环的结尾并进入循环条件判断。
*   `do`循环是用分号结尾的，而`while`循环不需要。

```javascript
//输出0~9
var count = 0;
do{
    console.log(count);
    count++;
}while(count<10);
```

## 3. for

`for`语句对常用的循环模式做了一些简化，更加方便控制循环。

```javascript
for(initialize; test; increment)
    statement

//与之等价的while循环
initialize;
while(test){
    statement;
    increment;
}
```

`initialize`、`test`和`increment`三个表达式之间用分号分隔，它们分别负责初始化操作、循环条件判断和计数器变量的更新。

```javascript
//输出0~9
for(var count=0; count<10; count++){
    console.log(count);
}
```

## 4. for/in

`for/in`语句也使用`for`关键词，但它是和常规的`for`循环完全不同的一类循环。

```javascript
for(variable in object)
    statement
```

`for/in`语句常用于属性枚举，遍历对象属性成员。JavaScript数据不过是一种特殊的对象，因此也可以像枚举对象属性一样枚举数组索引。

```javascript
//对象
var obj = {x:1,y:2,z:3};
for(var p in obj){
    console.log(p + ":" + obj[p]);
}

//数组
var arr=['x','y','z'];
for(var a in arr){
    console.log(a + ":" + arr[a]);
}
```