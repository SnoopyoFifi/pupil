# Dependency Injection
- 依赖注入要点
  + 依赖注入三个重要关键词: **使用者**、**服务(依赖对象)** 及 **注入器**。
   
  + 依赖注入可以实现松耦合，实现真正的可重用组件。

- 注入器
  
  > 注入器只有一种实现方法就是在构造函数中声明。
  
  ```js
    constructor(productService: ProductService){}
    // 组件创建了一个productService，其依赖ProductService，
    // ProductService只是一个token，其实现是由提供器说明
  ```

- 提供器
  > 提供器通常定义在应用级，即`app.module.ts`中，供所有组件或服务使用；也可以定义在某一个组件中，只提供这一个组件使用。
  
  ```js
    // 定义在应用级
    @NgModule({
      provides: [ProductService]  
      // 当token和想要实例化的类名称相同时，可以这么简写。
    })
    // 上面写法等同于
    @NgModule({
      provides: [{
        provide: ProductService,
        // provide声明的就是注入器中的token，这两个token一一对应，
        // angular会到提供器中找到和注入器中相同的token。
        useClass: ProductService
        // 通过useClass实例化一个ProductService类，
        // 此外，useFactory使用工厂模式实例化一个类。
      }]  
    })
    // 可复用性
    @NgModule({
      provide: ProductService,
      useClass: AnotherProductService
      // 当相同的组件在另一个地方使用另一个服务时，可以不必更改组件，
      // 即不更改token，而是更改app.module.ts中的提供器。
    })
  ```

- 依赖注入运行机制
  > 当组件在构造函数中说明需要依赖一个类时，
  > 
  > `Angular`首先会在这个组件自身找有没有提供器，
  > 
  > 如果没有就去这个组件的父组件中找，
  > 
  > 如果也没有就去应用级(app.module.ts)中找。
  > 
  > 找到后就会按照提供器的说明为组件注入它需要的。

- 依赖注入三种实现方法

  - 在组件中生成一个该服务的实例对象
  
  ```js
    import{ Component, OnInit } from '@angular/core';
    // 引入服务
    import{ AuthService } from '../core/auth.service';
    @Component({
      selector: 'app-login',
      template: `
        <div>
          <input #usernameRef type="text">
          <input #passwordRef type="text">
          <button (click)="onClick(usernameRef.value, passwordRef.value)">Login</button>
        </div>
      `,
      style: [],
    })    
    export class LoginComponent implements OnInit{
      // 声明成员变量，其类型为AuthService
      service: AuthService;
      constructor(){
        this.service = new AuthService();
      }
      ngOnInit(){}
      onClick(username, password){
        // 调用service方法
        console.log(`
          auth result is: ${this.service.loginWithCredentials(username, password)}
        `)
      }
    }
  ```
  
  - 在组件中使用注入器声明服务

  ```js
    // 在组件中使用注入器
    import{ Component, OnInit } from '@angular/core';
    // 引入服务
    import{ AuthService } from '../core/auth.service';

    @Component({
      selector: 'app-login',
      template: `
        <div>
          <input #usernameRef type="text">
          <input #passwordRef type="text">
          <button (click)="onClick(usernameRef.value, passwordRef.value)">Login</button>
        </div>
      `,
      style: [],
      // 在providers中定义服务
      providers: [AuthService]
    })    

    export class LoginComponent implements OnInit{
      // 在构造函数中将AuthService实例注入到成员变量service中
      // 而不需要显示的声明(new)成员变量service了
      constructor(private service: AuthService){
        this.service = new AuthService();
      }
      ngOnInit(){}
      onClick(username, password){
        // 调用service方法
        console.log(`
          auth result is: ${this.service.loginWithCredentials(username, password)}
        `)
      }
    }
   ```

  - 服务在应用级(app.module.ts)中声明，组件只是把主模块中的实例对象引用过来
  
  ```js
    import {Component, OnInit, Injectable} from '@anuglar/core';

    @Component({
      selector:'app-login',
      template:`
        <div>
          <input #usernameReftype="text">
          <input #passwordReftype="password">
          <button(click)="onClick(usernameRef.value,passwordRef.value)">Login</button>
        </div>
      `,
      styles: []
    })

    export class LoginComponent implements OnInit{
      constructor(@Injectable('auth') private service){}
      ngOnInit(){}

      onClick(username, password){
      // 调用service方法
      console.log(`
        auth result is: ${this.service.loginWithCredentials(username, password)}
      `)
      }
    }

  ```


