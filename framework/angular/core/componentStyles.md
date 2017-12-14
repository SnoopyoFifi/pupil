# 组件样式
- 使用`styles`或`style`属性
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
    - `:host`选择器，表示宿主元素，即`ProductComponent`组件模板中的`app-product`元素。
    - 在设置组件元数据时，通过`styles`或`styleUrls`属性，来设置组件的内联样式和外联样式。

- 使用`ngClass`指令
  ```typescript
    @Component({
      selector: 'app-simple-form',
      template: `
        <div>
          {{message}}
          <input #myInput type="text"
            [(ngModel)]="message"
            [ngClass]="{mousedown: isMousedown}"
            (mousedown)="isMousedown = true"
            (mouseup)="isMousedown = false"
            (mouseleave)="isMousedown = false"
          >

          <button (click)="updata.emit({text:message})">更新</button>
        </div>
      `,
      styles: [`
        :host {margin: 10px;}
        .mousedown {border:2px solic hotpink;}
        input:focus {font-weight: bold; outline: none;}
      `]
    })

    <!-- 使用布尔值 -->
    <div [ngClass]="{bordered: false}">始终没有边框</div>
    <div [ngClass]="{bordered: true}">始终有边框</div>

    <!-- 使用组件实例的属性 -->
    <div [ngClass]="{bordered: isBordered}">
      {{ isBordered ? "ON" : "OFF" }}
    </div>

    <!-- 样式包含'-' -->
    <div [ngClass]="{'border-box': false}">类名包含"-"必须用单引号</div>

    <!-- 使用样式列表 -->
    <div class="base" [ngClass]="['blue', 'round']">将会有绿色的背景色和圆角属性</div>

  ```

  **说明**: `ngClass`指令接收一个对象字面量，对象的键是css的类名，值是布尔值类型，表示是否应用该样式。

- 使用`ngStyle`指令
  ```html
      <div [ngStyle]="{color: 'white', 'background-color': blue">白色字体，红色背景</div>

      <!-- 设置元素背景 -->
      <div [style.background-color="'yellow'"]]></div>
      
      <!-- 设置字体大小 px | em | % -->
      <div>
         <span [ngStyle]="{color: 'red'}" [style.font-size.px]="fontSize"></span>
      </div>
  ```

  **说明**: `ngStyle`要求的参数是一个js对象，`color` 是一个有效的 `key`，而 `background-color` 不是一个有效的 `key` ，需要加''。

- 引入UI框架的样式表(`bootstrap`)
  ```json
    {
       "apps": [
        {
          "styles": [
            "styles.css",
            "../node_modules/bootstrap/dist/css/bootstrap.css"
          ],
          "scripts": [
            "../node_modules/jquery/dist/jquery.js",
            "../node_modules/bootstrap/dist/js/bootstrap.js"
          ]
        }
      ]
    }
   
  ```
  
  **说明**:
    - 使用命令行`npm i bootstrap --save`安装`bootstrap`模块包；
    - 修改`angular-cli`配置文件(`.angular-cli.json`)，如上。


- 使用`scss`预编译
  - 生成一个使用scss预编译的`angular`项目，
    - 使用命令行: `ng new myProject --style=scss`
    
    - 手动安装`node-sass`: `npm i node-sass --save-dev`

  - 将当前项目更改为使用`scss`预编译
    - 安装所需sass模块包: `npm i node-sass --save-dev`

    - 修改`angular-cli`配置文件(`.angular-cli.json`)
      ```
        // 修改defaults标签
        "defaults": {
          "styleExt": "sass",
        }
      
        // 修改styles标签
        "styles": [
          "style.scss"
        ]
      ```

  **说明**: 使用scss预编译，不支持内置在组件中的`styles`，主要在组件中使用`styleUrl`属性引用外部`scss`文件