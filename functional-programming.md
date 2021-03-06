函数式编程
===

JavaScript并非函数式编程语言，但可以像操控对象一样操控函数，也就是说可以在JavaScript应用函数式编程技术。

假设有一个数组，数组元素都是数字，我们想要计算这些元素的平均值和变准差。

```javascript
//=============
// 非函数式编程风格
//=============
var data = [1, 1, 3, 5, 5]; //这里是待处理的数组

//平均数是所有元素的累加和值除以元素个数
var total = 0;
for (var i = 0; i < data.length; i++) {
    total += data[i];
}
var mean = total / data.length; //平均数是3

//计算标准差
total = 0;
for (var i = 0; i < data.length; i++) {
    var deviation = data[i] - mean;
    total += deviation * deviation;
}
var stddev = Math.sqrt(total / (data.length - 1)); //标准差的值是2

//=============
// 函数式编程风格
//=============
//首先定义两个简单的函数
var sum = function(x, y) {
    return x + y;
};
var square = function(x) {
    return x * x;
};

//然后将这些函数和数组方法配合使用计算出平均数和标准差
var data = [1, 1, 3, 5, 5];
var mean = data.reduce(sum) / data.length;
var deviations = data.map(function(x) {
    return x - mean;
});
var stddev = Math.sqrt(deviations.map(square).reduce(sum) / (data.length - 1));
```