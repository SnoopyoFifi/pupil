# 显示数据

> `Angular`中最典型的数据显示方式，就是把`HTML`模板中的控件绑定到`Angular`组件的属性。

- 使用插值表达式显示组件属性
  ```typescript
    import {Component} from '@angular/core';

    @Component({
      selector: 'app-root',
      template: `
        <h1>\{\{title\}\}</h1>
        <h2>my name is: \{\{name\}\}</h2>
      `
    })

    export class AppComponent {
      title = '插值表达式显示组件属性';
      name = 'snoopy';
    }
  ```

  **插值表达式运行过程**: 
  
  - `Angular` 会自动从组件中提取`title`和`myHero`属性的值，并且把这些值插入浏览器中。当这些属性发生变化时，`Angular`就会自动刷新显示。

  - 没有调用 `new` 来创建`AppComponent`类的实例，是 `Angular` 替我们创建了它。

  - `@Component`装饰器中指定的 `CSS` 选择器`selector`，它指定了一个叫`my-app`的元素。 该元素是`index.html`的`body`里的占位符。

  - 当我们通过`main.ts`中的`AppComponent`类启动时，`Angular` 在`index.html`中查找一个`<my-app>`元素， 然后实例化一个`AppComponent`，并将其渲染到`<my-app>`标签中。


- 使用内联模板或者模板文件

  >存放组件模板，可以使用`template`属性把它定义为内联的，或者把模板定义在一个独立的 `HTML` 文件中， 再通过`@Component`装饰器中的`templateUrl`属性， 在组件元数据中把它链接到组件。

- 使用构造函数或者变量初始化
  ```typescript
    export class AppComponent {
      title: string;
      name: string;

      constructor() {
        this.title = "使用构造函数初始化";
        this.name = "snoopy";
      }
    }
  ```

- 使用`ngFor`显示数组属性
  ```typescript
    template: `
      <h1>\{\{title\}\}</h1>
      <h2>MyLove is: \{\{myLove\}\}</h2>
      <p>Names:</p>
      <ul>
        <li *ngFor="let name of names">
          \{\{name\}\}
        </li>
      </ul>
    `

    export class AppComponent {
      title = "使用ngFor显示数组属性";
      names = ["snoopy", "fifi", "jack", "rose"];
      myLove = this.names[1];
    }
  ```

- 为数据创建一个类
  ```typescript
    export class Name {
      constructor(
        public id: number,
        public name: string
      ){}
    }

    names = [
      new Name(1, 'snoopy'),
      new Name(2, 'fifi'),
      new Name(3, 'jack'),
      new Name(4, 'rose')
    ]
    myLove = this.names[1];

    template: `
      <h1>\{\{title\}\}</h1>
      <h2>My love is: \{\{myLove.name\}\}</h2>
      <p>Names:</p>
      <ul>
        <li *ngFor="let name of names">
          \{\{name.name\}\}
        </li>
      </ul>
    `
  ```
  **说明**:
  - 上面定义了具有一个构造函数和两个属性的类。**(用构造函数的参数直接定义属性)**

  - `public id: number`简写语法做的事有：

    + 声明了一个构造函数参数及其类型

    + 声明了一个同名的公共属性

    + 当创建该类的实例时，把该属性初始化为相应的参数值


- 通过`NgIf`进行条件显示
  ```typescript
    <p *ngIf="names.length > 3">还有更多的树</p>
  ```

- 数据显示小结: 
  + 带有双花括号的插值表达式 (interpolation) 来显示一个组件属性。

  + 用 ngFor 显示数组。

  + 用一个 TypeScript 类来为我们的组件描述模型数据并显示模型的属性。

  + 用 ngIf 根据一个布尔表达式有条件地显示一段 HTML。