# let&const

## const
> `const`是用来声明常量的。一旦声明，常量的值就不能改变。

```js
  const monent = require('moment');
```

> 如上`const`很好的应用场景是，当我们引用第三方库时声明变量，用`const`来声明可以避免未来不小心重命名而导致出现`bug`。

## let

> `let`在声明变量时，实际上为js新增了块级作用域，用它声明的变量，只有在其所在的代码块内才有效。

```js
  let name = 'snoopy'
  while(true) {
    let name = 'fifi'
    console.log(name)
  }
  console.log(name)
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


> 在程序或者函数的顶层，let并不会像var一样在全局对象上创造一个属性。

```js
  var x = 'global';
  let y = 'global';
  console.log(this.x); // "global"
  console.log(this.y); // undefined
```

> `let`的暂存死区

>  在同一个函数或同一个作用域中用let重复定义一个变量将引起 `TypeError`(类型错误)。

```js
  if(x){
    let foo;
    let foo;
  }
```


> `let`声明不会被提升到当前执行上下文的顶部。在块中的变量初始化之前，引用将会导致`ReferenceError`(引用错误)

```js
  function do_something() {
    console.log(bar); // undefined
    console.log(foo); // ReferenceError: foo is not defined
    var bar = 1;
    let foo = 2;
  }
```

## 块级作用域

> 语句块是用`{}`界定的，后面没有`;`。


