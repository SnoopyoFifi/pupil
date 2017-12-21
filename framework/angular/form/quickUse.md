# 快速使用

- 实现双向绑定

  > 在ng表单中，通过`ngModel`指令来实现双向绑定

  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      template: `
        <input type="text" [(ngModel)]="username">
        {{username}}
      `  
    })

    export class AppComponent {
      username = "snoopy"
    }
  ```

- 表单验证

  + 内置表单验证器有
    * `require` - 非空验证
    * `email`  - 设置表单值的格式为邮箱
    * `minlength` - 设置表单值的最小长度
    * `maxlength` - 设置表单值的最大长度
    * `pattern` - 设置表单值需要匹配pattern对应的模式
  
  + 必填验证
    * 通过`#userName="ngModel"`方式获取`ngModel`对象；
    * 然后通过`userName.valid`判断表单控件是否通过验证

  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      template: `
        <input 
          type="text" 
          required
          [(ngModel)]="username"
          #userName="ngModel">
        {{userName.valid}}
      `  
    })

    export class AppComponent {
      username = "snoopy"
    }
  ```

- 显示验证失败的错误信息
  + 通过`#userName="ngModel"`方式获取`ngModel`对象；
  + 通过`ngModel`对象的`errors`属性，来获取对应验证规则的验证状态。
  

  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      template: `
        <input 
          type="text" 
          required
          minlength="3"
          [(ngModel)]="username"
          #userName="ngModel">
        <hr>
        <div *ngIf="userName.errors?.required">请您输入用户名</div>
        <div *ngIf="userName.errors?.minlength">
          用户名的长度必须大于{{useName.errors?.minlength.requiredLenght}},
          当前的长度为{{userName.errors?.minlength.actualLength}}
        </div>
      `  
    })

    export class AppComponent {
      username = "snoopy"
    }
  ```

- 创建表单，并获取表单提交的值
  + 使用`form`表单必须给表单控件添加对应的`name`属性。
  + 通过`#loginForm="ngForm"`的方式获取`ngForm`对象；
  + 通过`loginForm.value`来获取表单的值。

  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      template: `
        <form #loginForm="ngForm" (ngSubmit)="onSubmit(loginForm.value)">
          <input 
            type="text" 
            name="username"
            required
            minlength="3"
            [(ngModel)]="username"
            #userName="ngModel">
          <hr>
          <div *ngIf="userName.errors?.required">请您输入用户名</div>
          <div *ngIf="userName.errors?.minlength">
            用户名的长度必须大于{{useName.errors?.minlength.requiredLenght}},
            当前的长度为{{userName.errors?.minlength.actualLength}}
          </div>
          <button type="submit">提交</button>
          {{loginForm.value | json}}
        </form>
      `  
    })

    export class AppComponent {
      username = "snoopy"

      onSubmit(value){
        console.dir(value);
      }
    }
  ```

- `ngModelGroup`
  
  > `ngModelGroup`指令是ng表单中提供的另一特殊指令，可以对表单输入内容分组，方便在语义上区分不同性质的输入。

  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      template: `
        <form #loginForm="ngForm" (ngSubmit)="onSubmit(loginForm.value)">
          <fieldset ngModelGroup="user">
            <input 
              type="text" 
              name="username"
              required
              minlength="3"
              [(ngModel)]="username"
              #userName="ngModel">
            <hr>
            <div *ngIf="userName.errors?.required">请您输入用户名</div>
            <div *ngIf="userName.errors?.minlength">
              用户名的长度必须大于{{useName.errors?.minlength.requiredLenght}},
              当前的长度为{{userName.errors?.minlength.actualLength}}
            </div>
            <input type="password" ngModel name="password">
          </fieldset>
          <button type="submit">提交</button>
          {{loginForm.value | json}} // {"user": {"username": "snoopy", "password": "123"}}
        </form>
      `  
    })

    export class AppComponent {
      username = "snoopy";
      password = "123";

      onSubmit(value){
        console.dir(value);
      }
    }
  ```

