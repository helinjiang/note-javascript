删除对象属性
===

`delete`运算符可以删除对象的属性。

```javascript
var book = {
    author:"helinjiang",
    "main title":"Hello, JavaScript!"
};
delete book.author; //book不再有“author”属性
delete book["main title"]; //book不再有“main title”属性
```