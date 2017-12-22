# Templates-driven Forms

> 模板式表单: 
> 
> 表单的数据模型是通过组件模板中的相关指令来定义的。
> 
> 因为使用这种方式定义表单的数据模型时，我们会受限于`HTML`的语法，
> 
> 所以，模板驱动方式只适合用于一些简单的场景。


NgForm NgModel NgModelGroup

- `NgForm`用来代表整个表单，在ng中会自动地添加到form标签上。

- `NgForm`隐式的创建一个`FormGroup`类，用来代表表单的数据模型，并存储表单的数据。

- 标有`NgForm`指令的`html`标签会自动发现其标有`NgModel`的子元素，并将该子元素的值添加到表单的数据模型中。

- `NgForm`指令可以在`form`标签之外使用；如果不想使用ng处理表单，在`form` 标签上添加`ngNoForm`指令即可。

- `NgForm`指令可以被一个模板本地变量引用，以便在模板中访问`NgForm`对象的实例。

- `NgForm`指令会拦截标准的表单提交事件，阻止表单自动提交，使用自定义`ngSubmit`事件提交表单。


`NgModel`除了用于双向数据绑定外，还用于标记一个html元素成为表单数据模型的一部分。
`NgModel`指令代表表单中的一个字段，同时，会隐式的创建一个`FormControl`实例来代表字段的数据模型，并用`FormControl`类型的对象来存储字段的值。
在标记了`NgForm`指令的表单内部使用`NgModel`指令时，不需要加上方括号`[]`，但是需要给添加了`ngModel`指令的元素添加一个`name`属性。