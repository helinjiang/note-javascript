对象属性的四个特性
===

数据属性有四个特性，分别是它的值（value）、可写性（writable）、可枚举性（enumerable）和可配置性（configurable）

在ECMAScript 3中无法设置这些特性，所有通过ECMAScript 3的程序创建的属性都是可写的、可枚举的和可配置的，且无法对这些特性做修改；而在ECMAScript 5中提供了查询和设置这些属性特性的API。这些API对于库的开发者来说非常重要，因为：

*   可以通过这些API给原型对象添加方法，井将它们设置成不可枚举的，这让它们看起来更像内置方法。
*   可以通过这些API给对象定义不能修改或删除的属性，借此‘锁定”这个对象。