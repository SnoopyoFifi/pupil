# 结构型指令

> 结构型指令就是通过添加和移除`DOM`元素改变`DOM`布局的指令。

- `*ngIf`
  > 条件成立时，添加DOM；条件不成立时，移除DOM
  ```html
    <div *ngIf="isShow"></div>
  ```

- `*ngFor`
  > 设定一个模板，然后循环一个数组的值，绑定到模板中，最后添加到DOM上。
  ```
    <div *ngFor="let item of itemList">
      <a>{{item.value}}</a>
    </div>

    <div *ngFor="let item of itemList; let i = index">  // 将当前索引index绑定到i上，传递到点击事件中。
      <a (click)="clickItem(i)">{{item.value}}</a> 
    </div>
    clickItem(index):void{
      conosle.log(this.itemList[index]);
    }

    // 优化，使用trackBy往组件中添加一个方法，告诉Angular应该追踪的值
    <div *ngFor="let item of itemList; let i = index; trackBy: trackByValue">
      <a (click)="clickItem(i)">{{item.value}}</a>
    </div>

    trackByValue(index: number, item: any):number {
      return item.value;
    }
  ```

- `ngSwitch`|`*ngSwitchCase`
  ```
    <div *ngFor="let item of itemList; let i = index; trackBy: trackByValue">
      <div [ngSwitch]="item.value" (click)="clickItem(i)">
        <a *ngSwitchCase="1">value is 1: {{item.value}}</a>
        <a *ngSwitchCase="2">value is 2: {{item.value}}</a>
      </div>
    </div>
  ```
