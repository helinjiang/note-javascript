不可变的原始值和可变的对象引用
===

本章节的标题很绕口，但它很实在的表达了两个意思：

 - 原始值是不可以改变的
 - 对象引用是可以改变的

JavaScript中的原始值(undefined、null、布尔值、数字和字符串)与对象(包括数组和函数等)有着根本区别。

## 1. 原始值不可更改

任何方法都无法更改(或“突变”)一个原始值。

对于数字和布尔值来说显然如此——改变数字的值本身就说不通。

而对字符串来说不那么明显了，因为字符串看起来像由字符组成的数组，我们期望可以通过指定索引来修改字符串中的字符。实际上，JavaScript是禁止这样做的。字符中所有的方法看上去返回了一个修改后的字符串，但实际上返回的是一个新的字符串值，而原有的字符串保持不变。

```javascript
var s = "hello"; //定义一个由小写字母组成的文本
s.toUpperCase(); //返回"HELLO"，但并没有改变s的值
s //"hello"，原始字符串的值并未改变
```

## 2. 原始值的比较是值的比较

只有两个原始值的值相等时，它们才相等。比如字符串，当且仅当它们长度相等且每个索引的字符都相等时，JavaScript才认为它们相等。

## 3. 对象是可变的

对象是可变的，即它们的值是可以修改的。

```javascript
var o = {x:1}; //定义一个对象
o.x = 2; //通过修改对象的属性值来改变对象
o.y = 3; //再次更改这个对象，给它增加一个新属性

var a = [1,2,3]; //定义一个数组
a[0] = 0; //更改数组的一个元素
a[3] = 4; //给数组增加一个新元素
```

## 4. 对象的比较是引用的比较

对象的比较并非值的比较，即使两个对象包含同样的属性及相同的值，它们也是不相等的。各个索引元素完全相等的两个数组也不相等。

```javascript
var o={x:1},p={x:1}; //具有相同属性的两个对象
o===p //false，两个单独的对象永不相等
var a=[],b=[];
a===b //false，两个单独的数组永不相等
```

我们通常将对象称为引用类型(reference type)，以此来和JavaScript的原始类型分开。按照术语的叫法，对象值都是引用(reference)，对象的比较均是引用的比较。当且仅当它们都引用同一个基对象时，它们才相等。

```javascript
var a = []; //定义一个引用空数组的变量a
var b = a; //变量b引用同一个数组
b[0] = 1; //通过变量b来修改引用的数组
a[0] //1，变量a也会修改
a === b //true，a和b引用同一个数组，因此它们始终相等
```

## 5. 对象复制

将对象(或数组)赋值给一个变量，仅仅是赋值的引用值，对象本身并没有复制一次。如果你想得到一个对象或数组的副本，则必须显式复制对象的每个属性或数组的每个元素。

```javascript
var a = ['a', 'b', 'c']; //待复制的数组
var b = []; //复制到的目标空数组
for(var i=0; i < a.length; i++){ //遍历a[]中的每个元素
    b[i] = a[i]; //将元素值复制到b中
}
```

## 6. 实际项目中的对象比较

对象的比较是引用的比较，这在实际项目中比较少用。更多的时候，我们会逐一比较两个对象或数组的属性或元素，以确定两者是否真的“相等”。

```javascript
function equalArrays(a, b){
    if(a.length != b.length){ //两个长度不同的数组不“相等”
        return false;
    }
    for(var i=0;i<a.length;i++){ //循环遍历所有元素
        if(a[i] !== b[i]){ //如果有任意元素不等，则数组不“相等”
            return false;
        }
    }
    return true; //各个索引元素完全相等时，两个数组才“相等”
}
```