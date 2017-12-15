# 管道
- 常见的管道
  ```typescript
      <p>{{birthday | date:'yyyy-MM-dd HH:mm:ss' | lowercase | uppercase}}</p>  // 日期，大写，小写
      <p>{{pi | number:'2.1-4'}}</p>  // 数字
      <p>{{pi | async}}</p>  // 处理异步流
  ```

- 自定义管道 
  > 通过命令行`ng g pipe pipe/multiple`，生成一个自定义管道
  **注意**: 自定义管道需要声明，即需要添加到模块`@NgModule`的`declarations`元数据中的。
  
  ```typescript
    // 一个简单的自定义管道
    import{ Pipe, PipeTransform } from  '@angular/core';
    @Pipe({
      name: 'multiple'  // 自定义管道操作符的名称
    })
    export class MutiplePipe implements PipeTransform {  
      transform(value: number, args?: number): any {
        if(!args) {
          args = 1;
        }
        return value * args;
      }
    }
    
    // 自定义管道的使用
    <p>自定义管道{{size | multiple: 2}}</p>
  ```
