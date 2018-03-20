# 数据类型扩展

## 数组的扩展

  - 扩展运算符`...`

  > 将一个数组变为一个参数序列，主要用于函数调用
  
  ```js
    function push(array, ...items) {
      array.push(...items)
    }

    function f(v, w, x, y, z) { }  
    var args = [0, 1];  
    f(-1, ...args, 2, ...[3]);  
  ```

  - 替代数组的`apply` 方法
    
    > 由于扩展运算符可以展开数组，所以不再需要`apply`方法，将数组转为函数的参数了。
  ```js
    // es5
    Math.max.apply(null, [14, 3, 77]);
    // es6
    Math.max(...[14, 3, 77]);
    // 等价于
    Math.max(14, 3, 77);
  ```


## 对象的扩展

- 属性初始化
  > 当对象的属性名和本地变量名相同时，可以直接用属性名称替换，

```js
  function createPerson(name, sex){
    return {
      name: name,
      age: age
    };
  }
  // 可替换为
  function createPerson(name, sex) {
    return {
      name,
      age
    };
  }
```

- 方法简写
  > 通过省略冒号与`function`关键字，改进了为对象字面量方法赋值的语法，

```js
  var person = {
    name: 'snoopy',
    fuck: function(){
      console.log(this.name);
    }
  }
  // 可替换为
  var person = {
    name: 'snoopy',
    fuck(){
      console.log(this.name);
    };
  }
```

- `Object.is()` 方法
  > 为了解决严格等(===)残留的问题(+0与-0相等，NaN与NaN不相等)，引入了`Object.is()` ，
  > `Object.is(x,y)`只有在x、y的类型和值都相等时，才返回`true`。

- `Object.asign()` 方法
  > 一个对象从另一个对象接收属性和方法，会使用混入的方式(浅复制，当属性值为对象时，仅复制其引用)，
  > 

```js
  // minx()函数 在supplier对象的属性上进行迭代，并讲这些属性复制到receiver对象
  function mixin(receiver, supplier) {
    Object.keys(supplier).forEach(function(key){
      receiver[key] = supplier[key];  
    })
    return receiver;
  }
  // 使用mixin()完成对象属性的复制
  function EventTarget(){}
  EvcentTarget.prototype = {
    constructor: EventTarget,
    emit: function(){},
    on: function(){}
  }
  var myObject = {},
  mixin(myObject, EventTarget.prototype);
  myObject.emit("somethingChanged");
  
```





