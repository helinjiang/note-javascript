枚举对象属性
===

通常用`for/in`循环遍历对象的属性，ECMAScript 5还提供了两个更好用的替代方案。

## 1. for/in遍历

`for/in`循环可以在循环体中遍历对象中所有可枚举的属性（包括自有属性和继承的属性），把属性名称赋值给循环变量。对象继承的内置方法是不可枚举的，但在代码中给对象添加的属性都是可枚举的（除非用下文中提到的一个方法将它们转换为不可枚举的）。

```javascript
//一般变量某个对象的属性（不包括方法）会如下
for (p in obj){
    //1.跳过继承的属性
    if(!obj.hasOwnProperty(p)){
        continue;
    }

    //2.跳过方法
    if(typeof obj[p] === "function"){
        continue;
    }

    //do something
}
```

## 2. Object.keys()

ECMAScript 5定义了`Object.keys()`，它返回一个数组，这个数组由对象中可枚举的自有属性的名称组成。

## 3. Object.getOwnPropertyNames()

ECMAScript 5定义了`Object.getOwnPropertyNames()`，它返回一个数组，这个数组由对象的所有属性的名称组成，而不仅仅是可枚举的属性。