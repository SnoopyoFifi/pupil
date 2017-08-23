# Arrows函数

- 当无参数或有多个参数时，就使用一个圆括号`()`代表参数部分；

```js
  let fifi = () => 'snoopy';
  let fifi = _ => 'fifi'; // 么有参数用`_`也是可以的

  let haveFun = (fifi, snoopy) => fifi + snoopy;
```

- 当代码块部分多于一条语句时，就要使用花括号`{}`，及`return`语句返回；

```js
  let snoopy = (n1, n2) => { return n1 + n2; }
```

- 由于花括号`{}`被解释为代码块，所以当直接返回一个对象时，必须在对象外加圆括号`()`

```js
  let getFifi =  sex => ({ sex: female, name: "Fifi" }) 
```

- 支持剩余参数和默认参数

```js
  let Fifi = (param1, paramn, ...rest) = {
    console.log(`%c {statements}`, `color: red;`)
  }
```

`注意`：

- 函数体内的`this`对象，为绑定定义时所在的对象，而不是使用时所在的对象
- 箭头函数不可以当做构造函数，即不可以使用`new`
- 不可以使用`arguments`对象，在函数体内不存在

## Set&Map数据结构

### Set

> `Set`类似于数组，但是成员唯一，没有重复的值；
> 本身为构造函数，用来生成`Set`数据结构；
> 可以接受一个数组作为参数，用于初始化

- `Set`实例的属性和方法

> `Set`实例属性

- Set.prototype.constructor：构造函数，默认就是Set函数。
- Set.prototype.size：返回Set实例的成员总数。

> `Set`实例方法

- add(value)：添加某个值，返回Set结构本身。
- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
- has(value)：返回一个布尔值，表示该值是否为Set的成员。
- clear()：清除所有成员，没有返回值。

### Map

## `for...of` 循环

> `for...in` 只能获得对象的键名， `for...of` 允许遍历获得键名及键值

```js
  var Snoopy = new Map();
```
