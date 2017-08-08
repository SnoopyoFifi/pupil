# API

## `classList` & `cssText`
### `classList`

> 用于对`DOM`元素的`css类`进行增、删、改操作

> 包含的方法有：
```js
{
  length: {number}, /* # of class on this element */
  add: function() { [native code] },  // 增加某个类
  contains: function() { [native code] }, // 检查是否包含某个类
  item: function() { [native code] }, /* by index */
  remove: function() { [native code] },  // 删除某个类
  toggle: function() { [native code] }  // 切换类样式
}
```


### `cssText`

> 用于批量操作元素的样式

```js
  var head = document.getElementById("head");
  head.style.cssText = "width:200px;height:70px;display:block";
```

> 注意：

- 优点： 当批量操作样式时，`cssText`只需要一次重绘操作，提高了页面渲染性能；
- 缺点： 使用它会覆盖之前的样式。

> 可以考虑使用叠加的方式以保留原有的样式：

```js
  function setStyle(el, strCss){
    var sty = el.style;
    sty.cssText = sty.cssText + strCss;
  }


  // 兼容ie6-8 （cssText返回值少了分号 ）
  
  function setStyle(el, strCss){
    function endsWith(str, suffix){
      var l = str.length-suffix.length;
      return l >= 0 && str.indexOf(suffix, l) == 1;
    }
    var sty = el.style,
        cssText = sty.cssText;
    if(!endWith(cssText, ';')){
      cssText += ';';
    }
    sty.cssText = cssText + strCss;
  }
```


## 给操作`DOM`起别名

```js
  document.getElementById
  document.getElementsByClass
  document.getElementsByName
  document.getElementsByTagName

  document.querySelector
  document.querySelectorAll
```

> 给document.querySelectorAll取别名

```js
  var $ = document.querySelectorAll;
  $("body")
  // 报错
```

> 报错的原因是 `querySelectorAll` 所需的执行上下文必需是 `document`，而我们赋值到 `$`` 调用后上下文变成了全局 `window`。

```js
  var $ = document.querySelectorAll.bind(document);
  $("body") 
  // 伪数组
```

> 给其他一系列DOM选择方法都加上简写：

```js
  var query = document.querySelector.bind(document);
  var queryAll = document.querySelectorAll.bind(document);
  var fromId = document.getElementById.bind(document);
  var fromClass = document.getElementsByClassName.bind(document);
  var fromTag = document.getElementsByTagName.bind(document);
```

> 注意：这些方法获取DOM返回的是单个Node节点，或是NodeList ，且NodeList是类数组对象，不可以直接使用数组的map、forEach等方法。

> 类数组正确使用数组的方法的姿势如下：

```js
  Array.prototype.map.call(document.querySelectorAll('button'), function(element, index){
    element.onclick = function(){}
  })


```

## 常用操作数组的方法

### `Array.forEach()`

> `.forEach()` 方法能够方便的遍历数组里的每个元素，可以在回调函数里对每个元素进行操作。
`.forEach()`方法没有返回值，不需要在回调函数里写`return`。

```js
  var animals = ['dog', 'cat', 'mouse'];
  
  animals.forEach(function(item){
      console.log(item);
  });
  
  array.forEach(callback(currentValue, index, array){
      //do something
  }, this)
```

### `Array.map()`

> `.map()` 方法能够遍历整个数组，然后返回一个新数组，这个新数组里的元素是经过了指定的回调函数处理过的。

> 如果想修改数组里的每个元素，然后将修改后的数组存入新的数组，那使用 `.map()` 方法最方便。

```js
  var numbers = [2, 4, 6, 8];
  
  var doubleNums = numbers.map(function(element) {
      return element * 2;
  });
  
  console.log('doubleNums: ', doubleNums)
```

### `Array.filter()`

> `.filter()` 方法能够 过滤掉数组中的某些元素，你可以在回调函数里设定条件，不符合条件的元素都会排除在外。

```js
  var scores = [3, 12, 5, 23, 19, 7];
  
  var topScores = scores.filter(function(item){
      if (item > 10){
          return true;
      } else {
          return false;
      }
  });
  
  console.log('topScores: ', topScores);
```

### `Array.indexOf()`

> `indexOf()` 能够告诉你 某个元素在数组中的位置，它返回的是索引值，如果数组里有重复的元素，它会返回第一个元素的位置。

```js
  var a = [2, 9, 9, 18];
  
  var i = a.indexOf(9);
  
  console.log('i: ', i);
  
  
  /*
  if (a.indexOf(7) === -1) {
    // 数组中没有这个元素
  }*/
```

### `Array.every()`

> .every() 方法的作用是用指定的回调函数去检查数组中的每个元素，如果对于每个元素，这个回调函数都返回true，则.every()返回true。否则，.every() 返回false。

> 如果想知道数组中的所有元素都是否符合某种条件，使用 .every() 最方便。

```js
  var ages = [23, 19, 32, 44];
  
  var olderThan18 = ages.every(function(element) {
      return element > 18;
  });
  
  console.log('olderThan18: ', olderThan18);
```

> 注意： 上面的这5个方法只是很多JavaScript方法中关于数组的最重要的几个，还有很多关于数组的方法、工具包(lodash and underscore)等都非常的有用。


## 事件委托

>  事件委托 应用场景：
 
- 给如所有`li`标签注册事件时，利用事件委托减少内存消耗
- 给如通过 AJAX 或者用户操作动态创建元素的事件绑定


实现把 `#list` 下的 `li`元素的事件

```js
  document.getElementById('co')
```
