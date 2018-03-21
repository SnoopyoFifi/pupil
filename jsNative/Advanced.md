# Advanced
## 执行环境及作用域

## 变量的作用域


## 闭包

```js
  // 创建一个闭包
function makeCounter() {
  let k = 0;

  return function() {
    return ++k;
  };
}

const counter = makeCounter();

console.log(counter());  // 1
console.log(counter());  // 2

```

> `makeCounter` 这个函数的代码块，在返回的函数中，对局部变量 `k` ，进行了引用，导致局部变量无法在函数执行结束后，被系统回收掉，从而产生了闭包。
而这个闭包的作用就是，`保留住` 了局部变量，使内层函数调用时，可以重复使用该变量；而不同于全局变量，该变量只能在函数内部被引用。

- 什么是闭包

> 闭包就是一个具有封闭的对外不公开的包裹结构或空间；
可以保留局部变量不被释放的代码块，被称为一个闭包；
换句话说，闭包其实就是创造出了一些函数私有的 "持久化变量" 。

- 闭包的创造条件是
 
> 存在内、外两层函数；内层函数对外层函数的局部变量进行了引用

- 闭包要解决的问题

> 函数内的数据不允许外界访问，要解决的问题就是间接访问该数据，函数可以构成闭包

- 函数可以构成闭包

> 一般函数是一个代码结构的封闭结构, 即包裹的特性, 同时根据作用域规则, 只允许函数访问外部的数据, 外部无法访问函数内部的数据, 即封闭的对外不公开的特性。因此，函数可以构成闭包

- 访问函数内部变量

```js
function foo(){
  var num1 = Math.random();
  function func(){
    retrun num1;
  } 
  return func;
}

var f = foo();
// f 可以直接访问 num， 而且多次访问，访问的也是同一个，并不会返回新的num
var res1 = f();
var res2 = f();
```

- 访问多个变量

```js
function foo(){
  var num1 = Math.random();
  var num2 = Math.random();
  // 可以将多个函数包含在一个对象里返回，这样就能在函数外部操作当前函数内的多个变量
  return {
    num1: function(){
      return num1;
    },
    num2: function(){
      return num2;
    }
  }
}
```

- 获取数据及修改这个数据

```js
function foo(){
  var num = Math.random();
  return {
    getNum: function(){
      return num;
    },
    setNum: function(value){
      num = value;
    }
  }
}
```

- 闭包的基本结构

> 一般闭包要解决的问题就是要想办法间接的获得函数内部数据的使用权。其基本使用模型如下：

   - 写一个函数，函数内定义一个新函数，返回新函数，用新函数获得函数内的数据
   - 写一个函数，函数内定义一个对象，对象中绑定多个函数（方法），返回对象，利用对象的方法访问函数内的数据。

