# Dependency Injection

> 依赖注入三个重要关键词: **使用者**、**服务(依赖对象)** 及 **注入器**

下面使用一个简单的例子展示**依赖注入**的过程:

- `product.service.ts`构建服务，实现数据共享
  ```typescript
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

  ```typescript
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

  ```typescript
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
  >在`@NgModule({})`或`@Component({})`的元数据(`Metadata`)中配置了`provider`的相关信息，是要告诉`Angular DI`系统，根据配置的provider信息，创建相应的依赖对象。
  而在`ProductComponent`组件类中，通过构造注入的方式告诉`Angular DI`系统，当前组件类需要的依赖对象类型是`ProductService`。

