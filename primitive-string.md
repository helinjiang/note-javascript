原始类型之String
===

字符串(string)是一组由16位值组成的不可变的有序序列，每个字符通常来自于Unicode字符集。JavaScript通过字符串类型来表示文本。

字符串长度(length)是其所含16位值的个数。空字符串(empty string)长度为0。

字符串(或其数组)的索引从零开始，即第一个字符的位置是0，第二个字符的位置是1，以此类推，最后一个字符的位置是其length-1。

JavaScript中，并没有表示单个字符的“字符型”。

## 1.字符串直接量

在JavaScript程序中的字符串直接量，是由单引号(')或双引号(")括起来的字符序列。

```javascript
"" //空字符串，它包含0个字符
'helinjiang.com'
"3.14"
'domainName="www.helinjiang.com"' //由单引号定界的字符串中可以包含双引号
"Woldn't you prefer he's book?" //由双引号定界的字符串中可以包含单引号
```

在ECMAScript 3中，字符串直接量必须写在一行中，而在ECMAScript 5中，字符串直接量可以拆分成数行，每行必须以反斜线(\)结束，反斜线和行结束符都不算是字符串直接量的内容。

```javascript
"two\nline" //这里定义了一个显示为两行的字符串
"two\nline".length //8，其中的\n算一个字符长度
"one\    //用三行代码定义了显示为单行的字符串，只在ECMAScript 5中可用，其长度为11，\不算入长度中
long\
line"
```

在客户端JavaScript程序设计中，当JavaScript代码和HTML代码混杂在一起时，建议JavaScript表达式使用单引号，而HTML事件处理程序属性中则使用双引号。

```javascript
<!-- HTML 代码 -->
<button onclick="alert('Thank you')">Click Me</button>

//JS代码
var dom = '<div class="mycss">hello!</div>';
```

## 2.转义字符

在JavaScript字符串中，反斜线(\)符号后加一个字符，用以表示转义。比如需要在单引号定界的字符串内使用撇号(')，就需要用(\')来代替，以避免被按照常规方式解析单引号。

```javascript
var str = 'You\'re right, it can\'t be a quote';
```

JavaScript转义字符如下表所示。未在此列表中的转义，则会被忽略"\"，比如"\#"和"#"等价。最后，上文提到过，在ECMAScript 5中，允许在一个多行字符串直接量里的每行结束处使用反斜线。

表2.1 JavaScript转义字符表

| 转义字符 | 含义 |
|---|---|
| \0 | NULL字符(\u0000) |
| \b | 退格符(\u0008) |
| \t | 水平制表符(\u0009) |
| \n | 换行符(\u000A) |
| \v | 垂直制表符(\u000B) |
| \f | 换页符(\u000C) |
| \r | 回车符(\u000D) |
| \" | 双引号(\u0022) |
| \' | 单引号(\u0027) |
| \\ | 反斜线(\u005C) |
| \xXX | 由两位十六进制数XX指定的Latin-1字符 |
| \uXXXX | 由四位十六进制数XXXX指定的Unicode字符 |

## 3.字符串的使用

**字符串拼接**：如果将加号(+)运算符用于数字，表示两数相加；但将它作用于字符串，则表示字符串连接，将第二个字符串拼接在第一个之后。【关于+号的用法】

**字符串长度**：使用字符串的length属性获得其长度。除了length属性，字符串还提供许多可以调用的方法，在xxx有更多详细信息

```javascript
var s = "hello,world" //定义一个字符串
s.charAt(0) //"h"，第一个字符
s.indexOf("l") //2，字符l首次出现的位置，从0开始计数
s.replace("h","H") //"Hello,world"，全文字符替换
```

**只读数组**：在ECMAScript 5中，字符串可以当作只读数组，除了使用charAt()方法，也可以使用方括号来访问字符串中的单个字符

```javascript
var s = "hello,word";
s[0]  //"h"，等效于s.charAt(0)
s[s.length-1] //"d"，s.charAt(s.length-1)
```

## 4.模式匹配

JavaScript定义了`RegExp()`构造函数，用来创建表示文本匹配模式的对象。这些模式成为“正则表达式”（regular expression）。JavaScript采用Perl中的正则表达式语法，更多内容请看xx一节。`String`和`RegExp`对象均定义了利用正则表达式进行模式匹配和查找与替换的函数。

尽管RegExp并不是语言中的基本数据类型，但是它们依然具有直接量写法，及在两条斜线之间的文本构成了一个正则表达式直接量，第二条斜线之后也可以跟随一个或多个字母，用来修饰匹配模式的含义。

```javascript
/^HTML/  //匹配以HTML开始的字符串
/\bjavascript\b/i  //匹配单词“javascript”，忽略大小写

var text = "testing: 1, 2, 3"; //文本示例
var pattern = /\d+/g;   //匹配所有包含一个或多个数字的实例
pattern.test(test)  //true，匹配成功
text.search(pattern) //9，首次匹配成功的位置
text.match(pattern)  //["1","2","3"]，所有匹配组成的数组
text.replace(pattern, '#'); //"testing: #, #, #"
text.split(/\D+/);  //["","1","2","3"]，用非数字字符截取字符串
```