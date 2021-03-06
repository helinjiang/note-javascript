闭包
===

JavaScript采用词法作用域（lexical scoping），也就是说，函数的执行依赖于变量作用域，这个作用域是在函数定义时决定的，而不是函数调用时决定的。为了实现这种词法作用域，JavaScript函数对象的内部状态不仅包含函数的代码逻辑，还必须引用当前的作用域链。

函数对象可以通过作用域链相互关联起来，函数体内的变量都可以保存在函数作用域内，这种特性在计算机科学文献中成为“闭包”。

从技术的角度讲，所有的JavaScript函数都是闭包:它们都是对象，它们都关联到作用域链。大多数时候，定义函数时的作用域链在调用函数时依然有效。

```javascript
function counter(){
    var n=0;
    return {
        count: function(){return n++;},
        reset: function(){n=0;}
    };
}

var c = counter(), d=counter(); //创建两个计数器
c.count(); //0
d.count(); //0，它们互不干扰
c.reset(); //reset()和count()方法共享一个作用域链
c.count(); //0，因为我们重置了c
d.count(); //1，我们没有重置d
```