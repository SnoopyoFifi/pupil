# Class

> ES6 引入了`Class`类的概念，作为对象的模板。通过`class`关键字，可以定义类。

## `Class` 的基本语法

- `ES5`中的构造函数与`ES6`中的类
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

- `constructor`方法
  - `constructor`构造方法，是类的默认方法，通过`new`命令生成对象实例时，自动调用该方法。
  - 一个类必须有`constructor`方法，如果没有显式定义，则一个空的`constructor`方法会被默认添加。
  - `constructor`方法默认返回实例对象(即`this`)，可以指定返回另一个对象。

- 类的实例对象
  - 通过`new`命令创建一个类的实例对象。
  - 实例的属性定义在其本身(即定义在`this`对象上)，否则都定义在原型上(即定义在`class`上)。
  - 实例对象的`__proto__`属性都指向类的原型`Point.prototype`，可以通过`__proto__`属性为原型添加方法/属性，但它会影响类所有的实例对象，且该属性是各大厂商添加的私有属性，所以不推荐。
  - 可以使用`Object.getPrototypeOf`方法来获取实例对象的原型，然后为原型添加方法/属性。

- `Class`表达式
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

- 不存在变量提升
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

- 私有方法&私有属性
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

- 继承的实现
  
  ```js
    //定义类
    class Point {
      constructor(x, y) {
        this.x = x;
        this.y = y;
      }

      toString() {
        return '(' + this.x + ', ' + this.y + ')';
      }
    }

    class ColorPoint extends Point {
      constructor(x, y, color) {
        super(x, y);          // 调用父类的constructor(x, y)
        this.color = color;
      }
      toString() {
        return this.color + ' ' + super.toString(); // 调用父类的toString()
      }
    }


    class A {
      static hello() {
        console.log('hello world');
      }
    }
    class B extends A{}
    B.hello();

  ```

  - 注意：
    + 类可以通过`extends`关键字实现继承。
    + `super`表示父类的构造函数，用来新建父类的`this`对象。
    + 子类没有自己的`this`对象，子类必须在`constructor`方法中，调用`super`方法来继承父类的`this`对象。
    + `ES6`中的继承是先创造父类的实例对象`this`(即先调用`super`方法)，然后再用子类的构造函数修改`this`。
    + 所以，必须先调用`super`方法，再使用`this`对象。
    + 父类的静态方法，也会被子类继承。

- `Object.getPrototypeOf()`
  > `Object.getPrototypeOf()`方法可以用来从子类上获取父类。
  
  ```js
    Object.getPrototypeOf(ColorPoint) === Point 
    // true
  ```
    
  - 注意：可以用该方法判断一个类是否继承了另一个类。

- `super`关键字
  + `super`的两种用法：
    * `super`作为函数调用时，代表父类的构造函数。且，子类的构造函数中必须执行一次`super`函数。
    * `super`作为对象时，在普通方法中，指向父类的原型对象；在静态方法中，指向父类。
  
  + `super`作为函数调用时
    ```js
      class A {
        constructor() {
          console.log(new.target.name);  //new.target指向当前正在执行的函数
        }
      }

      class B extends A {
        constructor(){
          super();
        }

        m() {
          super();  //报错
        }
      }

      new A(); 
      // A
      
      new B();
      // B
    ```

    - 注意：
      + 子类B的构造函数中的`super()`代表调用父类的构造函数。
      + `super`虽然代表了父类A的构造函数，但是返回的是子类B的实例，即`super`内部的`this`指向的是B(相当于：A.prototype.constructor.call(this))。
      + `super`作为函数时，只能在子类构造函数中调用，否则会报错。
  + `super`作为对象时
    * 在静态方法与普通方法指向不同
     
      ```js
        class Parent {
          static myMethod(msg) {
            console.log('static', msg);
          }
          myMethod(msg) {
            console.log('instance', msg);
          }
        }

        class Child extends Parent {
          static myMethod(msg) {
            super.myMethod(msg);  // 静态方法中super指向父类
          }
          myMethod(msg) {
            super.myMethod(msg);  // 普通方法中super指向原型
          }
        }

        Child.myMethod(1);
        // static 1
        var child = new Child();
        child.myMethod(2);
        // instance 2
      ```
      
    * 在普通方法中，指向父类的原型对象(父类.prototype)
    
      ```js
        class A {
          constructor() {
            this.p = 2;
            this.y = 4;
            this.z = 6;
          }
          p() {
            return 2;
          }
          print() {
            console.log(this.y);
          }
        }

        A.prototype.x = 3; 

        class B extends A {
          constructor() {
            super();
            console.log(super); // 报错
            console.log(super.valueOf() instanceof B); // true
            console.log(super.p()); // 2
            conosle.log(super.x); // 3
            this.y = 5;
            super.z = 7;
            console.log(super.z); // undefined
            console.log(ths.z); // 7
          }
          get m() {
            return super.p;
          }

          n() {
            super.print();
          }

        }
        let b = new B();
        b.m 
        // undefined
        b.n
        // 5
      ```
  
      - 注意：
        + 由于普通方法中的`super`指向父类的原型对象，所以定义在父类的实例上的方法或属性，是无法通过`super`调用的。
        + `p`是父类`A`实例的属性，`super.p`就引用不到它。
        + `x`是定义在父类的原型对象上的属性，就可以取到。
        + 调用父类方法时，`super.print()`虽然调用的是`A.prototype.print()`，但是`A.prototype.print()`会绑定子类B的`this`(即`super.print.call(this)`)，使得输出的是`5`。
        + 调用父类方法时，`super`就是`this`，通过 `super`对某个属性赋值，赋值的属性会变成子类实例的属性。
        + `super.z`赋值为7，等同于对this.z赋值为7。当读取`super.z`的时候，读的是`A.prototype.z`，所以返回`undefined`。
        + 使用`super`时，必须显式指定是作为函数、还是作为对象使用，否则会报错。如果表明`super`的数据类型，就不会报错。
        + `super.valueOf()`表明`super`是一个对象，因此就不会报错。同时，由于`super`绑定B的`this`，所以`super.valueOf()`返回的是一个B的实例。

  + 由于对象总是继承其他对象的，所以可以在任意一个对象中，使用`super`关键字。
    ```js
      var obj = {
      toString() {
        return "MyObject: " + super.toString();
      }
    };

    obj.toString(); // MyObject: [object Object]
    ```

