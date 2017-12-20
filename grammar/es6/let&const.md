# let&const
- var声明与变量提升
    > 变量提升: 使用`var`关键字声明的变量，无论其实际声明位置在何处，都会被视为声明于所在函数的顶部(如果声明不在任意函数内，则视为在全局作用域的顶部)，这就是变量提升

- 块级声明与块级作用域
    + 块级声明: 就是让所声明的变量在指定的作用域外无法被访问。
    + 块级作用域(又称词法作用域)在如下情况被创建:
      * 在一个函数内部
      * 在一个代码块(由一对花括号包裹)内部

- let声明

  > `let`会将变量作用域限制在当前代码块中，而不会将声明提升到当前代码块的顶部。

  ```js
    function getValue(condition){
      if(condition){
        let value = 'blue';
        return value;
      }else{
        // value 在此处不可用
        return null;
      }
      // value 在此处不可用
    }
  ```

  > 同一作用域内禁止重复声明，而在嵌套作用域内声明同名新变量不会报错

  ```js
    var num = 20;
    let num = 10; //语法错误

    var name = "snoopy";
    if(condition) {
      let name = "fifi";  // 不会报错，
      // 这个新变量会屏蔽全局的name变量，从而在局部阻止对于全局name的访问
    }
  ```

- 常量声明

  > `const`是用来声明常量的。一旦声明，常量的值就不能被重新赋值。
  >
  > `const`很好的应用场景是，当我们引用第三方库时声明变量，用`const`来声明可以避免未来不小心重命名而导致出现`bug`。

  ```js
    const monent = require('moment');
  ```

  > const声明会阻止对于变量绑定与变量自身值的修改，但是不会阻止对变量成员的修改。

  ```
    // 使用const声明对象
    const person = {
      name: "snoopy"
    }
    person.name = "fifi"; // 不会报错
    person = {  // 抛出错误
      name: "fifi"; 
    }
  ```

- 暂时性死区

  > 暂时性死区常用于描述`let`或`const`声明的变量为何在声明处之前无法被访问的情形。
  > 
  > 只有执行到变量的声明语句时，该变量才会从暂时性死区内被移除并可以安全使用。
  > 
  > 暂时性死区只是块级绑定的一个独特表现。

  ```js
    console.log(typeof value); // undefined ，
    // 并没有绑定value变量，而typeof仅单纯返回了undefined
    
    if(condition) {
      console.log(typeof value); // 引用错误
      let value = "blue";


    }
  ```

- 循环中的块级绑定
  > `let`声明循环变量`i`，仅在`for`循环内部可用，一旦循环结束，该变量在任意位置都不可访问。
  ```js
    for(var i = 0; i < 10; i++){
      process(items[i]);
    }
    // i可被访问
    console.log(i); //10

    for(let i = 0; i < 10; i++){
      process(item[i]);
    }
    // i不可被访问，报错
    console.log(i);
  ```

