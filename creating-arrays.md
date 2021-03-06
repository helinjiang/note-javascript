创建数组
===

我们可以使用数组直接量和调用构造函数`Array()`来创建数组。

## 1. 数组直接量

使用数组直接量（也有的称之为数组的字面量）是创建数组最简单的方法，在方括号中将数组元素用逗号(`,`)隔开即可。

```javascript
var empty = []; //没有元素的数组
var primes = [2,3,5,7,11]; //有5个数值的数组

//3个不同类型的元素和结尾的逗号，注意：misc.length=3
var misc = [1.1, true,"a",]; 

//数组直接量中的值不一定要是常量，它们可以是任意的表达式
var base = 1024;
var table = [base, base+1, base+2, base+3];

//也可以包含对象直接量或其他数组直接量
var b = [[1,{x:1,y:2}],[2,{x:3,y:4}]];

//如果省略数组直接量中的某个值，则被省略的元素将被赋予undefined值
var count = [1,,3]; //数组3个元素
var undefs = [,,]; //允许可选的结尾的逗号，故只有两个元素而非三个
```

## 2. 构造函数Array()

调用构造函数`Array()`是创建数组的另一种方法。[点此](http://www.helinjiang.com/api/javascript/array.html#h_array_constructor)可以查看其更详细的语法定义和解释。

```javascript
var a1 = new Array(); //创建一个空数组，等价于[]
var a2 = new Array(3); //创建长度为3的数组，等价于[undefined,undefined,undefined]
var a3_1 = new Array("3"); //创建长度为1的数组，等价于["3"]
var a3_n = new Array(5,3,1,"testing"); //显示指定，等价于[5,3,1,"testing"]
```