- 类的`prototype`属性和`__proto__` 属性
  - `Object.setPrototypeOf`方法实现
    ```js
      Object.setPrototypeOf = function(obj, proto) {
        obj.__proto__ = proto;
        return obj;
      }
    ```
  
  - 类的继承实现的模式
    ```js
      class A {}
      class B {}

      // B 的实例继承 A 的实例
      Object.setPrototypeOf(B.prototype, A.prototype);
      // 等同于
      B.prototype.__proto__ = A.prototype;

      // B 的实例继承 A 的静态属性
      Object.setPrototypeOf(B, A);
      // 等同于
      B.__proto__ = A;

      const b = new B();
    ```
    
  - 上述继承链关系可以如下理解：
    - 作为一个对象，子类B的原型(`__proto__`属性)是父类A；
    - 作为一个构造函数，子类B的原型对象(`prototype`属性)是父类A的原型对象(`prototype`属性)的实例。

- `extends`的继承目标
  - 子类继承`Object`类：这时子类就是`Object`的实例。
  - 不存在任何继承：是一个基类，直接继承`Function.prototype`，但是调用后返回的是一个空对象，`A.prototype.__proto__`指向`Object`的`prototype`属性。
  - 子类继承`null`：直接继承`Function.prototype`，`__proto__`指向`Function.prototype`

- 实例的`__proto__`属性
  - 子类的原型的原型，是父类的原型。
    ```js
      var p1 = new Point(2, 3);
      var p2 = new ColorPoint(2, 3, 'red');

      p2.__proto__ === p1.__proto__ 
      // false
      p2.__proto__.__proto__ === p1.__proto__ 
      // true
    ```

  - 通过子类实例的`__proto__.__proto__`属性，可以修改父类实例
    ```js
      p2.__proto__.__proto__.printName = function () {
        console.log('Ha');
      };

      p1.printName() 
      // "Ha"
    ```

- 原生构造函数的继承
  
  - `ES6` 是先新建父类的实例对象`this`，然后再用子类的构造函数修饰`this`，使得父类的所有行为都可以继承。
  - `ES6` 可以自定义原生数据结构（比如`Array、String`等）的子类，这是 `ES5` 无法做到的。
  - `extends`关键字不仅可以用来继承类，还可以用来继承原生的构造函数。

- `Mixin` 模式的实现
  > Mixin 指的是多个对象合成一个新的对象，新对象具有各个组成成员的接口。
  - 简单实现多个对象合成一个新的对象
  ```js
    const a = { a: 'a' };
    const b = { b: 'b' };
    const c = {..a, ...b}; 
    // {a: 'a', b: 'b'}
  ```
  
  - 具体实现多个对象合成一个新的对象 
  ```js
    function mix(...mixins) {
      class Mix {}
      for (let mixin of mixins) {
        copyProperties(Mix, mixin);
        copyProperties(Mix.prototype, mixin.prototype);
      }
      return Mix;
    }

    function copyProperties(target, source) {
      for(let key of Reflect.ownKeys(source)) {
        if ( key !== "constructor"
          && key !== "prototype"
          && key !== "name"
        ) {
          let desc = Object.getOwnPrototyDescriptor(source,key);
          Object.defineProperty(target, key, desc);
        }
      }
    }


    class son extends mix(snoopy, fifi) {}
  ```
  
  - 注意： 上面代码的`mix`函数，可以将多个对象合成为一个类。使用的时候，只要继承这个类即可。
