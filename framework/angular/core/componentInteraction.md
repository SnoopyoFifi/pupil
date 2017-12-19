# 组件交互

- 通过输入型绑定把数据从父组件传到子组件
	- 输入型属性通常带`@Input装饰器`。
	- 父组件`HeroParentComponent`把子组件的`HeroChildComponent`放到`*ngFor`循环器中，把自己的`master`字符串属性绑定到子组件的`master`别名上，并把每个循环的`hero`实例绑定到子组件的`hero`属性。
	```js
		// HeroChildComponent
		import { Component, Input } from '@angular/core';
		import { Hero } from './hero';

		@Component({
			selector: 'app-hero-child',
			template: `
				<h3>{{hero.name}} says:</h3>
				<p>I, {{hero.name}}, am at your service, {{masterName}}.</p>
			`
		})

		export class HeroChildComponent {
			@Input() hero: Hero;
			@Input('master') masterName: string;  // 为子组件`masterName`属性指定一个别名`master`
		}

		// HeroParentComponent
		import { Component } from '@angular/core';
		import { HEROES } from './hero';
		@Component({
			selector: 'app-hero-parent',
			template: `
				<h2>{{master}} controls {{heroes.length}} heroes</h2> 
				<app-hero-child *ngFor = "let hero of heroes"
					[hero] = "hero"
					[master] = "master">
				</app-hero-child>
			`
		})

		export class HeroParentComponent {
			heroes = HEROES;
			master = 'Master';
		}
	```

- 通过`setter`截听输入属性值的变化
	
## 组件间的通讯内容简介
- 父组件通过属性绑定到子组件，子组件通过事件传递参数到父组件
	```typescript
		// 父组件模板
		<li *ngFor="let item of dataSet; let i = index">
			<span>{{item.name}}</span>
			<app-child [names] = "item" (foo)="bar($event)"></app-child>
		</li>

		// 父组件ts
		import { Component, OnInit } from '@angular/core';
		@Component({
			selector: 'app-parent';
			templateUrl: './parent.component.html',
			styleUrls: ['./parent.component.scss']
		})
		export class ParentComponent implements OnInit {
			constructor(){}
			ngOnInit(){}

			dataSet = [
				{"id": 0, "name": "snoopy"},
				{"id": 1, "name": "fifi"},
				{"id": 2, "name": "jack"},
				{"id": 3, "name": "rose"},
			]

			bar(event: any) {
				console.log(event);
			}
		}

		// 子组件模板
		<input type="button" value="{{names.name}}" (click)="todo($event)">

		// 子组件ts
		import { Component, OnInit, Input, Output, EventEmitter } from '@angular/core';
		@Component({
			selector: 'app-child',
			templateUrl: './child.component.html',
			styleUrls: ['./child.component.scss']
		})
		export class ChildComponent implements OnInit {
			@Input() names: any = {}
			@Output() foo = new EventEmitter<string>();

			todo(event:any) {
				this.foo.emit(this.names.id); // 触发指定事件，子组件通过`emit`将要传递出去的参数传递给父组件，父组件中就可以获取到
			}

			constructor(){}
			ngOnInit(){}
		}
	```

	- `EventEmitter类`: 
		- `EventEmitter类`是`node`中事件的基础，实现了事件模型需要的接口，包括`addListener`、`removeListener`、`emit`及其他工具方法。同原生js事件类似，采用了观察者的方式，使用内部`_events`列表类纪录注册的事件处理器。

		- `EventEmitter` 的核心是事件监听器on与事件发射emit。
		
		- 使用步骤
			+ 调用`events`模块，获取`events.EventEmitter`对象	

			+ `EventEmitter.on(event, listener)`: 为事件注册一个监听参数，(event: 字符串，事件名, listener：回调函数)

			+ `EventEmitter.emit(event, [arg1], [arg2], [...])`: 触发指定事件，(event: 字符串，事件名,  可选参数: 按顺序传入回调函数的参数, 返回值: 该事件是否有监听)

		- EventEmitter.prototype生成的函数包括:

			```
				on = addListener ( type, callback )           // 注册函数，类似原生addListener的机制
				once ( type, callback )                       // 通过fired（bool类型），注册函数只运行一次
				removeListener ( type, callback )             // 取消注册，类似原生removeListener
				removeAllListeners ( type )                   // 遍历_events，循环调用removeListener
				emit ( type )                                 // 遍历_events,  循环调用_events注册的函数
				setMaxListeners ( n )                         // 设置每个_events属性最大注册函数上限
				listeners ( type )                            // 提取_events中注册的函数        
			 	EventEmitter.listenerCount ( emitter, type )  // 获取注册的函数最大数量
			```


