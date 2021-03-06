# 原理解析

> 主要是一些前端书籍的读书笔记
## 作用域和闭包

**`js`的编译原理**
比起那些<b>编译</b>过程只有<i>词法分析</i>、<i>语法分析</i>以及<i>代码生成</i>三个步骤的语言的编译器，js引擎要复杂得多。
js的编译过程不是发生在构建之前的，大部分情况下编译发生在代码执行前的几微秒内。
所以，任何js代码片段在执行前都要进行编译(通常在执行前)。
如`var a = 2;`对于js编译器首先会对这段程序进行编译，然后做好执行它的准备，并且通常马上就会执行。
编译三个步骤如下：
  - 词法分析过程会将由字符组成的字符串分解成(对编程语言来说)有意义的代码块(被称之为<b>词法单元</b>)，如`var a= 2;`会被分解成: `var、a、=、2、;`;
  - 语法分析过程是将词法单元流(数组)转换成一个由元素主机嵌套所组成的代表了程序语法结构的树(被称之为<b>抽象语法树AST</b>)；
  - 代码生成是将AST转换为可执行代码的过程。

理解js工作原理必须先知道下面三个家伙: 
  - 引擎: 从头到尾负责整个js程序的编译及执行过程;
  - 编译器: 负责语法分析及代码生成等任务;
  - 作用域: 负责收集并维护由所有声明的标识符(变量)组成的一系列查询，并实施一套非常严格的规则，确定当前执行的代码对这些标识符的访问权限。

下面通过将`var a = 2;`分解，看看引擎、编译器和作用域三者如何协同工作的。
  - 编译器首先会将这段程序分解成词法单元，然后将词法单元解析成一个树结构，但是当编译器开始进行代码生成时，并不是像以前理解一样“为一个变量分配内存，将其命名为a，然后将值2保存进这个变量”，这个理解是不正确的;
  - 实际上，编译器遇到`var a`时，会询问作用域是否已经有一个该名称的变量存在同一个作用域的集合中。如果是，编译器会忽略该声明，继续进行编译；否则它会要求作用域在当前作用域的集合中声明一个新的变量，并命名为`a`;
  - 接下来编译器会为引擎生成运行时所需的代码，这些代码被用来处理`a = 2`这个赋值操作;
  - 引擎运行时会首先询问作用域，在当前作用域中是否存在一个叫`a`的变量。如果是，引擎就会使用这个变量；否则，引擎就会继续查找该变量直至最外层作用域(即全局作用域);
  - 如果引擎最终找到`a`变量，就会将`2`赋值给它。否则引擎就会抛出异常。
**总结**
  变量的赋值操作会执行两个动作，首先编译器会在当前作用域中声明一个变量(若之前没有声明过)，然后在运行时引擎会在作用域链中查找该变量，如果能够找到就会对它赋值。