## `this` 的指向
[javascript_this](http://www.cnblogs.com/isaboy/p/javascript_this.html)

> `Javascript`的 `this`总是指向一个对象，而具体指向哪个对象是<b>在运行时基于函数的执行环境动态绑定的</b>，而非函数被声明时的环境。

- `this`的四种指向
  + 作为对象的方法调用。
  + 作为普通函数调用。
  + 构造器调用。
  + `Function.prototype.call`或`Function.prototype.apply`调用。

- 作为对象的方法调用

> 当函数作为对象的方法被调用时，`this` 指向该对象。
  
  ```js
    var obj = {
      name: 'snoopy',
      getName: function() {
        alert(this === obj);
        alert(this.name);
      }
    }

    obj.getName();
  ```

- 作为普通函数调用

> 当函数作为普通函数方式调用时，此时的`this`总是指向全局对象(浏览器环境中是`window`)。

  ```js
    window.name = 'snoopy';
    var getName = function() {
      return this.name;
    }
    console.log(getName());
  
    // or
    
    window.name = 'snoopy';
    var myObject = {
      name: 'fifi',
      getName: function() {
        return this.name;
      }
    }

    var getName = myObject.getName;
    console.log(getName()); // snoopy
  ```

- 构造器调用

> js中函数都可以当作构造器使用来创建对象。当用`new`运算符调用函数时，该函数总会返回一个对象，构造器里的`this`就指向返回的这个对象。
> 
> 如果构造器显式的返回了一个`object`类型的对象，那么此次运算结果最终返回这个对象，而非`this`。

  ```js
    var myClass = function() {
      this.name = 'snoopy';
    }
    var obj = new myClass();
    alert(obj.name); // snoopy

    // 构造器显示返回一个对象
    var myClass = {
      this.name = 'snoopy';
      return {
        name: 'fifi'
      }
    }
    var obj = new myClass();
    alert(obj.name);// fifi
  ```

- `Function.prototype.call`或`Function.prototype.apply`调用

> 跟普通的函数调用相比，用`call`或`apply`可以动态的改变传入函数的`this`

  ```js
    var obj1 = {
      name: 'snoopy',
      getName: function() {
        return this.name;
      }
    }

    var obj2 = {
      this.name = 'fifi'
    }

    console.log(obj1.getName()); // snoopy
    console.log(obj2.getName.call(obj2)); // fifi
  ```

- 丢失的`this`

> 对象的方法当作了普通函数调用，`this`指向了全局`window`

```js
  var obj = {
    name: 'snoopy',
    getName: function() {
      return this.name;
    }
  }

  console.log(obj.getName()); // snoopy

  var getName2 = obj.getName;
  console.log(getName2()); // undefine
```


> 使用短函数替换`document.getElementById`
```js
  var getId = function(id) {
    return document.getElementById(id);
  }
  // 使用以下方式会报错，
  // 原因是`document.getElementById`方法内部实现需要用到`this`，本来`this`的指向是`document`
  // 但是使用getId引用再调用，此时成了普通函数调用。
  var getId = document.getElementById;
  getId('test');

  // 使用`apply`把`document`当作`this`传入getId函数，重新更改`this`指向
  document.getElementById = (function(func){
    return function() {
      return func.apply(document, arguments);
    }  
  })(document.getElementById);
  var getId = document.getElementById;

```


**注意**： 函数的执行过程

  >JavaScript 中的函数既可以被当作普通函数执行，也可以作为对象的方法执行，这是导致 this 含义如此丰富的主要原因。
  >
  >一个函数被执行时，会创建一个执行环境（`ExecutionContext`），函数的所有的行为均发生在此执行环境中，构建该执行环境时，JavaScript 首先会创建 >arguments变量，其中包含调用函数时传入的参数。
  >
  >接下来创建作用域链。
  >
  >然后初始化变量，首先初始化函数的形参表，值为 arguments变量中对应的值，如果 arguments变量中没有对应值，则该形参初始化为 undefined。
  >
  >如果该函数中含有内部函数，则初始化这些内部函数。
  >
  >如果没有，继续初始化该函数内定义的局部变量，需要注意的是此时这些变量初始化为 `undefined`，其赋值操作在执行环境（`ExecutionContext`>）创建成功后，函数执行时才会执行，这点对于理解 JavaScript 中的变量作用域非常重要。
  >
  >最后为 this变量赋值，如前所述，会根据函数调用方式的不同，赋给 this全局对象，当前对象等。
  >
  >至此函数的执行环境（`ExecutionContext`）创建成功，函数开始逐行执行，所需变量均从之前构建好的执行环境（`ExecutionContext`）中读取。


## `call` & `apply`

> `call` & `apply`是在`ECAMScript 3`中给`Function`的原型定义的两个方法。

- `call`和`apply`的区别
  + 二者作用一样，区别在于传入参数的形式不同。
  + `apply`接受两个参数：一个参数指定了函数体内`this`对象的指向；第二个参数为一个带下标的集合(数组、类数组)，`apply`方法把集合中的元素作为参数传递给被调用的函数。
    ```js
      var func = functiong(a, b, c) {
        alert([a, b, c]); // [2, 3, 4]
      };
      func.apply(null, [2, 3, 4]);
    ```
  
  + `call`传入的参数不固定：第一个参数也是代表函数体内的`this`指向；从第二个参数开始往后，每个参数被依次传入函数。
    ```js
      var func = function(a, b, c) {
        alert([a, b, c]); // [2, 3, 4]
      }
      func.call(null, 2, 3, 4)
    ```
  
  + 如果传入的一个参数为`null`，函数体内的`this`会指向默认的宿主对象，在浏览器中就是`window`；但是在严格模式下，`this`为`null`。
    ```js
      var func = function(a, b, c) {
        alert(this === window); // true
      };
      func.apply(null, [1, 2, 3])

      var func = function(a, b, c) {
        "use strict";
        alert(this === null); // true
      };
      func.apply(null, [1, 2, 3]);
    ```
 
  + 同时，传入`null`另有用途，比如借用其他对象的方法，传入`null`来代替某个具体的对象。
    ```js
        Math.max.apply(null, [1, 2, 3, 4])
    ```

  + 注意：
    
    > 当调用一个函数时，`JavaScript`的解释器并不会计较形参和实参在数量、类型以及顺序上的区别，`JavaScript`的参数在内部就是用一个数组来表示的。
    > 
    > 从这个意义上说， `apply` 比 `call` 的使用率更高，我们不必关心具体有多少参数被传入函数，只要用 `apply` 一股脑地推过去就可以了。
    > 
    > `call` 是包装在 apply 上面的一颗语法糖，如果我们明确地知道函数接受多少个参数，而且想一目了然地表达形参和实参的对应关系，那么也可以用 `call` 来传送参数。
  

- `call`和`apply`的用法
  + 改变`this`指向 
    ```js
      var obj1 = {
        name: 'snoopy'
      };
      var obj2 = {
        name: 'fifi'
      };
      window.name = 'window';

      var getName = function(){
        alert(this.name);
      }
      getName(); // window
      getName.call(obj1); // snoopy 
      getName.call(obj2); // fifi
    ```

  + 修正不经意间更改的`this`指向
    ```js
      // 问题：
      document.getElementById('div1').onclick = function() {
        alert(this.id); // div1
        var func = function(){
          alert(this.id); // undefined
        }
        func();
      };

      // 使用call修正func函数内的this
      document.getElementById('div1').onclick = function() {
        var func = function() {
          alert(this.id); // div1
        }
        func.call(this);
      };

      // 使用apply修正document.getElementById函数内部丢失的this
      document.getElementById = (function(func){
        return function() {
          return func.apply(document, arguments);// this重新指向document
        }  
      })(document.getElementById)
    ```

  + `Function.prototype.bind`
  
    ```js
      // `Function.prototype.bind`用来指定函数内部的`this`指向,在大部分高级浏览器都内置了，下面模拟一个：
      Function.prototype.bind = function(context) {
        var self = this;
        return function() {
          return self.apply( context, arguments );
        }
      }

      var obj = {
        name: 'snoopy'
      };

      var func = function() {
        alert(this.name);  // snoopy
      }.bind(obj);
      func();
      // 终结版
      Function.prototype.bind = function() {
        var self = this, // 保存原函数
            context = [].shift.call(arguments), // 需要绑定的this上下文
            args = [].slice.call(arguments);  // 剩余的参数转成数组 
        return function() {  // 返回一个新函数
          return self.apply( context, [].concat.call(args, [].slice.call(arguments)) );
            // 执行新的函数的时候，会把之前传入的context作为新函数体内的this
            // 并且组合两次分别传入的参数，作为新函数的参数
        }
      };

      var obj = {
        name: 'snoopy'
      };

      var func = function(a, b, c, d) {
        alert(this.name);  // snoopy
        alert([a, b, c, d]);  // [1, 2, 3, 4]
      }.bind(obj, 1, 2);
      func(3, 4);
    ```

  + 借用其他对象的方法
    
    > 借用构造函数，类似继承的效果
    
    ```js
        var A = function(name) {
          this.name = name;
        };
        var B = function() {
          A.apply(this, arguments)
        };
        B.prototype.getName = function() {
          return this.name;
        };

        var b = new B('snoopy');
        console.log(b.getName()); // snoopy

    ```

    > 给像函数的参数列表`arguments`一样的类数组对象添加一个新元素，通常会借用`Array.prototype.push`。
    > 类似的，使用`Array.prototype.slice`将`arguments`转为真正的数组；
    > 使用`Array.prototype.shift`截去`arguments`列表中头一个元素；
    
    ```js
      (function(){
        Array.prototype.push.call(arguments, 3);
        console.log(arguments); // [1, 2, 3] 
      })(1, 2)
    ```
    
  **注意**: Array.prototype.push`在V8引擎中的具体实现
    
    ```js
      function ArrayPush() {
        var n = TO_UINT32( this.length ); // 被 push 的对象的 length
        var m = %_ArgumentsLength(); // push 的参数个数
        for (var i = 0; i < m; i++) {
        this[ i + n ] = %_Arguments( i ); // 复制元素 (1)  对象本身要可以存取属性；
      }
      this.length = n + m; // 修正 length 属性的值 (2) 对象的 length 属性可读写。
        return this.length;
      };
    ```

    > 可以看到， `Array.prototype.push` 实际上是一个属性复制的过程，
    > 
    > 把参数按照下标依次添加到被 `push` 的对象上面，顺便修改了这个对象的 `length` 属性。
    > 
    > 至于被修改的对象是谁，到底是数组还是类数组对象，这一点并不重要。只要满足上述(1)(2)两点就可以使用`push`。




## DOM的事件编程

事件是一种异步编程的实现方式，本质上是程序各个组成部分之间的通信。

### EventTarget接口

DOM的事件操作（监听和触发），都定义在`EventTarget`接口。`Element`节点、`document`节点和`window`对象，都部署了这个接口。此外，`XMLHttpRequest`、`AudioNode`、`AudioContext`等浏览器内置对象，也部署了这个接口。

该接口就是三个方法。

- `addEventListener`：绑定事件的监听函数
- `removeEventListener`：移除事件的监听函数
- `dispatchEvent`：触发事件

#### addEventListener()

`addEventListener`方法用于在当前节点或对象上，定义一个特定事件的监听函数。

```javascript
// 使用格式
target.addEventListener(type, listener[, useCapture]);

// 实例
window.addEventListener('load', function () {...}, false);
request.addEventListener('readystatechange', function () {...}, false);
```

`addEventListener`方法接受三个参数。

- `type`：事件名称，大小写敏感。
- `listener`：监听函数。事件发生时，会调用该监听函数。
- `useCapture`：布尔值，表示监听函数是否在捕获阶段（capture）触发（参见后文《事件的传播》部分），默认为`false`（监听函数只在冒泡阶段被触发）。老式浏览器规定该参数必写，较新版本的浏览器允许该参数可选。为了保持兼容，建议总是写上该参数。

下面是一个例子。

```javascript
function hello() {
  console.log('Hello world');
}

var button = document.getElementById('btn');
button.addEventListener('click', hello, false);
```

上面代码中，`addEventListener`方法为`button`元素节点，绑定`click`事件的监听函数`hello`，该函数只在冒泡阶段触发。

`addEventListener`方法可以为当前对象的同一个事件，添加多个监听函数。这些函数按照添加顺序触发，即先添加先触发。如果为同一个事件多次添加同一个监听函数，该函数只会执行一次，多余的添加将自动被去除（不必使用`removeEventListener`方法手动去除）。

```javascript
function hello() {
  console.log('Hello world');
}

document.addEventListener('click', hello, false);
document.addEventListener('click', hello, false);
```

执行上面代码，点击文档只会输出一行`Hello world`。

如果希望向监听函数传递参数，可以用匿名函数包装一下监听函数。

```javascript
function print(x) {
  console.log(x);
}

var el = document.getElementById('div1');
el.addEventListener('click', function () { print('Hello'); }, false);
```

上面代码通过匿名函数，向监听函数`print`传递了一个参数。

#### removeEventListener()

`removeEventListener`方法用来移除`addEventListener`方法添加的事件监听函数。

```javascript
div.addEventListener('click', listener, false);
div.removeEventListener('click', listener, false);
```

`removeEventListener`方法的参数，与`addEventListener`方法完全一致。它的第一个参数“事件类型”，大小写敏感。

注意，`removeEventListener`方法移除的监听函数，必须与对应的`addEventListener`方法的参数完全一致，而且必须在同一个元素节点，否则无效。

#### dispatchEvent()

`dispatchEvent`方法在当前节点上触发指定事件，从而触发监听函数的执行。该方法返回一个布尔值，只要有一个监听函数调用了`Event.preventDefault()`，则返回值为`false`，否则为`true`。

```javascript
target.dispatchEvent(event)
```

`dispatchEvent`方法的参数是一个`Event`对象的实例。

```javascript
para.addEventListener('click', hello, false);
var event = new Event('click');
para.dispatchEvent(event);
```

上面代码在当前节点触发了`click`事件。

如果`dispatchEvent`方法的参数为空，或者不是一个有效的事件对象，将报错。

下面代码根据`dispatchEvent`方法的返回值，判断事件是否被取消了。

```javascript
var canceled = !cb.dispatchEvent(event);
  if (canceled) {
    console.log('事件取消');
  } else {
    console.log('事件未取消');
  }
}
```

### 监听函数

监听函数（listener）是事件发生时，程序所要执行的函数。它是事件驱动编程模式的主要编程方式。

DOM提供三种方法，可以用来为事件绑定监听函数。

#### HTML标签的on-属性

HTML语言允许在元素标签的属性中，直接定义某些事件的监听代码。

```html
<body onload="doSomething()">
<div onclick="console.log('触发事件')">
```

上面代码为`body`节点的`load`事件、`div`节点的`click`事件，指定了监听函数。

使用这个方法指定的监听函数，只会在冒泡阶段触发。

注意，使用这种方法时，`on-`属性的值是将会执行的代码，而不是一个函数。

```html
<!-- 正确 -->
<body onload="doSomething()">

