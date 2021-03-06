函数的定义
===

函数使用`function`关键字来定义。定义函数有三种方式：函数声明语句、函数定义表达式和`Function()`构造函数，最后一种很少会用到。函数还可以嵌套在其他函数里。

```javascript
//方法一：函数声明语句
function sayHello(str){
    console.log("hello, " + str);
}

//方法二：函数定义表达式
var sayHello = function(str){
    console.log("hello, " + str);
}

//方法三：Function()构造函数
var sayHello = new Function("str", 'console.log("hello, " + str);');

//嵌套函数
function doSomeThing(){
    var getHello = function(str){
       return "hello, " + str;
    }

    console.log(getHello("world"));
}
```