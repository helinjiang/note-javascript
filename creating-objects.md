创建对象
===

可以通过对象直接量、关键字`new`和（ECMAScript 5中的）`Object.create()`函数来创建对象。

## 1. 通过对象直接量创建对象

对象直接量是由若干名/值对组成的映射表，名/值对中间用冒号分隔，名/值对之间用逗号分隔，整个映射表用花括号括起来。

```javascript
var empty = {}; //没有任何属性的对象
var point = {x:0,y:0}; //两个属性
var point2 = {x:point.x, y:point.y+1}; //更复杂的值
var book = {
    "main title":"JavaScript", //属性名字里有空格，必须用字符串表示
    "sub-title":"The Definitive Guide", //属性名字里有连字符，必须用字符串表示
    "for":"all audiences", //"for"是保留字，因此必须用引号
    author:{ //这个属性的值是一个对象
        firstname:"linjiang", //注意，这里的属性名都没有引号
        subname:"he"
    }
}
```

## 2. 通过new创建对象

`new`运算符创建并初始化一个新对象，关键字`new`后跟随一个函数调用，这里的函数称做构造函数（constructor）。

```javascript
var obj = new Object(); //创建一个空对象，和var obj={}；一样
var reg = new RegExp("js"); //创建一个可以进行模式匹配的RegExp对象
```

## 3. 通过Object.create()创建对象

ECMAScript 5定义了一个名为`Object.create()`的方法，它创建一个新对象，其中第一个参数是这个对象的原型（详细请看xxx），第二个为可选参数，用以对对象的属性进行进一步描述。

```javascript
var o1 = Object.create({x:1, y:2}); //o1继承了属性x和y

var o2 = Object.create(null); //o2不基础任何属性和方法，甚至不包括基础方法，比如toString()

var o3 = Object.create(Object.prototype); //o3和{}和new Object()一样
```

更多详情请看xxx