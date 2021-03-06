类型转换关系表
===

下表简要说明了在JavaScript中如何进行类型转换，粗体部分突出显示了那些让你倍感意外的类型转换。

| 值 | 转换为字符串 | 转换为数字 | 转换为布尔值 | 转换为对象 |
| --- | --- | --- | --- | --- |
| `undefined` | "undefined" | NaN | false | throws TypeError |
| `null`      | "null" | 0 | false | throws TypeError |
| `true`      | "true" | 1 | | new Boolean(true) |
| `false`     | "false" | 0 | | new Boolean(false) |
| `""` (空字符串) | | 0 | false | new String("") |
| `"1.2"` (非空，数字) | | 1.2 | true | new String("1.2") |
| `"one"` (非空，非数字) | | NaN | true | new String("one") |
| `0` | "0" | | false | new Number(0) |
| `-0` | "0" | | false | new Number(-0) |
| `NaN` | "NaN" | | false | new Number(NaN) |
| `Infinity` | "Infinity" | | true | new Number(Infinity) |
| `-Infinity` | "-Infinity" | | true | new Number(-Infinity) |
| `1` (非零) | "1" | | true | new Number(1) |
| `{}` (任意对象) | 参考xxx | 参考xxx | true | |
| `[]` (任意数组) | "" | 0 | true | |
| `[9]` (1个数字元素) | "9" | 9 | true | |
| `['a']` (其他数组) | 使用join()方法 | NaN | true | |
| `function(){}` (任意函数) | 参考xxx | NaN | true | |