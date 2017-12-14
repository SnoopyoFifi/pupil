# 生命周期钩子

- 什么是钩子
  > 钩子(`hook`)就是一些具有既定生命周期的框架工具，在生命周期的各个阶段预留给用户执行一些特定操作的口子，这其实是一种面向切面的编程。

  + [钩子函数的运行机理](https://juejin.im/post/5a1b5324f265da43305e2dfa)

- 生命周期的顺序

  | 钩子                        | 目的和时机                                    |
  | ------------------------- | ---------------------------------------- |
  | `ngOnChanges()`           | 当Angular（重新）设置数据绑定输入属性时响应。 该方法接受当前和上一属性值的`SimpleChanges`对象当被绑定的输入属性的值发生变化时调用，首次调用一定会发生在`ngOnInit()`之前。 |
  | `ngOnInit()`              | 在Angular第一次显示数据绑定和设置指令/组件的输入属性之后，初始化指令/组件。在第一轮`ngOnChanges()`完成之后调用，只调用**一次**。 |
  | `ngDoCheck()`             | 检测，并在发生Angular无法或不愿意自己检测的变化时作出反应。在每个Angular变更检测周期中调用，`ngOnChanges()`和`ngOnInit()`之后。 |
  | `ngAfterContentInit()`    | 当把内容投影进组件之后调用。第一次`ngDoCheck()`之后调用，只调用一次。**只适用于组件**。 |
  | `ngAfterContentChecked()` | 每次完成被投影组件内容的变更检测之后调用。`ngAfterContentInit()`和每次`ngDoCheck()`之后调用**只适合组件**。 |
  | `ngAfterViewInit()`       | 初始化完组件视图及其子视图之后调用。第一次`ngAfterContentChecked()`之后调用，只调用一次。**只适合组件**。 |
  | `ngAfterViewChecked()`    | 每次做完组件视图和子视图的变更检测之后调用。`ngAfterViewInit()`和每次`ngAfterContentChecked()`之后调用。**只适合组件**。 |
  | `ngOnDestroy`             | 当Angular每次销毁指令/组件之前调用并清扫。 在这儿反订阅可观察对象和分离事件处理器，以防内存泄漏。在Angular销毁指令/组件之前调用。 |

- 组件生命周期钩子
  + 指令和组件的实例有一个生命周期： 新建、更新、销毁。
  + 通过实现一个或多个`Angular core`库里定义的生命周期钩子接口，开发者可以介入周期中的各个阶段。
  + 每个接口都有唯一一个钩子方法，钩子命名由接口名加上`ng`前缀构成。
  + 如：`OnInit`接口的钩子方法叫做`ngOnInit`，`Angular`在创建组件后会立即调用它。
  + 没有指令或组件会实现所有这些接口，并且有些钩子只对组件有意义。
  + 只有在指令、组件中定义过的那些钩子方法才会被`Angular`调用。

  ```js
  	export class PeekABoo implements OnInit {
  		constructor(private logger: LoggerService){
  			ngOnInit() { this.logIt(`OnInit`); }
  			logIt(msg: string) {
  				this.logger.log(`#${nextId++} ${msg}`);
  			}
  		}
  	}
  ```

## 组件间的通讯内容简介

## 输入属性

## 输出属性

## 中间人模式

## OnChanges钩子

## 变更检测和DoCheck钩子

## view钩子

## ngContent指令

## 最后的钩子