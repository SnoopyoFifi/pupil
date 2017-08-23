# 数据结构新增

## Set&Map数据结构


### Set
- 什么是`Set`

> `Set`类似于数组，但是成员唯一，没有重复的值；
> 本身为构造函数，用来生成`Set`数据结构；
> 可以接受一个数组作为参数，用于初始化。

- `Set`数据结构不会添加重复的值

```js
  var s = new Set();
  [2,3,4,5,5,4,3,3].map(x => s.add(x))
  for (i of s) {
    console.log(i)
  }
```


- `Set`实例的属性和方法

   - Set.prototype.constructor：构造函数，默认就是Set函数。
   - Set.prototype.size：返回Set实例的成员总数。

   - add(value)：添加某个值，返回Set结构本身。
   - delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
   - has(value)：返回一个布尔值，表示该值是否为Set的成员。
   - clear()：清除所有成员，没有返回值。

- 将`Set`实例转为数组

```js
  const items = new Set([1,2,3]);
  const array = Array.from(itmes);
```

- 利用`Set`将数组去重

```js
  function dedupe(array){
    return Array.from(new Set(array));
  }
```

### Map

- 什么是`Map`

> `Map`类似于对象，是一个键值对的集合；
> "键"的范围可以是字符串，甚至可以是对象

```js
  var m = new Map();

  m.set("snoopy", "perfect")
  m.set(1314, 520 )
  m.set(undefined, 'never')
  m.set(function(){console.log("hello")}, "hello snoopy")
  
  m.has(undefined) // true
  m.delete(undefined) 
  m.has(undefined) // false
```

## `for...of` 循环

> `for...in` 只能获得对象的键名， `for...of` 允许遍历获得键名及键值

```js
  var arr = ["s", "n", "o", "o", "p", "y"];
  for(a of arr){
    console.log(a)
  }

  var sSnoopy = new Set(snoopy);
  sSnoopy.add()

  var mSnoopy = new Map(snoopy);
  for(var m of msnoopy){
    console.log(m);
  }
  

```