下面使用一个简单的例子展示**依赖注入**的过程:

- `product.service.ts`构建服务，实现数据共享
 
  ```js
    import { Injectable } from '@angular/core';

    @Injectable()  //技巧: 将`@Injectable()`装饰器直接添加到服务中，在其他组件中引用该服务时，就不用再添加`@Injectbale()`装饰器了
    export class ProductService {

      private products: Product[] = [
        new Product(1, "第1个商品", 1.99, 2.5, "这是snoopy.Q写的一段话！", ["电子设备"]),
        new Product(2, "第2个商品", 2.99, 4.5, "这是snoopy.Q写的一段话！", ["电子设备"]),
        new Product(3, "第3个商品", 3.99, 3.5, "这是snoopy.Q写的一段话！", ["电子设备"]),
        new Product(4, "第4个商品", 4.99, 1.5, "这是snoopy.Q写的一段话！", ["电子设备"]),
        new Product(5, "第5个商品", 5.99, 3.5, "这是snoopy.Q写的一段话！", ["电子设备"]),
        new Product(6, "第6个商品", 6.99, 4.5, "这是snoopy.Q写的一段话！", ["电子设备"])
      ];

      constructor() { }

      getProducts(){
        return this.products;
      }

      getProduct(id: number): Product {
        return this.products.find((product) => product.id ==id);
      }

    }
    export class Product {
      constructor(
        public id: number,
        public title: string,
        public price: number,
        public rating: number,
        public desc: string,
        public categories: Array<string>
      ){}
    }
  ```

- 在`product.component.ts`组件中，使用`ProductService`服务

  ```js
    import { Component, OnInit } from '@angular/core';
    import {Product, ProductService} from "../shared/product.service";  // 1.导入服务

    @Component({
      selector: 'app-product',
      templateUrl: './product.component.html',
      styleUrls: ['./product.component.css'],
      providers: [ProductService]  //  2. 在当前组件中声明`ProductService`只可以在当前组件中使用该服务
    })
    export class ProductComponent implements OnInit {
      // 声明数组存储页面展示需要的数据
      private products: Product[];

      constructor(private productService: ProductService) { }  // 3. 注入`ProductService`服务

      ngOnInit() {  // 在组件被实例化后调用一次，用来初始化组件中的数据
        this.products = this.productService.getProducts();
      }

    }

  ```

- 也可在`app.module.ts`根模块中声明服务

  ```js
    import { BrowserModule } from '@angular/platform-browser';
    import { NgModule } from '@angular/core';
   
    import { AppComponent } from './app.component';
    import { ProductComponent } from './product/product.component';
    import { ProductService } from "./shared/product.service";

    @NgModule({
      declarations: [
        AppComponent,
        ProductDetailComponent
      ],
      imports: [BrowserModule],
      providers: [ProductService],  // 2. 在根模块中声明`ProductService`，所有组件都可以使用`ProductService`服务
      bootstrap: [AppComponent]
    })
    export class AppModule { }

  ```

- **说明**:
  
  > 在`@NgModule({})`或`@Component({})`的元数据(`Metadata`)中配置了`provider`的相关信息，
  > 
  > 是要告诉`Angular DI`系统，根据配置的provider信息，创建相应的依赖对象。
  > 
  > 而在`ProductComponent`组件类中，通过构造注入的方式告诉`Angular DI`系统，当前组件类需要的依赖对象类型是`ProductService`。


- 关于`@Injectable`和`@Component`

  + `@Injectable`是关键注解，`@Component`是关键字。

  + `@Injectable`表示该js文件所导出的类是服务，而服务可以通过注入来创建。

  + `@Component`表示该js导出的类是组件。

  + 服务的注入，是ng中用来分离控制器和业务逻辑的主要方式。