- 父组件通过<b>局部变量</b>获取子组件的引用
	
	> 可以使用局部变量获取到子组件的实例引用，模板局部变量的定义使用`#name`的方式。
	
	```typescript
		// 父组件模板
		<li *ngFor="let item of dataSet">
			// 使用模板局部变量调用子类的方法
			<app-child [names]="item" (click)="father.childFn()" #father></app-child>
		</li>
		// 父组件ts
		dataSet = [
			{"id": 0, "name": "snoopy"},
			{"id": 1, "name": "fifi"},
			{"id": 2, "name": "jack"},
			{"id": 3, "name": "rose"},
		]

		
		// 子组件模板
		<span>{{names.name}}</span> 
		// 子组件ts
		@Input() names: any = {}
		childFn() {
			console.log("我是子类的方法");
		}
	```

- 父组件使用`@ViewChild`获取子组件的引用
	
	> 同模板局部变量，都是在父组件中调用子组件的方法
	
	```typescript
		// 父组件模板
		<li *ngFor="let item of dataSet">
			<app-child [names]="itme" (click)="father()"></app-child>
		</li>

		// 父组件ts
		dataSet = [
			{"id": 0, "name": "snoopy"},
			{"id": 1, "name": "fifi"},
			{"id": 2, "name": "jack"},
			{"id": 3, "name": "rose"},
		]
		@ViewChild(ChildComponent) child: ChildComponent;  // @ViewChild(子组件名称) 
		father(){
			this.child.childFn();	 // 调用子组件的方法
		}
	```

- 两个不相关联的组件使用<b>中间人模式</b>交互
	> 毫无关联的组件1与组件2，实现从组件1点击按钮传递参数到组件2中，使用中间人(可以是根组件)模式
	
	```typescript
		// com1模板
		<div class="com1">
			<p>我是组件1</p>
			<input type="button" value="com1按钮" (click)="com1Fn($event)"/>
		</div>
		// com1 ts
		@Output() outcom1Fn = new EventEmitter<string>();
		com1Fn(){
			this.outcom1Fn.emit("我是组件1传过来的");
		}

		// 根组件模板
		<app-com1 (outcom1Fn)="appFn($event)"></app-com1>
		<app-com2 [com2]="com1Tocom2"></app-com2>
		// 根组件ts
		private com1Tocom2;
		appFn(event:any){
			console.log(event);
			this.com1Tocom2 = event;
		}

		// com2模板
		<div class="com2">
			<p>我是组件2</p>
			<p>组件1传过来的内容是: {{com2}}</p>
		</div>
		// com2 ts
		@Input() com2: string = "";

	```

- 创建一个<b>服务</b>注入到组件中
	```typescript
		// 实现一个可观察的服务DataService
		import { Injectable } from '@angular/core';
		import { Subject } from 'rxjs/Subject';
		import { Observable } from 'rxjs/Observable';

		@Injectable()
		export class DataService {

			private data: any;
			private subject: Subject<any> = new Subject<any>();

			setData(data: any):void {
				this.data = data;
				this.subject.next(data);
			}

			getData(): Observable<any> {
				return this.subject.asObservable();
			}
		}

		// 使用服务
		import { Component, OnInit } from '@angular/core';
		import { DataService } from './shared/DataService';
		@Component({
			moduleId: module.id,
			selector: '<my-component></my-component>',
			templateUrl: 'my.component.html',
			providers: [DataService]
		})
		export class MyComponent implements OnInit {
			constructor(private dataService: DataService){}
			ngOnInit(){
				this.dataService.getData().subscribe(data=>console.log(data));
			}
		}

		
	```

- 直接把父组件当做服务注入到子组件中
	```typescript
		// 父组件ts
		import { Component, OnInit } from '@angular/core';
		@Component({
			selector: 'app-father1',
			templateUrl: './father.component.html',
			styleUrls: ['./father1.component.css']	
		})
		export class Father1Component implements OnInit {
			constructor() {}
			public name: string = "我是父组件的名称";
			public dataSet: Array<any> = [
				{"id": 0, "name": "snoopy"},
				{"id": 1, "name": "fifi"},
				{"id": 2, "name": "jack"},
				{"id": 3, "name": "rose"},
			]
			ngOnit(){}
		}

		// 子组件ts
		import { Component, OnInit } from '@angular/core';
		import { Father1Component } from 'app/father1/father1.component';
		@Component({
			selector: 'app-child1',
			templateUrl: './child.component.html',
			styleUrls: ['./child1.component.css']	
		})
		export class ChildComponent implements OnInit {
			constructor(private father1: Father1Component){}
			ngOnInit(){}
	
		}

		// 子组件模板
		<p>{{father1.name}}</p>
		<ul>
			<li *ngFor="let item of father1.dataSet"></li>
		</ul>
	```

- 补充
	> 在父组件传递数据到子组件中，子组件接受数据，可以对其接收的数据进行处理后再显示在页面中，这里就要用到`set`与`get`方法
	
	```typescript
		// 父组件ts
		data:string = "parent";
		// 父组件模板
		<app-child [input]="data"></app-child>

		// 子组件ts
		export class ChildComponent implements OnInit {
			_input: string;
			@Input()
			public set input(v: string) {
				this._input = v.toUpperCase(); //转换大写并输出
				console.log(v);
			}

			public get input(): string {
				return this._input;
			}

			constructor(){}
			ngOnInit(){}
		}

		// 子组件模板
		<span>I am from {{input}}</span>
	```
