转换成Boolean类型
===

## 1. 其他原始值转换成Boolean类型
一般而言，转换成布尔值有以下几种方法：

1.  通过 `Boolean()` 函数
2.  隐式的类型转换（一元“`!`”运算符将其操作数转换为布尔值并取反）

```javascript
Boolean([]) //true
!!x //等价于 Boolean(x)，注意是双感叹号
```

## 2. 对象类型转换成Boolean类型
所有对象（包括数组和函数）都转换为true。对于包装对象亦是如此： `new Boolean(false)` 是一个对象而不是原始值，因此它将转换为 `true`。