- 循环内的let声明

  > 块级作用域出现之前，广泛应用于立即执行函数

  ```js
    // IIFE写法
    (function(){
      var snoopy = ...;
      ...
    }())

    // 块级作用域写法
    {
      let snoopy = ...;
      ...
    }
  ```


  ```js
    var funcs = [];
    for (var i = 0; i < 10; i++) {
      funcs.push(function() { console.log(i); });
    }
    funcs.forEach(function(func) {
      func(); // 输出数值 "10" 十次
    })

    // 使用IIFEs立即执行函数
    var funcs = [];
    for (var i = 0; i < 10; i++) {
      funcs.push((function(value) {  
        // 变量i被传递给IIFE，从而创建了value变量作为自身副本并将值存储于其中。 
        return function() {
          console.log(value);
        }
      }(i)));
    }
    funcs.forEach(function(func) {
      func(); // 从 0 到 9 依次输出
    });

    // 循环内的let声明
    var funcs = [];
    for (let i = 0; i < 10; i++) {
      funcs.push(function() { console.log(i); });
    }
    funcs.forEach(function(func) {
      func(); // 从0到9一次输出
    })
    
    // for-in 与 for-of 循环中使用
    var funcs = [],
        object = {
          a: true,
          b: true,
          c: true
        };
    for(let key in object) {
      funcs.push(function(){
        console.log(key);  
      })
    }
    func.forEach(function(func){
      func(); // 依次输出"a"、"b"、"c" 
    })

  ```

  > `let`解决了用来计数的循环变量泄露为全局变量的问题，let的作用域是块，而var的作用域是函数。

  ```js
  // 计数变量i泄露为全局变量
    var a = [];
    for(var i = 0; i < 10; i++){
      a[i] = function(){
        console.log(i);
      };
    }
    a[6](); // 10

  // let 轻松解决
    var a = [];
    for(let i = 0; i < 10; i++){
      a[i] = function(){
        console.log(i);
      }
    }
    a[6](); // 6
  ```

  > 拓展：闭包如何解决上述问题

  ```js
  // 需求：点击不同clickBox，输出对应的索引。
  // 下面无论点击哪个clickBox都会输出5
    var clickBoxs = document.querySelectorAll('.clickBox'); // 假设有5个clickBox
    for(var i = 0; i < clickBoxs.length; i++){
      clickBoxs[i].onclick = function(){
        console.log(i);
      } 
    }

  // 闭包解决
    function iteratorFactory(i){
      var onclick = function(){
        console.log(i);
      }
      return onclick;
    }
    var clickBoxs = document.querySelectorAll('.clickBox');
    for(var i = 0; i < clickBoxs.length; i++){
      clickBoxs[i].onclick = iteratorFactory(i)
    }
  ```

  > 再看一个栗子彻底理解块级作用域

  ```js
    var list = document.getElementById("list");

    for (let i = 1; i <= 5; i++) {
      var item = document.createElement("LI");
      item.appendChild(document.createTextNode("Item " + i));

      let j = i;
      item.onclick = function (ev) {
        console.log("Item " + j + " is clicked.");
      };
      list.appendChild(item);
    }
  ```

  > 需求: 创建5个`li`,点击不同的`li`能够打印出当前li的序号。</br>
  > 如果用`var`的话，将总是打印出 `Item 5 is Clicked`，因为 `j` 是函数级变量，5个内部函数都指向了同一个 `j` ,而 `j` 最后一次赋值是5。</br>
  > 用了`let`后，`j` 变成块级域（也就是花括号中的块，每进入一次花括号就生成了一个块级域）,所以 5 个内部函数指向了不同的 `j` 。

- 循环中的常量声明
  
  > `const` 能够在`for-in`与`for-of`循环内工作，是因为循环为每次迭代创建了一个新的变量绑定，而不是试图去修改已绑定的变量的值
  
  ```js
    var funcs = [];
    for (const i = 0; i < 10; i++) {  // 在进行第二次循环时报错
      funcs.push(function() { console.log(i); });
    }

    // 在for-in 与 for-of 中使用时，与`let`效果相同
    var funcs = [],
        object = {
          a: true,
          b: true,
          c: true
        };
    for(const key in object) {
      funcs.push(function(){
        console.log(key);  
      })
    }
    func.forEach(function(func){
      func(); // 依次输出"a"、"b"、"c" 
    })
  ```
  
- 全局块级绑定
  > 若想让代码能从全局对象中被访问，你仍然需要使用`var`。在浏览器中跨越帧或窗口去访问代码时，这种做法非常普遍

- 块级绑定总结

  > `let`与`const`块级绑定将词法作用域引入了 JS 。
  >
  > `let`与`const`声明都不会进行提升，并且只会在声明它们的代码块内部存在。
  >
  > 由于块级绑定存在暂时性死区（ TDZ ），试图在声明位置之前访问它就会导致错误。
  > 
  > `let`与`const`的表现在很多情况下都相似于`var`，然而在循环中就不是这样。
  > 
  > 在`for-in`与`for-of`循环中，`let`与`const`都能在每一次迭代时创建一个新的绑定，这意味着在循环体内创建的函数可以使用当前迭代所绑定的循环变量值（而不是像使用`var`  那样，统一使用循环结束时的变量值）。这一点在`for`循环中使用`let`声明时也成立，不过在`for`循环中使用`const`声明则会导致错误。
  > 
  > 块级绑定当前的最佳实践就是：在默认情况下使用`const`，而只在你知道变量值需要被更改的情况下才使用`let`。这在代码中能确保基本层次的不可变性，有助于防止某些类型的错
  误。