<!-- 错误 -->
<body onload="doSomething">
```

一旦指定的事件发生，`on-`属性的值是原样传入JavaScript引擎执行。因此如果要执行函数，不要忘记加上一对圆括号。

另外，Element元素节点的`setAttribute`方法，其实设置的也是这种效果。

```javascript
el.setAttribute('onclick', 'doSomething()');
```

#### Element节点的事件属性

Element节点对象有事件属性，同样可以指定监听函数。

```javascript
window.onload = doSomething;

div.onclick = function(event){
  console.log('触发事件');
};
```

使用这个方法指定的监听函数，只会在冒泡阶段触发。

#### addEventListener方法

通过`Element`节点、`document`节点、`window`对象的`addEventListener`方法，也可以定义事件的监听函数。

```javascript
window.addEventListener('load', doSomething, false);
```

addEventListener方法的详细介绍，参见本节EventTarget接口的部分。

在上面三种方法中，第一种“HTML标签的on-属性”，违反了HTML与JavaScript代码相分离的原则；第二种“Element节点的事件属性”的缺点是，同一个事件只能定义一个监听函数，也就是说，如果定义两次onclick属性，后一次定义会覆盖前一次。因此，这两种方法都不推荐使用，除非是为了程序的兼容问题，因为所有浏览器都支持这两种方法。

addEventListener是推荐的指定监听函数的方法。它有如下优点：

- 可以针对同一个事件，添加多个监听函数。

- 能够指定在哪个阶段（捕获阶段还是冒泡阶段）触发回监听函数。

- 除了DOM节点，还可以部署在`window`、`XMLHttpRequest`等对象上面，等于统一了整个JavaScript的监听函数接口。

#### this对象的指向

实际编程中，监听函数内部的`this`对象，常常需要指向触发事件的那个Element节点。

`addEventListener`方法指定的监听函数，内部的`this`对象总是指向触发事件的那个节点。

```javascript
// HTML代码为
// <p id="para">Hello</p>

