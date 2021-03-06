检测对象属性
===

JavaScript对象可以看做属性的集合，我们经常会检测集合中成员的所属关系——判断某个属性是否存在于某个对象中。可以通过`in`运算符、`hasOwnProperty(）`和`propertyIsEnumerable()`方法来完成这个工作，甚至仅通过属性查询也可以做到这一点。

## 1. in运算符

`in`运算符的左侧是属性名（字符串），右侧是对象。如果对象的自有属性或继承属性中包含这个属性，则返回`true`。

```javascript
var obj = {x:1};
"x" in obj; //true
"y" in obj; //false
"toString" in obj; //true，obj继承了toString属性
```

## 2. hasOwnProperty()

对象的`hasOwnProperty()`方法用来检测给定的名字是否是对象的自有属性，对与继承属性它将返回`false`。

```javascript
var obj = {x:1};
obj.hasOwnProperty("x"); //true
obj.hasOwnProperty("y"); //false
obj.hasOwnProperty("toString"); //false，toString是继承属性
```

## 3. propertyIsEnumerable()

对象的`propertyIsEnumerable()`方法是`hasOwnProperty()`的增强版，只有检测到是自有属性，且这个属性的可枚举性（enumerable attribute）为`true`时，它才返回`true`。

通常由JavaScript代码创建的属性都是可枚举的，除非ECMAScipt 5中使用一个特殊的方法来改变属性的可枚举性。

## 4. 属性查询

和`in`运算符类似，另外一种更简便的方法是使用“`!==`”判断一个属性是否是`undefined`。

```javascript
var obj = {x:1};
obj.x !== undefined; //true
obj.y !== undefined; //false
obj.toString !== undefined; //true，obj继承了toString属性
```

然而有一种场景只能使用`in`运算符而不能使用上述属性访问的方式。`in`操作符可以区分不存在的属性和存在但值为`undefined`的属性。

```javascript
var obj = {x:undefined}; //属性被显示赋值为undefined
obj.x !== undefined //false，属性存在，但值为undefined
obj.y !== undefined //false，属性不存在
"x" in obj; //true，属性存在
"y" in obj; //false，属性不存在
delete obj.x; //删除了属性x
"x" in obj; //false，属性不再存在
```

注意，上述代码中使用的是“`!==`”运算符，而不是“`!=`”，因为前者可以区分`undefined`和`null`。但实际项目中，我们通常不特意做此区分。

```javascript
//如果obj中含有属性x，且x值不是null或undefined，则obj.x乘以2
if(obj.x != null){
    obj.x *= 2;
}

//如果obj中含有属性x，且x的值不能转换为false，则obj.x乘以2，
//也即x是undefined、null、false、" "、0或NaN，则它保持不变
if(obj.x){
    obj.x *= 2;
}
```