# React
[React入门实例教程](http://www.ruanyifeng.com/blog/2015/03/react.html)
* `ReactDOM.render()`
  - `ReactDOM.render()` 是 `React` 的最基本方法，用于将模板转为 `HTML` 语言，并插入指定的 `DOM` 节点。
* `JSX语法`
  - `HTML`语言直接写在`Js`语言中，不加任何引号，允许`HTML`与`Js`的混写。
  - 基本语法规则：遇到`HTML`标签(以`<`开头)，就用`HTML`规则解析；遇到代码块(以`{`开头)，就用`Js`规则解析。
  - `JSX`允许直接在模板中插入`Js`变量。如果该变量是一个数组，则会展开这个数组的所有成员。
* 组件
  - `React`允许将代码封装成组件(component)，然后像插入普通`HTML`标签一样，在网页中插入这个组件。
  - `React.creatClass`方法用于生成一个组件类。下面代码中，`HelloMessage`就是一个组件类。模板插入<HelloMessage/>时，会自动生成`HelloMessage`的一个实例("组件"一般都是指组件类的实例)。所有的组件类都必须有自己的`render`方法，用于输出组件。
  - 注意，组件类的第一个字母必须大写，否则报错；组件类只能包含一个顶层标签，否则也会报错。
  - 组件的用法跟原生的`HTML`标签完全一致，可以任意加入属性。组件的属性可以在组件类的`this.props`对象上获取。
  - 添加组件属性，`class`属性需要写成`className`，`for`属性需要写成`htmlFor`

    ```
      var HelloMessage = React.createClass({
        render: function(){
          return <h1>Hello {this.props.name}</h1>
        }  
      })

      ReactDOM.render(
        <HelloMessage name="John"/>,
        document.getElementById('example')
      )
    ```

* `this.props.children`
  - `this.props`对象的属性与组件的属性一一对应，但是，`this.props.children`属性。它表示组件的所有子节点。
  - `this.props.children`的值有三种可能：
    + 如果当前没有子节点，就是`undefined`；
    + 如果有一个子节点，数据类型是`object`；
    + 如果有多个子节点，数据类型是`array`.
  - `Reach`提供一个工具方法`React.Children`来处理`this.props.children`。可以利用`React.Children.map`来遍历子节点。
* PropTypes
  - 组件的属性可以接受任意值，组件类的`PropTypes`属性，就是用来验证组件实例的属性是否符合要求的。
  - 下面代码中，`PorpTypes`属性指出`title`属性是必须的，而且它的值必须是字符串。当设置`title`属性值为一个数值时，控制台就会显示一行错误信息。
    ```
      var MyTitle = React.createClass({
        propTypes: {
          title: React.PropTypes.string.isRequired,
        },
        render: function(){
          return <h1> {this.props.title} </h1>;
        }
      })

      var data = 123;
      ReactDOM.render(
        <MyTitle title={data}/>
        document.body
      )
    ```
  
  - `getDefaultProps`方法用以设置组件属性的默认值。
    ```
      var MyTitle = React.createClass({
        getDefaultProps: function(){
          return {
            title: 'Hello World'
          };
        },
        render: function(){
          return <h1> {this.props.title} </h1>;
        }
      });

      ReactDOM.render(
        <MyTitle/>,
        document.body
      )
    ```

* 获取真实的DOM节点

  - 组件并不是真实的`DOM`节点，而是存在于内存之中的一种数据结构，叫做虚拟DOM(`virtual DOM`)。只有当它插入文档以后，才会变成真实的`DOM`。
  - 根据`React`的设计，所有的`DOM`变动，都先在虚拟`DOM`上发生，然后再将实际发生变动的部分，反映在真实`DOM`上，这种算法叫做`DOM diff`，可以极大提高网页的性能表现。
  - `ref`属性用来获取真实`DOM`节点
    ```
      var MyComponent = React.createClass({
        handleClick: function(){
          this.refs.myTextInput.focus();
        },
        render: function(){
          return (
            <div>
              <input type="text" ref="myTextInput"/>
              <input type="button" value="Focus the text input" onClick={this.handleClick}>
            </div>
          )
        }
      });

      ReactDOM.render(
        <MyComponent/>,
        document.getElementById('example')
      )
    ```
  
  - `this.refs.[refName]`属性获取的是真实`DOM`，所以必须等到虚拟`DOM`插入文档以后，才能使用这个属性，否则会报错。上面代码通过`Click`事件的回调函数，确保了只有等到真实`DOM`发生`Click`事件之后，才会读取`this.refs.[refName]`属性。
  - `React`组件支持很多事件，如`Click`、`KeyDown`、`Copy`、`Scroll`等

* `this.state`
  - 组件免不了要与用户互动，`React`的一大创新，就是讲组件看成一个状态机，一开始就有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染`UI`。

  
