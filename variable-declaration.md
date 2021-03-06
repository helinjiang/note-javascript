变量声明
===

在JavaScript程序中，使用一个变量之前应当先声明。

## 1. 使用关键字var来声明

变量是使用关键字 `var` 来声明的，也可以通过一个 `var` 关键字来声明多个变量，还可以将变量的初始赋值和变量声明合写在一起。

```javascript
var i; //使用var来声明变量
var i,sum; //使用var也可同时声明多个变量
var i=0,j=1,k=2; //还可以将变量的初始赋值和变量声明合写在一起
```

如果未在 `var` 声明语句中给变量指定初始值，此时它的初始值就是`undefined`。

在for和for/in循环中同样可以使用 `var` 语句，这样可以更简洁地声明在循环体语法内中使用的循环变量。

```javascript
for(var i=0; i<10;i++){
    console.log(i);
}

for(var p in o){
    console.log(p);
}
```

## 2. 无需指定变量的的数据类型

如果你之前编写过诸如C或Java的<a class="jpostcite postcite" role="button" tabindex="0" data-original-title="" title="" style="box-sizing: border-box; color: green; text-decoration: none; cursor: pointer; padding: 0px 5px; background-color: transparent;">静态语言<sup style="box-sizing: border-box; position: relative; font-size: 12px; line-height: 0; vertical-align: baseline; top: -0.5em;">[1]</sup></a>你会注意到JavaScript的变量声明中并没有指定变量的数据类型。JavaScript变量可以是任意数据类型。例如首先将数字赋值给一个变量，然后再将字符串赋值给这个变量，这是完全合法的（但不推荐这么做）。

```javascript
var i=10; //i为数字
i="ten"; //此时i变成了字符串
```

## 3. 重复的声明

使用 `var` 语句重复声明变量是合法且无害的。如果重复声明带有初始化器，那么这就和一条简单的赋值语句没什么样。

## 4. 遗漏的声明

你可以给一个未使用 `var` 语句声明的变量赋值，此时该变量会被JavaScript当作全局变量，这并不会报错（注意：在ECMAScript 5严格模式中会报错），但不推荐这么做；但如果你试图读取一个没有声明的变量的值，则JavaScript会报错。

然而从历史上讲，在非严格模式下，如果给一个未声明的变量赋值，JavaScript实际上会给全局对象创建一个同名属性，并且它工作起来像（但并不完全一样）一个正确声明的全局变量。这意味着你可以侥幸不声明全局变量。但这是一个不好的习惯并会造成很多bug，因此，**你应当始终使用 `var` 来声明变量。**