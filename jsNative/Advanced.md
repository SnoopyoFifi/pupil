# Advanced

## 闭包

- 什么是闭包

> 闭包就是一个具有封闭的对外不公开的，包裹结构或空间

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