var id = 'doc';
var para = document.getElementById('para');

function hello(){
  console.log(this.id);
}

para.addEventListener('click', hello, false);
```

执行上面代码，点击`<p>`节点会输出`para`。这是因为监听函数被“拷贝”成了节点的一个属性，所以`this`指向节点对象。使用下面的写法，会看得更清楚。

```javascript
para.onclick = hello;
```

如果将监听函数部署在Element节点的`on-`属性上面，`this`不会指向触发事件的元素节点。

```html
<p id="para" onclick="hello()">Hello</p>
<!-- 或者使用JavaScript代码  -->
<script>
  pElement.setAttribute('onclick', 'hello()');
</script>
```

执行上面代码，点击`<p>`节点会输出`doc`。这是因为这里只是调用`hello`函数，而`hello`函数实际是在全局作用域执行，相当于下面的代码。

```javascript
para.onclick = function () {
  hello();
}
```

一种解决方法是，不引入函数作用域，直接在`on-`属性写入所要执行的代码。因为`on-`属性是在当前节点上执行的。

```html
<p id="para" onclick="console.log(id)">Hello</p>
<!-- 或者 -->
<p id="para" onclick="console.log(this.id)">Hello</p>
```

上面两行，最后输出的都是`para`。

总结一下，以下写法的`this`对象都指向Element节点。

```javascript
// JavaScript代码
element.onclick = print
element.addEventListener('click', print, false)
element.onclick = function () {console.log(this.id);}

