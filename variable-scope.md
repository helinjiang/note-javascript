变量作用域
===

一个变量的作用域(scope)是程序源代码中定义这个变量的区域。

*   全局变量拥有全局作用域，在JavaScript代码中的任何地方都是有定义的。
*   局部变量的作用域是局限性的，比如函数内声明的变量只在函数体内定义，函数参数也是局部变量，它们只在函数体内有定义。
*   在函数体内，局部变量的优先级高于同名的全局变量。

```javascript
var scope="global"; //声明一个全局变量
function checkscope(){
    var scope = "local"; //声明一个同名的局部变量
    return scope; //返回局部变量的值，而不是全局变量的值
}
checkscope(); //"local"
```

尽管在全局作用域编写代码时可以不写 `var` 语句（强烈建议定义全局变量也要加 `var` ），但声明局部变量时，则必须使用 `var` 语句。

```javascript
scope="global"; //声明一个全局变量，甚至不用var来声明，但强烈建议不要省略var
function checkscope2(){
    scope = "local"; //糟糕！我们刚修改了全局变量
    myscope= "local"; //这里显式地声明了一个新的全局变量并赋值
    return [scope, myscope]; //返回两个值
}
checkscope2(); //["local","local"]，产生了副作用
scope //"local"，全局变量修改了
myscope //"local"，全局命名空间搞乱了
```

### 3.2.2 函数作用域

在一些类似C语言的编程语言中，花括号内的每一段代码都具有各自的作用域，而且变量在声明它们的代码段之外是不可见的，我们称为**块级作用域（block scope）**。而JavaScript中没有块级作用域。JavaScript取而代之地使用了**函数作用域（function scope)**：变量在声明它们的函数体以及这个函数体嵌套的任意函数体内都是有定义的。

```javascript
function test(o){
    var i=0; //i在整个函数体内均是有定义的
    if (typeof o == "object"){
        var j=0; //j在整个函数体内也是有定义的，不仅仅在这个代码段内
        for(var k=0; k<10;k++){  //k在整个函数体内也是有定义的，不仅仅在这个循环内
            console.log(k); //输出数字0~9
        }
        console.log(k); //k已经定义了，且在上述循环中已变化，输出10
    }
    console.log(j); //j已经定义了，且值未发生变化，输出0
}
```

### 3.2.3 声明提前

JavaScript的函数作用域是指在函数内声明的所有变量在函数体内始终是可见的。有意思的是，这意味着变量在声明之前甚至已经可用。JavaScript的这个特性被非正式地称为**声明提前（hoisting)**，即JavaScript函数里声明的所有变量（但不涉及赋值）都被“提前”至函数体的顶部。

“声明提前”这步操作是在JavaScript引擎的“预编译”时运行的，是在代码开始运行之前。更多细节请阅读xxx。

```javascript
var scope="global"; //定义全局变量
function f(){
    console.log(scope); //输出"undefined"，而不是"global"
    var scope="local"; //变量在这里赋初始值，但变量本身在函数体内任何地方均是有定义的
    console.log(scope); //输出"local"
}

//f()函数“预编译”之后等价于下面的方法
function f(){
    var scope; //在函数顶部声明了局部变量
    console.log(scope); //变量存在，但其值为"undefined"
    scope = "local"; //这里将其初始化并赋值
    console.log(scope); //这里它具有了我们所期待的值
}
```

在具有块级作用域的编程语言中，在狭小的作用域里让变量声明和使用变量的代码尽可能靠近彼此，通常来讲．这是一个非常不错的编程习惯。但由于JavaScript没有块级作用域，因此一些程序员特意将变量声明放在函数体顶部，而不是将声明靠近放在使用变量之处。这种做法使得他们的源代码非常清晰地反映了真实的变量作用域。

### 3.2.4 作为属性的变量

当声明一个JavaScript全局变量时，实际上是定义了全局对象的一个属性。

*   当使用 `var` 声明一个变量时，创建的这个属性是不可配置的，也就是说这个变量无法通过 `delete` 运算符删除
*   如果没有使用严格模式，且并给一个未声明的变量赋值的话，JavaScript会自动创建一个全局变量，以这种方式创建的变量是全局对象的正常的可配置属性，并可以删除它们

```javascript
var truevar = 1; //声明一个不可删除的全局变量
fakevar = 2; //创建全局对象的一个可删除的属性
this.fakevar2=3; //同上
delete truevar; //false，变量并没有被删除
delete fakevar; //true，变量被删除
delete this.fakevar2; //true，变量被删除
```

### 3.2.4 作用域链scope chain

JavaScript是基于词法作用域（静态作用域）的语言：通过阅读包含变量定义在内的数行源码就能知道变量的作用域。全局变量在程序中始终都是有定义的。局部变量在声明它的函数体内以及其所嵌套的函数内始终是有定义的。

当定义一个函数时，它实际上是保存一个作用域链。JavaScript需要查找变量 `x` 的值的时候（这个过程称作“变量解析”（variable resolution）），它会从链中的第一个对象开始查找。如果这个对象有一个名为 `x` 的属性，则会直接使用这个属性的值，否则会继续查找链上的下一个对象。从另外一种角度来说，它会先在函数内部查找，查找不到就会向上查找，直到顶层为止。