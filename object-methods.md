对象方法
===

所有的JavaScript对象都从`Object.prototype`继承属性（除了那些不通过原型显示创建的对象），而这些继承属性主要是方法。常见的除了上文提到过的`hasOwnProperty()`、`propertyIsEnumerable()`和`isPrototypeOf()`这三个方法，以及在Object构造函数里定义的静态函数`Object.create()`、和`Object.getPrototypeOf()`等，还有定义在`Object.prototype`里的对象方法`toString()`、`toLocalString()`、`toJSON()`、`valueOf()`方法