// HTML代码
<element onclick="console.log(this.id)">
```

以下写法的`this`对象，都指向全局对象。

```javascript
// JavaScript代码
element.onclick = function (){ doSomething() };
element.setAttribute('onclick', 'doSomething()');

// HTML代码
<element onclick="doSomething()">
```

### 事件的传播

#### 传播的三个阶段

当一个事件发生以后，它会在不同的DOM节点之间传播（propagation）。这种传播分成三个阶段：

- **第一阶段**：从window对象传导到目标节点，称为“捕获阶段”（capture phase）。

- **第二阶段**：在目标节点上触发，称为“目标阶段”（target phase）。

- **第三阶段**：从目标节点传导回window对象，称为“冒泡阶段”（bubbling phase）。

这种三阶段的传播模型，会使得一个事件在多个节点上触发。比如，假设点击`<div>`之中嵌套一个`<p>`节点。

```html
<div>
  <p>Click Me</p>
</div>
```

如果对这两个节点的`click`事件都设定监听函数，则`click`事件会被触发四次。

```javascript
var phases = {
  1: 'capture',
  2: 'target',
  3: 'bubble'
};

var div = document.querySelector('div');
var p = document.querySelector('p');

div.addEventListener('click', callback, true);
p.addEventListener('click', callback, true);
div.addEventListener('click', callback, false);
p.addEventListener('click', callback, false);

function callback(event) {
  var tag = event.currentTarget.tagName;
  var phase = phases[event.eventPhase];
  console.log("Tag: '" + tag + "'. EventPhase: '" + phase + "'");
}

// 点击以后的结果
// Tag: 'DIV'. EventPhase: 'capture'
// Tag: 'P'. EventPhase: 'target'
// Tag: 'P'. EventPhase: 'target'
// Tag: 'DIV'. EventPhase: 'bubble'
```

上面代码表示，`click`事件被触发了四次：`<p>`节点的捕获阶段和冒泡阶段各1次，`<div>`节点的捕获阶段和冒泡阶段各1次。

1. 捕获阶段：事件从`<div>`向`<p>`传播时，触发`<div>`的`click`事件；
2. 目标阶段：事件从`<div>`到达`<p>`时，触发`<p>`的`click`事件；
3. 目标阶段：事件离开`<p>`时，触发`<p>`的`click`事件；
4. 冒泡阶段：事件从`<p>`传回`<div>`时，再次触发`<div>`的`click`事件。

注意，用户点击网页的时候，浏览器总是假定`click`事件的目标节点，就是点击位置的嵌套最深的那个节点（嵌套在`<div>`节点的`<p>`节点）。所以，`<p>`节点的捕获阶段和冒泡阶段，都会显示为`target`阶段。

事件传播的最上层对象是`window`，接着依次是`document`，`html`（`document.documentElement`）和`body`（`document.dody`）。也就是说，如果`<body>`元素中有一个`<div>`元素，点击该元素。事件的传播顺序，在捕获阶段依次为`window`、`document`、`html`、`body`、`div`，在冒泡阶段依次为`div`、`body`、`html`、`document`、`window`。

#### 事件的代理

由于事件会在冒泡阶段向上传播到父节点，因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件。这种方法叫做事件的代理（delegation）。

```javascript
var ul = document.querySelector('ul');

ul.addEventListener('click', function(event) {
  if (event.target.tagName.toLowerCase() === 'li') {
    // some code
  }
});
```

上面代码的`click`事件的监听函数定义在`<ul>`节点，但是实际上，它处理的是子节点`<li>`的`click`事件。这样做的好处是，只要定义一个监听函数，就能处理多个子节点的事件，而且以后再添加子节点，监听函数依然有效。

如果希望事件到某个节点为止，不再传播，可以使用事件对象的`stopPropagation`方法。

```javascript
p.addEventListener('click', function(event) {
  event.stopPropagation();
});
```

使用上面的代码以后，`click`事件在冒泡阶段到达`<p>`节点以后，就不再向上（父节点的方向）传播了。

但是，`stopPropagation`方法只会阻止当前监听函数的传播，不会阻止`<p>`节点上的其他`click`事件的监听函数。如果想要不再触发那些监听函数，可以使用`stopImmediatePropagation`方法。

```javascript
p.addEventListener('click', function(event) {
 event.stopImmediatePropagation();
});

