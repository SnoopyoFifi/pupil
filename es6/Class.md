# Class

> ES6 引入了`Class`类的概念，作为对象的模板。通过`class`关键字，可以定义类。

## `ES5`中的构造函数与`ES6`中的类
  - `ES5`中的构造函数
  ```js
    function Point(x, y) {
      this.x = x;
      this.y = y;
    }

    Point.prototype.toString = function() {
      return '(' + this.x + ', ' + this.y + ')';
    };
    var p = new Point(1, 2);
  ```
  
  - `ES6`中的类
```js
  class Point {
    constructor(x, y) {
      this.x = x;
      this.y = y;
    }

    toString() {
      return '(' + this.x + ', ' + this.y + ')';
    }
  }
  
  var point = new Point(1, 2);// 类的实例，及其方法调用
  point.toString();

  typeof Point // "function"
  Point === Point.prototype.constructor // true
  point.constructor === Point.prototype.constructor

  Point.prototype = { // 等同于
    constructor() {},
    toString() {}
  }

  Object.assign(Point.prototype, {
    toString() {},
    toValue() {}  
  })


  Object.keys(Point.prototype) // []
  Object.getOwnPropertyNames(Point.prototype) // ["constructor", "toString", "toValue"]

  Point(); // TypeError；Class constructor Foo cannot be invoked without 'new'

  point.hasOwnProperty('x') // true
  point.hasOwnProperty('toString') // false
  point.__proto__.hasOwnProperty('toString') // true
```

  - 注意：
    + `ES6`中类中`constructor`就是构造方法(对应`ES5`中的构造函数)，`this` 关键字则代表实例对象。
    + 写法上，方法之间是不需要用逗号分隔的，不需要`function`关键字。
    + 构造函数的`prototype`属性在类上依然存在，类的所有方法都定义在`prototype`属性上，可以通过`Object.assign`方法向类中添加多个方法。
    + 类的数据类型是函数，`prototype`对象的`constructor`属性指向类的本身，类本身就指向构造函数(方法)。
    + 类在使用时，也是通过`new`命令，如果直接调用类则会报错。
    + `toString`方法是类内部定义的方法，是不可枚举的(与`ES5`不同)。
    + 方法名可以使用表达式。

## `constructor`方法
  - `constructor`构造方法，是类的默认方法，通过`new`命令生成对象实例时，自动调用该方法。
  - 一个类必须有`constructor`方法，如果没有显式定义，则一个空的`constructor`方法会被默认添加。
  - `constructor`方法默认返回实例对象(即`this`)，可以指定返回另一个对象。

## 类的实例对象
  - 通过`new`命令创建一个类的实例对象。
  - 实例的属性定义在其本身(即定义在`this`对象上)，否则都定义在原型上(即定义在`class`上)。
  - 实例对象的`__proto__`属性都指向类的原型`Point.prototype`，可以通过`__proto__`属性为原型添加方法/属性，但它会影响类所有的实例对象，且该属性是各大厂商添加的私有属性，所以不推荐。
  - 可以使用`Object.getPrototypeOf`方法来获取实例对象的原型，然后为原型添加方法/属性。

## `Class`表达式
  - 类也可以使用表达式的形式定义。

  ```js
    const MyClass = class Me {
      getClassName() {
        return Me.name;
      }
    }
    let inst = new MyClass();
    inst.getClassName() // Me
    Me.name // ReferenceError: Me is not defined

    const MyClass = class{/* 代码块 */}

  ```

  -  注意：
    +  上述类的名字是`MyClass`而不是`Me`，`Me`只在`Class`内部代码可用，指代当前类。
    +  如果类在内部没用到的话，可以省略`Me`。
  
  - 采用`Class`表达式，可以写出立即执行的`Class`
  
  ```js
    let Person = new Class {
      constructor(name) {
        this.name = name;
      }
      sayName() {
        console.log(this.name);
      }
    }('snoopy.Q');

    person.sayName(); // 'snoopy.Q'
  ```

## 不存在变量提升
  - 类不存在变量提升
  ```js
    new Foo(); // ReferenceError
    class Foo {}
  ```

  - 类继承时，由于必须要保证子类在父类之后定义，`ES6`不会把类的声明提升到代码头部。
  ```js
    {
      let Foo = class {};
      class Bar extends Foo {
      }
    }
  ```


## 私有方法&私有属性
  - 私有方法的一种是在方法名前面加上下划线，表示这是一个只限于内部使用的私有方法(但是有缺陷，在外部仍可访问)。
    ```js
      class Widget {
        // 公有方法
        foo(baz) {
          this._bar(baz);
        }

        // 私有方法
        _bar(baz) {
          return this.sanf = baz;
        }
      }
    ```

  - 私有方法的另一种是将方法移出模块，因为模块内部所有的方法都是对外可见的。
    ```js
      class Widget {
        foo(baz) {
          bar.call(this, baz);
        }
      }

      function bar(baz) {
        return this.snaf = baz;
      }
    ```

  - 私有方法还有一种实现思路就是使用`Symbol`值的唯一性。
    ```js
      const bar = Symbol('bar');
      const snaf = Symbol('snaf');

      export default class myClass {
        // 公有方法
        foo(baz) {
          this[bar](baz);
        }

        // 私有方法
        [bar](baz) {
          return this[snaf] = baz;
        }
      }
    ```

  - 同时，私有属性有一个提案，就是在属性名之前添加`#`，当然可以用来写私有方法。
    ```js
      class Point {
        #x;
        constructor(x = 0) {
          #x = +x;
        }

        get x() {return #x}
        set x(value) { #x = +value }
      }
    ```

## `this`指向
  


## `Class`的继承
  
