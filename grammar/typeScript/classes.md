# 类

> 类是ts的核心，使用ts开发时，大部分代码都是写在类里面的。
> 需要掌握类的定义、构造方法、以及类的继承

- 一个类的简单定义
  ```js

    class Person {  // 声明一个Person类
      static dna = "xy";  // 静态属性

      readonly id: number = 342401;  // 只读属性
      public length: number;  // 公有属性

      protected money: number;  // 受保护属性
      private age: number;  // 私有属性
      public name: string;  // 公有属性
      construction(money: number, theAge: number, name: string){ // 构造方法
        this.money = money;
        this.age = theAge;
        this.name = name;
      }
      // 参数属性, 上面写法等价于
      construction(protected money: number, private age: number, public name: string){
        this.money = money;
        this.age = age;
        this.name = name;
      }
 
      /**************************/

      eat() { // eat方法
        console.log(`My name is ${this.name} , I'm ${this.age} , I have ${this.money}cash, and, I'm eating`);
      }

      distinguishDNA(){  // 鉴定DNA方法
        let xy = Grid.dna;
      }
    }

    let person = new Person(0， 18, "snoopy"); // 创建一个Person实例，调用构造函数初始化实例对象。
    person.length = 15;

    class American extends Person {

      constructor(money: number, age: number, name: string, code: string){
        super(money, age, name);
        this.code = code;
      }

      talk(){
        console.log("bala,bala...");
      }

      work(){
        super.eat();
        this.doWork();
      }

      private doWork() {
        console.log("I'm working")
      }
    }
    let american = new American(-1, 60, "jack");
    anerican.work();
  ```
    
- 类的访问控制符
> `public`为默认访问控制符，公共的属性和方法可以在类的外部和内部访问。
> `private`为私有访问控制符，私有的属性和方法只可以在类的内部访问。
> `protected`为受保护访问控制符，受保护的属性和方法可以在类的内部和其子类被访问。
> `readonly`为只读访问控制符，表示属性为只读的，该属性必须在声明时或构造函数里被初始化。

- 参数属性
> 通过将声明和赋值合并至一处，来避免给类声明属性时，立即在构造函数中赋值；
> 参数属性通过给构造函数参数添加一个访问控制符来声明；
> 使用 `private`限定一个参数属性会声明并初始化一个私有成员；对于 `public`和 `protected`来说也是一样。

- 构造函数
> 在创建类的实例对象(person)的时候，构造函数会被调用一次；
> 并且会执行构造函数来初始化实例对象；
> 构造函数不能在类的外部访问。

- 静态属性
> 那些仅当类被实例化的时候才会被初始化的属性，被称为实例成员，使用`this.`访问；
> 而那些存在于类本身上面而不是类的实例上的属性，被称为静态成员，使用`Grid.`访问；

- 继承
> extend
> super

