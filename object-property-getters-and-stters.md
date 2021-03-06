对象属性getter和setter
===

在ECMAScript 5中，定义了`setter`和`getter`两个方法，用于处理对象的属性，由它们定义的属性称做“存取器属性”（accessor property）。相比普通的“数据属性”（data property），它们有更多的灵活性，比如定义属性的可读或可写等。

```javascript
var obj = {
    //x和y是普通的可读写的数据属性
    x:1.0,
    y:1.0,

    //r是可读写的存取器属性，因为它有getter和setter
    //注意：函数体结束后不要忘记带上逗号。
    get r(){return Math.sqrt(this.x*this.x + this.y*this.y);},
    set r(newvalue){
        var oldvalue = Math.sqrt(this.x*this.x + this.y*this.y);
        var ratio = newvalue/oldvalue;
        this.x *= ratio;
        this.y *= ratio;
    },

    //theta是只读存取器属性，因为它只有getter方法
    get theta(){return Math.atan2(this.y, this.x);}
}

obj.r //1.4142135623730951，直接读取r
obj.r = 4; //重新设置r
obj.x; //2.82842712474619，因为我们在上一步设置了r时，x值发生了变化
obj.theta //0.7853981633974483，直接读取theta
obj.theta = 4; //虽然theta没有setter，但此处我们强制赋值
obj.theta //0.7853981633974483，我们再读取theta时，该值并没有变化，是因为它没有setter方法
```