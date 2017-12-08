# 基础类型

> 在js的类型基础上ts，还拓展了实用的枚举类型，同时，ts还提供了静态的代码分析，可以分析代码结构和提供的类型注解。

- 布尔值
  ```js
    let isDone: boolean = false;
  ```

- 数字
  ```js
    let num1 = 6;
    let num2 = 5.2;
  ```

- 字符串
  ```js
    let name: string = "snoopy";
    let age: number = 18;

    // 模板字符串
    let introduce = `Hello, my name is ${ name }, 
      I'm ${ age } years old.`;

  ```

- 数组
  ```js
    // 在元素类型(number)后面加上[]，表示由此类型元素(number)组成一个数组
    let list1: number[] = [1, 2, 3];

    // 数组泛型，Array<number>
    let list2: Array<number> = [1, 2, 3];
  ```

- 元组
> 元组类型(Tuple)允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。
  ```js
    let tuple1: [string, number];

    tuple1 = ["snoopy", 18]; // right
    tuple1 = [18, "snoopy"]; // error
    console.log(tuple1[0].substr(1)); // right
    console.log(tuple1[1].substr(1)); // error
    
    // 访问越界的元素，会使用联合类型替代->(string|number)
    tuple1[3] = 'fifi'; // right，字符串可以赋值给(string|number)类型
    tuple[6] = true; // error，布尔不是(string|number)类型

  ```

- 枚举
> 枚举是ts对js标准数据类型的补充，其可为一组数值赋予名字。
  ```js
    enum Color {hotpink, skyblue, yellowgreen};
    let hot: Color = Color.hotpink;

    // 默认，从0为元素编号，可以手动指定
    enum Color {hotpink=1, skyblue, yellowgreen};
    enum Color {hotpink=2, skyblue = 4, yellowgreen=1};

    // 可以通过枚举的值得到它的名字
    enum Color {hotpink=1, skyblue, yellowgreen};
    let colorName: string = Color[2];
    alert(colorName); // skyblue


  ```

- `Any`
> 对于可能来自动态的内容而不确定变量类型情况，通常在编译阶段不对这些变量的类型进行检查，可以使用`any`类型来标记这些变量。
  ```js
    let notSure: any = 4;
    notSure = "maybe a string instead";
    notSure = false;

    // 在对现有代码改写时，作用显著，允许调用任意方法。
    notSure.ifItExists();
    notSure.toFixed();

    // 当只知道一部分数据的类型时，如一组数组中包含不同类型的数据。
    let list: any[] = [1, true, "snoopy"];
    list[1] = 100;
    
  ```

- `Void`
> `Void`类型表示没有任何类型。如一个没有返回值的函数，会常见到返回值得类型是`void`
  ```js
    function warnUser(): void{
      alert("this is a warning message");
    }
  ```

- 类型断言
> 类型断言使用的场景是确切知道数据类型时，只是在编译阶段起作用。
  ```js
    // "尖括号"语法
    let someValue: any = "this is a string";
    let strLength: number = (<string>someValue).length;

    // `as`语法
    let strLength: number = (someValue as string).length;
  ```

- `Numll`和`Undefined`
> 默认，二者是所有类型的子类，可以把其赋值给number类型的变量。
> 但是，当指定`--strictNullChecks`标记，二者只可赋值给其本身和`void`。
> `--strictNullChecks`的使用场景是：当想传入一个`string`或`null`或`undefined`，可以使用联合类型(string|null|undefined)

- `Never`
> `never`类型表示那些永不存在的值的类型。
> 其是任何类型的子类型，也可以赋值给任何类型；然而，没有类型是never的子类型或可以赋值给never类型（除了never本身之外）。 即使 any也不可以赋值给never。
  ```js
    // 返回never的函数必须存在无法达到的终点
    function error(message: string): never {
      throw new Error(message);
    }

    // 推断的返回值类型为never
    function fail() {
      return error("Something failed");
    }

    // 返回never的函数必须存在无法达到的终点
    function infiniteLoop(): never {
      while (true) {
      }
    }
  ```
  