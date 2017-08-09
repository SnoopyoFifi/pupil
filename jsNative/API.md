# API

## `classList` & `cssText`
- `classList`

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


- `cssText`

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

## 操作数组的方法

## 常用的几个方法

- `Array.forEach()`

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

- `Array.map()`

> `.map()` 方法能够遍历整个数组，然后返回一个新数组，这个新数组里的元素是经过了指定的回调函数处理过的。

> 如果想修改数组里的每个元素，然后将修改后的数组存入新的数组，那使用 `.map()` 方法最方便。

```js
  var numbers = [2, 4, 6, 8];
  
  var doubleNums = numbers.map(function(element) {
      return element * 2;
  });
  
  console.log('doubleNums: ', doubleNums)
```

- `Array.filter()`

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

- `Array.indexOf()`

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

- `Array.every()`

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

### 方法的汇总

- 数组元素的添加

```js
  Array.push() // 将一个或多个新元素添加到数组结尾，并返回数组新长度。
  
  Array.unshift() // 将一个或多个新元素添加到数组开始，数组中的元素自动后移，返回数组新长度。
  
  Array.splice(插入位置, 删除元素个数, 新增的元素) 
  // 将一个或多个新元素插入到数组的指定位置，插入位置的元素自动后移，
```

- 数组元素的删除

```js
  Array.pop() // 移除最后一个元素并返回该元素值。
  
  Array.shift() // 移除最前一个元素返回该元素值，数组中元素自动前移。
  
  Array.splice(删除元素起始位置, 删除元素的个数) 
  // 删除从指定位置开始的指定数量的元素，数组形式返回所移除的元素
```


- 数组的截取和合并

```js
  Array.slice(start, [end]) // 以数组的形式返回数组的一部分。
  // 注意不包括`end`对应的元素，如果省略`end`将复制`start`之后所有元素，返回截取后的数组，原数组不变。
  
  Array.concat() // 将多个数组（字符串，或者是数组和字符串的混合）连接为一个数组，返回连接好的新数组。
```

- 数组的拷贝

```js
  Array.slice(0) // 返回数组的拷贝数组。
  
  Array.concat() // 返回数组的拷贝数组。
```

- 数组元素的排序

```js
  Array.reverse() // 反转元素（最前面的排到最后、最后面的排到最前），返回排序后的数组，改变了原数组。
 
  Array.sort() // 对数组元素排序，返回数组地址。
```

- 数组元素的字符串化

```js
  Array.join(连接符)  // 返回字符串，这个字符串将数组的每一个元素值连接在一起，中间用 连接符 隔开。

  // toLocaleString\toString\valueOf: 可以看作是join的特殊用法，不常用
```

## 操作字符串的方法

- 获取子串方法

```js
  String.charAt(index) // 用来获取指定位置的字符串。
  // `index` 为字符串的索引值，从0开始到`String.length-1`，若不在这个范围将返回一个空字符串。

  String.charCodeAt(index) // 可返回指定位置字符的`Unicode`编码。

 // `charCodeAt()`与`charAt()`类似，区别是前者返回指定位置的字符的编码，而后者返回的是字符子串。
 
 String.fromCharCode(num,...) // 可接受一个或多个Unicode值，然后返回一个字符串。
 // 另外该方法是`String `的静态方法，字符串中的每个字符都由单独的数字`Unicode`编码指定。
```

- 查找类方法

```js
  String.indexOf(searchvalue, fromindex) // 用来检索指定的字符串值在字符串中首次出现的位置。
  // `searchvalue`要查找的子字符串，`fromindex`查找的开始位置，省略的话则从开始位置进行检索。

  String.lastIndexOf(searchvalue, fromindex) // `lastIndexOf()`语法与`indexOf()`类似。
  // 它返回的是一个指定的子字符串值最后出现的位置，其检索顺序是从后向前。

  String.search(substr)/String.search(regexp) // lastIndexOf()语法与indexOf()类似。
  // 它返回的是一个指定的子字符串值最后出现的位置，其检索顺序是从后向前。

  String.match(substr/regexp) // 可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配。

// 参数中传入的是子字符串或是没有进行全局匹配的正则，那么match()方法会从开始位置执行一次匹配，
//如果没有匹配到结果，则返回null。
//否则则会返回一个数组，该数组的第0个元素存放的是匹配文本，
//返回的数组还含有两个对象属性index和input，匹配文本的起始索引和原字符串。
// 栗子："1a2b3c4d5e".match('b') // 返回： ["b", index: 3, input: "1a2b3c4d5e"]
```

- 截取子串的方法

```js
  String.substring(start, end) // 常用于字符串截取。
  // 返回内容从`start`处到`end-1`处的所有字符。

  String.sclice(start, end) // 与`substring`类似。
  // 参数可为负值，表示从字符串的尾部开始，-1为最后一个字符。

  String.substr(Start, length) // 可在字符串中抽取从`start`下标开始的指定数目的字符。
  // 返回包括start所指的字符开始的`length`个字符。
  // 如果没有指定 `length`，那么返回的字符串包含从`start`到`String`的结尾的字符。
  // 如果`start`为负数，则表示从字符串尾部开始算起。
```

- 其他方法

```js
  String.replace(regexp/substr, replacement) // 用来进行字符串替换操作。
  // 它可以接收两个参数，前者为被替换的子字符串（可以是正则），后者为用来替换的文本。

  // 第一个参数是子字符串/没有进行全局匹配的正则，进行一次替换（替换最前面的）。
  
  String.split(separator, howmany) // 用于把一个字符串分割成字符串数组。
  // separator表示分割位置(参考符)，howmany表示返回数组的允许最大长度(一般情况下不设置)。

  String.toLowerCase()
  String.toUpperCase()

  //`toLowerCase()`方法可以把字符串中的大写字母转换为小写;
  //`toUpperCase()`方法可以把字符串中的小写字母转换为大写。

```

## 事件委托

>  事件委托 应用场景：
 
- 给如所有`li`标签注册事件时，利用事件委托减少内存消耗
- 给如通过 AJAX 或者用户操作动态创建元素的事件绑定


实现把 `#list` 下的 `li`元素的事件

```js
  document.getElementById('co')
```


## AJAX 封装

