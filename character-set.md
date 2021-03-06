字符集
===

JavaScript程序是用 `Unicode` 字符集编写的。`Unicode` 是 `ASCII` 和 `Latin-1` 的超集，并支持地球上几乎所有的语言。【更多…】

## 1. JavaScript 区分大小写

JavaScript 是区分大小写的语言，也即关键字、变量、函数名和所有的标识符（identifier）都必须严格区分大小写。

比如，关键字 `while` 必须写成 `while` ，而不能写成 `While` 或者 `WHILE` 。同样， `online` 、 `Online` 、 `OnLine` 和 `ONLINE` 是 4 个不同的变量。

但需要注意的是，HTML 并不区分大小写（尽管 xHTML 区分大小写，但由于浏览器有着非常强大的纠错能力，即使文档中包含很多不严格的大小写，浏览器还是比较“宽容”地正确解析渲染）。由于它和客户端 JavaScript 联系紧密，因此这点区别很容易混淆。许多客户端 JavaScript 对象和属性与它们所表示的 HTML 标签和属性同名。在 HTML 中，这些标签和属性名可以使用大写也可以是小写，而在 JavaScript 中则必须是小写。例如，在 HTML 中设置事件处理程序时，`oncllck` 属性可以写成 `onClick`，但在 JavaScript 代码（或者 xHTML 文档）中，必须使用小写的 `onclick`。【补充例子】

## 2. 空格、换行符

JavaScript 会忽略程序中 [标识（token）](http://en.wikipedia.org/wiki/Token) 之间的空格。多数情况下，JavaScript 同样会忽略换行符（[可选的分号](optional-semicolons.md) 章节中提到了一种意外情形）。

由于可以在代码中随意使用空格和换行，因此可以采用整齐、一致的缩进来形成统一的编码风格，从而提高代码的可读性。【TODO：编程风格】


## 3. 格式控制符

## 4. Unicode转义序列

关于字符集，还有格式控制符、Unicode转义序列、标准化等内容，请参考【这篇文章】

## 3. 其他

关于字符集，还有格式控制符、Unicode转义序列、标准化等内容，请参考【这篇文章】