p.addEventListener('click', function(event) {
 // 不会被触发
});
```

### Event对象

事件发生以后，会生成一个事件对象，作为参数传给监听函数。浏览器原生提供一个`Event`对象，所有的事件都是这个对象的实例，或者说继承了`Event.prototype`对象。

`Event`对象本身就是一个构造函数，可以用来生成新的实例。

```javascript
event = new Event(typeArg, eventInit);
```

Event构造函数接受两个参数。第一个参数是字符串，表示事件的名称；第二个参数是一个对象，表示事件对象的配置。该参数可以有以下两个属性。

- `bubbles`：布尔值，可选，默认为`false`，表示事件对象是否冒泡。
- `cancelable`：布尔值，可选，默认为`false`，表示事件是否可以被取消。

```javascript
var ev = new Event(
  'look',
  {
    'bubbles': true,
    'cancelable': false
  }
);
document.dispatchEvent(ev);
```

上面代码新建一个`look`事件实例，然后使用`dispatchEvent`方法触发该事件。

IE8及以下版本，事件对象不作为参数传递，而是通过`window`对象的`event`属性读取，并且事件对象的`target`属性叫做`srcElement`属性。所以，以前获取事件信息，往往要写成下面这样。

```javascript
function myEventHandler(event) {
  var actualEvent = event || window.event;
  var actualTarget = actualEvent.target || actualEvent.srcElement;
  // ...
}
```
 
上面的代码只是为了说明以前的程序为什么这样写，在新代码中，这样的写法不应该再用了。

#### event.bubbles，event.eventPhase

以下属性与事件的阶段有关。

**（1）bubbles**

bubbles属性返回一个布尔值，表示当前事件是否会冒泡。该属性为只读属性，只能在新建事件时改变。除非显式声明，Event构造函数生成的事件，默认是不冒泡的。

```javascript
function goInput(e) {
  if (!e.bubbles) {
    passItOn(e);
  } else {
    doOutput(e);
  }
}
```

上面代码根据事件是否冒泡，调用不同的函数。

**（2）event.eventPhase**

eventPhase属性返回一个整数值，表示事件目前所处的节点。

```javascript
var phase = event.eventPhase;
```

- 0，事件目前没有发生。
- 1，事件目前处于捕获阶段，即处于从祖先节点向目标节点的传播过程中。该过程是从Window对象到Document节点，再到HTMLHtmlElement节点，直到目标节点的父节点为止。
- 2，事件到达目标节点，即target属性指向的那个节点。
- 3，事件处于冒泡阶段，即处于从目标节点向祖先节点的反向传播过程中。该过程是从父节点一直到Window对象。只有bubbles属性为true时，这个阶段才可能发生。

### event.cancelable，event.defaultPrevented

以下属性与事件的默认行为有关。

**（1）cancelable**

cancelable属性返回一个布尔值，表示事件是否可以取消。该属性为只读属性，只能在新建事件时改变。除非显式声明，Event构造函数生成的事件，默认是不可以取消的。

```javascript
var bool = event.cancelable;
```

如果要取消某个事件，需要在这个事件上面调用preventDefault方法，这会阻止浏览器对某种事件部署的默认行为。

**（2）defaultPrevented**

defaultPrevented属性返回一个布尔值，表示该事件是否调用过preventDefault方法。

```javascript
if (e.defaultPrevented) {
  // ...
}
```

#### event.currentTarget，event.target

以下属性与事件的目标节点有关。

**（1）currentTarget**

currentTarget属性返回事件当前所在的节点，即正在执行的监听函数所绑定的那个节点。作为比较，target属性返回事件发生的节点。如果监听函数在捕获阶段和冒泡阶段触发，那么这两个属性返回的值是不一样的。

```javascript
function hide(e){
  console.log(this === e.currentTarget);  // true
  e.currentTarget.style.visibility = "hidden";
}

para.addEventListener('click', hide, false);
```

上面代码中，点击para节点，该节点会不可见。另外，在监听函数中，currentTarget属性实际上等同于this对象。

**（2）target**

target属性返回触发事件的那个节点，即事件最初发生的节点。如果监听函数不在该节点触发，那么它与currentTarget属性返回的值是不一样的。

```javascript
function hide(e){
  console.log(this === e.target);  // 有可能不是true
  e.target.style.visibility = "hidden";
}

// HTML代码为
// <p id="para">Hello <em>World</em></p>
para.addEventListener('click', hide, false);
```

上面代码中，如果在para节点的em子节点上面点击，则`e.target`指向em子节点，导致em子节点（即World部分）会不可见，且输出false。

在IE6—IE8之中，该属性的名字不是target，而是srcElement，因此经常可以看到下面这样的代码。

```javascript
function hide(e) {
  var target = e.target || e.srcElement;
  target.style.visibility = 'hidden';
}
```

### event.type，event.detail，event.timeStamp，event.isTrusted

以下属性与事件对象的其他信息相关。

**（1）type**

`type`属性返回一个字符串，表示事件类型，大小写敏感。

```javascript
var string = event.type;
```

**（2）detail**

`detail`属性返回一个数值，表示事件的某种信息。具体含义与事件类型有关，对于鼠标事件，表示鼠标按键在某个位置按下的次数，比如对于dblclick事件，detail属性的值总是2。

```javascript
function giveDetails(e) {
  this.textContent = e.detail;
}

