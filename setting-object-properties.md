设置对象属性
===

可以通过点（`.`）或方括号（`[]`）运算符来获取属性的值。运算符左侧应当是一个表达式，它返回一个对象。

*   对于点（`.`）来说，右侧必须是一个以属性名称命名的简单标识符。
*   对于方括号（`[]`）来说，方括号内必须是一个计算结果为字符串的表达式，这个字符串就是属性的名字。

查询一个不存在的属性并不会报错，而是返回`undefined`。

和查询属性值的写法一样，通过点和方括号也可以创建属性或给属性赋值，但需要将它们放在赋值表达式的左侧。

```javascript
var book = {
    author:"helinjiang",
    "main title":"Hello, JavaScript!"
};
var author = book.author; //得到book的“author”属性
var title = book["main title"]; //得到book的“main title”属性
var otherfiled = book.otherfiled; //因为book中没有otherfiled这个属性，因此返回undefined

book.edition = 6; //给book创建一个名为“edition”的属性
book["main title"] = "ECMAScript"; //给“main title”属性赋值
```