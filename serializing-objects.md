序列化对象
===

对象序列化（serialization）是指将对象的状态转换为字符串，也可以将字符串还原为对象。

ECMAScript 5提供了内置函数`JSON.stringify()`和`JSON.parse()`用来序列化和还原JavaScript对象。在ECMAScript 3环境中没有这两个内置函数，需要额外引入json2.js。

```javascript
var obj = {x:1, y:{z:[false, null, ""]}}; //定义一个测试对象
var str = JSON.stringify(obj); //'{x:1, y:{z:[false, null, ""]}}'
var p = JSON.parse(str); //p是obj的深拷贝
```