el.onclick = giveDetails;
```

**（3）timeStamp**

`timeStamp`属性返回一个毫秒时间戳，表示事件发生的时间。

```javascript
var number = event.timeStamp;
```

Chrome在49版以前，这个属性返回的是一个整数，单位是毫秒（millisecond），表示从Unix纪元开始的时间戳。从49版开始，该属性返回的是一个高精度时间戳，也就是说，毫秒之后还带三位小数，精确到微秒。并且，这个值不再从Unix纪元开始计算，而是从`PerformanceTiming.navigationStart`开始计算，即表示距离用户导航至该网页的时间。如果想将这个值转为Unix纪元时间戳，就要计算`event.timeStamp + performance.timing.navigationStart`。

下面是一个计算鼠标移动速度的例子，显示每秒移动的像素数量。

```javascript
var previousX;
var previousY;
var previousT;

window.addEventListener('mousemove', function(event) {
  if (!(previousX === undefined ||
        previousY === undefined ||
        previousT === undefined)) {
    var deltaX = event.screenX - previousX;
    var deltaY = event.screenY - previousY;
    var deltaD = Math.sqrt(Math.pow(deltaX, 2) + Math.pow(deltaY, 2));

    var deltaT = event.timeStamp - previousT;
    console.log(deltaD / deltaT * 1000);
  }

  previousX = event.screenX;
  previousY = event.screenY;
  previousT = event.timeStamp;
});
```

**（4）isTrusted**

`isTrusted`属性返回一个布尔值，表示该事件是否为真实用户触发。

```javascript
var bool = event.isTrusted;
```

用户触发的事件返回`true`，脚本触发的事件返回`false`。

### event.preventDefault()

preventDefault方法取消浏览器对当前事件的默认行为，比如点击链接后，浏览器跳转到指定页面，或者按一下空格键，页面向下滚动一段距离。该方法生效的前提是，事件的cancelable属性为true，如果为false，则调用该方法没有任何效果。

该方法不会阻止事件的进一步传播（stopPropagation方法可用于这个目的）。只要在事件的传播过程中（捕获阶段、目标阶段、冒泡阶段皆可），使用了preventDefault方法，该事件的默认方法就不会执行。

```javascript
// HTML代码为
// <input type="checkbox" id="my-checkbox" />

var cb = document.getElementById('my-checkbox');

cb.addEventListener(
  'click',
  function (e){ e.preventDefault(); },
  false
);
```

上面代码为点击单选框的事件，设置监听函数，取消默认行为。由于浏览器的默认行为是选中单选框，所以这段代码会导致无法选中单选框。

利用这个方法，可以为文本输入框设置校验条件。如果用户的输入不符合条件，就无法将字符输入文本框。

```javascript
function checkName(e) {
  if (e.charCode < 97 || e.charCode > 122) {
    e.preventDefault();
  }
}
```

上面函数设为文本框的keypress监听函数后，将只能输入小写字母，否则输入事件的默认事件（写入文本框）将被取消。

如果监听函数最后返回布尔值false（即return false），浏览器也不会触发默认行为，与preventDefault方法有等同效果。

#### event.stopPropagation()

`stopPropagation`方法阻止事件在DOM中继续传播，防止再触发定义在别的节点上的监听函数，但是不包括在当前节点上新定义的事件监听函数。

```javascript
function stopEvent(e) {
  e.stopPropagation();
}

el.addEventListener('click', stopEvent, false);
```

将上面函数指定为监听函数，会阻止事件进一步冒泡到el节点的父节点。

#### event.stopImmediatePropagation()

`stopImmediatePropagation`方法阻止同一个事件的其他监听函数被调用。

如果同一个节点对于同一个事件指定了多个监听函数，这些函数会根据添加的顺序依次调用。只要其中有一个监听函数调用了stopImmediatePropagation方法，其他的监听函数就不会再执行了。

```javascript
function l1(e){
  e.stopImmediatePropagation();
}

function l2(e){
  console.log('hello world');
}

el.addEventListener('click', l1, false);
el.addEventListener('click', l2, false);
```

上面代码在el节点上，为click事件添加了两个监听函数l1和l2。由于l1调用了stopImmediatePropagation方法，所以l2不会被调用。

### 自定义事件和事件模拟

除了浏览器预定义的那些事件，用户还可以自定义事件，然后手动触发。

```javascript
// 新建事件实例
var event = new Event('build');

// 添加监听函数
elem.addEventListener('build', function (e) { ... }, false);

// 触发事件
elem.dispatchEvent(event);
```

上面代码触发了自定义事件，该事件会层层向上冒泡。在冒泡过程中，如果有一个元素定义了该事件的监听函数，该监听函数就会触发。

由于IE不支持这个API，如果在IE中自定义事件，需要使用后文的“老式方法”。

#### CustomEvent()

Event构造函数只能指定事件名，不能在事件上绑定数据。如果需要在触发事件的同时，传入指定的数据，需要使用CustomEvent构造函数生成自定义的事件对象。

```javascript
var event = new CustomEvent('build', { 'detail': 'hello' });
function eventHandler(e) {
  console.log(e.detail);
}
```

上面代码中，CustomEvent构造函数的第一个参数是事件名称，第二个参数是一个对象，该对象的detail属性会绑定在事件对象之上。

下面是另一个例子。

```javascript
var myEvent = new CustomEvent("myevent", {
  detail: {
    foo: "bar"
  },
  bubbles: true,
  cancelable: false
});