- 表单添加验证状态样式
  
  > 验证通过则在表单控件上添加`ng-valid`类，
  > 
  > 若验证失败则在表单上添加`ng-invalid`类。
  
  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      styles: [`
        input.ng-invalid {
          border: 3px solid hotpink;
        }

        input.ng-valid {
          border: 3px solid yellowgreen;
        }
      `]
      template: `
        <form #loginForm="ngForm" (ngSubmit)="onSubmit(loginForm.value)">
          <fieldset ngModelGroup="user">
            <input 
              type="text" 
              name="username"
              required
              minlength="3"
              [(ngModel)]="username"
              #userName="ngModel">
            <hr>
            <div *ngIf="userName.errors?.required">请您输入用户名</div>
            <div *ngIf="userName.errors?.minlength">
              用户名的长度必须大于{{useName.errors?.minlength.requiredLenght}},
              当前的长度为{{userName.errors?.minlength.actualLength}}
            </div>
            <input type="password" required ngModel name="password">
          </fieldset>
          <button type="submit">提交</button>
          {{loginForm.value | json}} // {"user": {"username": "snoopy", "password": "123"}}
        </form>
      `  
    })

    export class AppComponent {
      username = "snoopy";
      password = "123";

      onSubmit(value){
        console.dir(value);
      }
    }
  ```

- 表单控件的状态
  > 通过`#username="ngModel"`方式获取`ngModel`对象，进而获取控件的状态信息。
  
  + `valid` - 有效
  + `invalid` - 无效
  + `pristine` - 值未改变
  + `dirty` - 值已改变
  + `touched` - 已被访问过
  + `untouched` - 未被访问过

  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      styles: [`
        input.ng-invalid {
          border: 3px solid hotpink;
        }

        input.ng-valid {
          border: 3px solid yellowgreen;
        }
      `]
      template: `
        <form #loginForm="ngForm" (ngSubmit)="onSubmit(loginForm.value)">
          <fieldset ngModelGroup="user">
            <input 
              type="text" 
              name="username"
              required
              minlength="3"
              [(ngModel)]="username"
              #userName="ngModel">
            <hr>
            
            <p>Name控件的valid状态：{{userName.valid}} - 表示控件有效</p>
            <p>Name控件的invalid状态：{{userName.invalid}} - 表示控件无效</p>
            <p>Name控件的pristine状态：{{userName.pristine}} - 表示控件值未改变</p>
            <p>Name控件的dirty状态：{{userName.dirty}} - 表示控件值已改变</p>
            <p>Name控件的touched状态：{{userName.touched}} - 表示控件已被访问过</p>
            <p>Name控件的untouched状态：{{userName.untouched}} - 表示控件未被访问过</p>

            <div *ngIf="userName.errors?.required">请您输入用户名</div>
            <div *ngIf="userName.errors?.minlength">
              用户名的长度必须大于{{useName.errors?.minlength.requiredLenght}},
              当前的长度为{{userName.errors?.minlength.actualLength}}
            </div>
            <input type="password" required ngModel name="password">
          </fieldset>
          <button type="submit">提交</button>
          {{loginForm.value | json}} // {"user": {"username": "snoopy", "password": "123"}}
        </form>
      `  
    })

    export class AppComponent {
      username = "snoopy";
      password = "123";

      onSubmit(value){
        console.dir(value);
      }
    } 
  ```

- 使用单选控件

  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      template: `
        <form #loginForm="ngForm">
          <div *ngFor="let version of versions;">
            <input 
              type="radio"
              name="version"
              [attr.id]="version"
              ngModel
              required
              [value]="version"
            >
            <label [attr.for]="version">{{version}}</label>
          </div>
          <hr>
          {{loginForm.value | json}}
        </form>
      `  
    })

    export class AppComponent{
      versions = ['1.x', '2.x', '3.x', '4.x']
    }
  ```

- 使用多选控件并添加必填验证

  ```js
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      styles: [`
        select.ng-invalid + label:after {
          content: '<--请选择版本！-->'
        }
      `],
      template: `
        <form #loginForm="ngForm">
          <select name="version" [ngModel]="version" required>
            <option 
              *ngFor="let version of versions;"
              [value] = "version">
              {{version}}
            </option>
          </select>
          <label></label>
          <hr>
          {{loginForm.value | json}}
        </form>
      `  
    })

    export class AppComponent{
      versions = ['1.x', '2.x', '3.x', '4.x']
    }
  ```