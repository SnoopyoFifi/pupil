# Arrows函数

## 箭头函数对比传统js函数
  - 没有 `this`、`super`、`arguments`、以及函数内部的 `new.target`，上述对象的值由所在的、最靠近的非箭头函数来决定。
  
  - 不能使用`new`调用，箭头函数没有`construct`方法，因此不能被用为构造函数，使用`new`调用箭头函数会抛出错误。

  - 没有原型，也就是没有`prototype`属性。
  
  - 不能更改`this`，`this`的值在函数内部不能被修改，在函数的整个生命周期内其值会保持不变。
 
  - 箭头函数内的`this`对象，通过词法作用域(块级作用域)派生来的，为绑定定义时所在的对象，而不是使用时所在的对象。

  - 没有`arguments`对象，箭头函数没有`arguments`绑定，必须依赖于具名参数或剩余参数来访问函数的参数。

  - 不允许重复的具名参数。

## 箭头函数的使用
  - 当无参数或有多个参数时，就使用一个圆括号`()`代表参数部分；

  ```js
    let fifi = () => 'snoopy';
    let fifi = _ => 'fifi'; // 么有参数用`_`也是可以的

    let haveFun = (fifi, snoopy) => fifi + snoopy;
  ```

  - 当代码块部分多于一条语句时，就要使用花括号`{}`，及`return`语句返回；

  ```js
    let snoopy = (n1, n2) => { return n1 + n2; }
  ```

  - 由于花括号`{}`被解释为代码块，所以当直接返回一个对象时，必须在对象外加圆括号`()`

  ```js
    let getFifi =  sex => ({ sex: female, name: "Fifi" }) 
  ```

  - 支持剩余参数和默认参数

  ```js
    let Fifi = (param1, paramn, ...rest) => {
      console.log(`%c {statements}`, `color: red;`)
    }
  ```


## 创建立即执行函数表达式

  ```js
    let preson = ((name) => {
      return {
        getName: function(){
          return name;
        }
      };  
    })("snoopy");
  ```