el.addEventListener('myevent', function(event) {
  console.log('Hello ' + event.detail.foo);
});

el.dispatchEvent(myEvent);
```

IE不支持这个方法，可以用下面的垫片函数模拟。

```javascript
(function () {
  function CustomEvent ( event, params ) {
    params = params || { bubbles: false, cancelable: false, detail: undefined };
    var evt = document.createEvent( 'CustomEvent' );
    evt.initCustomEvent( event, params.bubbles, params.cancelable, params.detail );
    return evt;
   }

  CustomEvent.prototype = window.Event.prototype;

  window.CustomEvent = CustomEvent;
})();
```

#### 事件的模拟

有时，需要在脚本中模拟触发某种类型的事件，这时就必须使用这种事件的构造函数。

下面是一个通过MouseEvent构造函数，模拟触发click鼠标事件的例子。

```javascript
function simulateClick() {
  var event = new MouseEvent('click', {
    'bubbles': true,
    'cancelable': true
  });
  var cb = document.getElementById('checkbox');
  cb.dispatchEvent(event);
}
```

#### 自定义事件的老式写法

老式浏览器不一定支持各种类型事件的构造函数。因此，有时为了兼容，会用到一些非标准的方法。这些方法未来会被逐步淘汰，但是目前浏览器还广泛支持。除非是为了兼容老式浏览器，尽量不要使用。

**（1）document.createEvent()**

document.createEvent方法用来新建指定类型的事件。它所生成的Event实例，可以传入dispatchEvent方法。

```javascript
// 新建Event实例
var event = document.createEvent('Event');

// 事件的初始化
event.initEvent('build', true, true);

// 加上监听函数
document.addEventListener('build', doSomething, false);

// 触发事件
document.dispatchEvent(event);
```

createEvent方法接受一个字符串作为参数，可能的值参见下表“数据类型”一栏。使用了某一种“事件类型”，就必须使用对应的事件初始化方法。

|事件类型|事件初始化方法|
|--------|--------------|
|UIEvents|event.initUIEvent|
|MouseEvents|event.initMouseEvent|
|MutationEvents|event.initMutationEvent|
|HTMLEvents|event.initEvent|
|Event|event.initEvent|
|CustomEvent|event.initCustomEvent|
|KeyboardEvent|event.initKeyEvent|

**（2）event.initEvent()**

事件对象的initEvent方法，用来初始化事件对象，还能向事件对象添加属性。该方法的参数必须是一个使用`Document.createEvent()`生成的Event实例，而且必须在dispatchEvent方法之前调用。

```javascript
var event = document.createEvent('Event');
event.initEvent('my-custom-event', true, true, {foo:'bar'});
someElement.dispatchEvent(event);
```

initEvent方法可以接受四个参数。

- type：事件名称，格式为字符串。
- bubbles：事件是否应该冒泡，格式为布尔值。可以使用event.bubbles属性读取它的值。
- cancelable：事件是否能被取消，格式为布尔值。可以使用event.cancelable属性读取它的值。
- option：为事件对象指定额外的属性。

#### 事件模拟的老式写法

事件模拟的非标准做法是，对document.createEvent方法生成的事件对象，使用对应的事件初始化方法进行初始化。比如，click事件对象属于MouseEvent对象，也属于UIEvent对象，因此要用initMouseEvent方法或initUIEvent方法进行初始化。

**（1）event.initMouseEvent()**

initMouseEvent方法用来初始化Document.createEvent方法新建的鼠标事件。该方法必须在事件新建（document.createEvent方法）之后、触发（dispatchEvent方法）之前调用。

initMouseEvent方法有很长的参数。

```javascript
event.initMouseEvent(type, canBubble, cancelable, view,
  detail, screenX, screenY, clientX, clientY,
  ctrlKey, altKey, shiftKey, metaKey,
  button, relatedTarget
);
```

上面这些参数的含义，参见MouseEvent构造函数的部分。

模仿并触发click事件的写法如下。

```javascript
var simulateDivClick = document.createEvent('MouseEvents');

simulateDivClick.initMouseEvent('click',true,true,
  document.defaultView,0,0,0,0,0,false,
  false,false,0,null,null
);

divElement.dispatchEvent(simulateDivClick);
```

**（2）UIEvent.initUIEvent()**

`UIEvent.initUIEvent()`用来初始化一个UI事件。该方法必须在事件新建（document.createEvent方法）之后、触发（dispatchEvent方法）之前调用。

```javascript
event.initUIEvent(type, canBubble, cancelable, view, detail)
```

该方法的参数含义，可以参见MouseEvent构造函数的部分。其中，detail参数是一个数值，含义与事件类型有关，对于鼠标事件，这个值表示鼠标按键在某个位置按下的次数。

```javascript
var e = document.createEvent("UIEvent");
e.initUIEvent("click", true, true, window, 1);
```

