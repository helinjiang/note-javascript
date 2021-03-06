对象的三个特性
===

每一个对象都有与之相关的原型（prototype）、类（class）和可扩展性（extensible attribute）。

## 1. 原型属性

对象的原型属性是用来继承属性的，这个属性如此重要，以至于我们经常把“o的原型属性”直接叫做“o的原型”。

原型属性是在实例对象创建之初就设置好的。

*   通过对象直接量创建的对象，使用`Object.prototype`作为它们的原型。
*   通过`new`创建的对象使用构造函数的`prototype`属性作为它们的原型。
*   通过`Object.create()`创建的对象使用第一个参数（也可以是`null`）作为它们的原型。

## 2. 类属性

对象的类属性是一个字符串，用以表示对象的类型信息。

```javascript
/**
 * 根据默认的toString()方法返回[object class]，来判断对象的类型class为何值
 */
function classof(o){
    if(o===null){
        return "Null";
    } 
    if(o===undefined){
        return "Undefined";
    } 

    return Object.prototype.toString.call(o).slice(8,-1);
}

classof(null) //"Null"
classof(1) //"Number"
classof("") //"String"
classof(false) //"Boolean"
classof({}) //"Object"
classof([]) //"Array"
classof(/./) //"RegExp"
classof(new Date()) //"Date"
classof(window) //"Window"（这是客户端宿主对象）？"global"
function f(){} //定义一个自定义构造函数
classof(new f()) //"Object"
```

## 3. 可扩展性

对象的可扩展性用以表示是否可以给对象添加新属性。所有内置对象和自定义对象都是显式可扩展的，宿主对象的可扩展性是由JavaScript引擎定义的。

可扩展性的目的是将对象“锁定”，以避免外界的干扰，其通常和属性的可配置性与可写性配合使用。