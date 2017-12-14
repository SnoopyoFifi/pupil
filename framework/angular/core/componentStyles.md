# 组件样式

- 使用`styles`或`style`属性
  > 在设置组件元数据时，通过`styles`或`styleUrls`属性，来设置组件的内联样式和外联样式。
  ```typescript
    import { Component, OnInit } from '@angular/core';
    @Component({
        selector: 'app-product',
        templateUrl: './product.component.html',
        //styleUrl: './product.component.css',
        styles: [`
          :host { background-color: hotpink; }
          :host(.active) {
            border-width: 3px;
          }
          :host-context(.theme-light) h2 {
            background-color: #eef;
          }

          .desc {font-size: 14px;}
        `]
    })

    export class ProductComponent implements OnInit {
      ngOnInit(){}
    }
  ```

  **说明**:
    - `:host`选择器，表示宿主元素，即`AppComponent`组件模板中的

