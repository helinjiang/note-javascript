语句
===

在《表达式》一章中提到，表达式在JavaScript中是短语，那么语句（statement）就是JavaScript整句或命令，以分号结束。

表达式计算出一个值，但语句用来执行以使某件事发生。“使某件事发生”一般有两种方法：

*   方法一：计算带有副作用的表达式。诸如赋值和函数调用这些有副作用的表达式，是可以作为单独的语句的，这种把表达式当作语句的用法也称作表达式语句（expression statement）。类似的语句还有声明语句（declaration statement），用来声明新变量或定义新函数。
*   方法二：改变语句的默认执行顺序。JavaScript中有很多语句和控制结构（control structure）来改变语句的默认执行顺序
    *   条件（condition）语句，JavaScript解释器可以根据一个表达式的值来判断是执行还是跳过这些语句，比如if语句和switch语句。
    *   循环（loop）语句，可以重复执行语句，如while和for语句。
    *   跳转（jump）语句，可以让解释器跳转至程序的其他部分继续执行，如break、return和throw语句。

一个JavaScript程序无非是一个以分号分隔的语句集合，所以一旦掌握了JavaScript语句，就可以开始编写JavaScript程序了。