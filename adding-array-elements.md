添加数组元素
===

## 1. 为新索引赋值

添加数组元素最简单的方法：为新索引赋值。

```javascript
var a = []; //开始是一个空数组
a[0] = "zero"; //然后向其中添加元素
a[1] = "one";
```

## 2. push()方法

`push()`方法在数组末尾增加一个或多个元素。在数组尾部压入一个元素时，与给数组`a[a.length]`赋值是一样的。

```javascript
var a = []; //开始是一个空数组
a.push("zero"); //在末尾添加一个元素，等价于a[a.length]="zero"，此时a=["zero"]
a.push("one","two"); //再在末尾添加两个个元素，此时a=["zero","one","two"]
```

## 3. unshift()方法

`unshift()`方法在数组的首部插入一个元素，并且将其他元素依次移动更高的索引处。

```javascript
var a=["zero"]; 
a.unshift("test"); //在首部插入一个元素后，a=["test","zero"]
```

## 4. splice()方法

`splice()`是一个通用的方法来插入、删除或替换数组元素。

```javascript
var a=["zero","one","two"];
a.splice(1,0,"test"); //执行完毕之后，a=["zero", "test", "one", "two"]
```