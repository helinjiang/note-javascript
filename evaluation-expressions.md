表达式运算
===

JavaScript通过全局函数`eval()`来解释运行由JavaScript源代码组成的字符串，并产生一个值，这就是表达式计算。

真正需要`eval()`来执行代码段的场景并不多见，并且ECMSAScript严格模式对`eval()`函数的行为施加了更多的限制，更多详情请看xxx

```javascript
eval("3+2")  //5
```