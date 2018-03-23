# InterviewQuestion

> 前端面试题总结

## 常见问题
### 请解释 CSS 动画和 JavaScript 动画的优缺点。

### 浏览器同一时间可以从一个域名下载多少资源？有什么例外么？

### 请说出三种减少页面加载的方法。

### 你是如何对网站的文件和资源进行优化的？

### 你能描述渐进增强和优雅降级之间的不同么？

### 如果有5个不同的样式表文件，整合进网站的最好方式是？

### 什么是跨域资源共享（cors）？用于解决什么问题？

### 什么是FOUC(无样式内容闪烁)？你是如何避免FOUC?

### 最近遇到什么技术挑战？

### 在制作一个网页应用或网站的过程中，你是如何考虑其UI、安全性、高性能、SEO、可维护性以及技术因素的？


## JS部分

### 请解释事件委托
事件委托是将事件监听器添加到父元素，而不是每个子元素单独设置事件监听器。当触发子元素时，事件会冒泡到父元素，监听就会触发。
事件委托的好处是：
- 内存占用少，因为只需要一个父元素的事件处理程序，而不必为每个后代都添加事件处理程序；
- 无需从已删除的元素中解绑处理程序，也无需将处理程序绑定到新元素上。

### 请简述`javascript`中的`this`
粗略的讲，函数的调用方式决定了`this`的值。
- 在调用函数时使用`new`关键字，函数内的`this`指向新创建的实例对象；
- 如果`apply`、`call`或`bind`方法用于调用、创建一个函数，函数内的`this` 就是作为参数(第一个)传入这些方法的对象。
- 当函数作为对象里的方法被调用时，函数内的`this`的值就是调用该函数的对象。
- 当函数作为普通函数调用，`this`指向全局对象。浏览器环境下`this`的值指向`window`，但是严格模式下，`this`的值为`undefined`。
- 如果同时符合上述多个规则，则较高的规则(1号最高)将决定`this`的值。
- 如果该函数时`ES2015`中的箭头函数，将忽略上面所有规则，`this`将被设置为它被创建时的上下文。

### 请解释原型继承的原理。

### 请举出一个匿名函数的典型用例？

### 描述以下变量的区别：null，undefined 或 undeclared？ 该如何检测它们？

### 请解释为什么接下来这段代码不是 IIFE (立即调用的函数表达式)：`function foo(){ }()`;要做哪些改动使它变成 IIFE?

### 你是如何组织自己的代码？是使用模块模式，还是使用经典继承的方法？

### .call 和 .apply 的区别是什么？

### 请解释 Function.prototype.bind？

### 请指出 JavaScript 宿主对象 (host objects) 和原生对象 (native objects) 的区别？

### 请指出浏览器特性检测，特性推断和浏览器 UA 字符串嗅探的区别？

### 请尽可能详尽的解释 Ajax 的工作原理。
### 使用 Ajax 都有哪些优劣？
### 请解释 JSONP 的工作原理，以及它为什么不是真正的 Ajax。

### 你使用过 JavaScript 模板系统吗？ 如有使用过，请谈谈你都使用过哪些库？

### 请解释变量声明提升 (hoisting)。

### 请描述事件冒泡机制 (event bubbling)。
### "attribute" 和 "property" 的区别是什么？
### 为什么扩展 JavaScript 内置对象不是好的做法？
### 请指出 document load 和 document DOMContentLoaded 两个事件的区别。
### `==` 和 `===` 有什么不同？
### 请解释 JavaScript 的同源策略 (same-origin policy)。
### 如何实现下列代码：
```javascript
[1,2,3,4,5].duplicator(); // [1,2,3,4,5,1,2,3,4,5]
```

### 什么是三元表达式 (Ternary expression)？“三元 (Ternary)” 表示什么意思？
### 什么是 `"use strict";` ? 使用它的好处和坏处分别是什么？
### 请实现一个遍历至 `100` 的 for loop 循环，在能被 `3` 整除时输出 **"fizz"**，在能被 `5` 整除时输出 **"buzz"**，在能同时被 `3` 和 `5` 整除时输出 **"fizzbuzz"**。
### 为何通常会认为保留网站现有的全局作用域 (global scope) 不去改变它，是较好的选择？
### 为何你会使用 `load` 之类的事件 (event)？此事件有缺点吗？你是否知道其他替代品，以及为何使用它们？
### 请解释什么是单页应用 (single page app), 以及如何使其对搜索引擎友好 (SEO-friendly)。
### 你使用过 Promises 及其 polyfills 吗? 请写出 Promise 的基本用法（ES6）。
### 使用 Promises 而非回调 (callbacks) 优缺点是什么？
### 使用一种可以编译成 JavaScript 的语言来写 JavaScript 代码有哪些优缺点？
### 你使用哪些工具和技术来调试 JavaScript 代码？
### 你会使用怎样的语言结构来遍历对象属性 (object properties) 和数组内容？
### 请解释可变 (mutable) 和不变 (immutable) 对象的区别。
### 请举出 JavaScript 中一个不变性对象 (immutable object) 的例子？
### 不变性 (immutability) 有哪些优缺点？
### 如何用你自己的代码来实现不变性 (immutability)？
### 请解释同步 (synchronous) 和异步 (asynchronous) 函数的区别。
### 什么是事件循环 (event loop)？请问调用栈 (call stack) 和任务队列 (task queue) 的区别是什么？
### 解释 `function foo() {}` 与 `var foo = function() {}` 用法的区别

### 什么是闭包，如何使用它，为什么要使用它？
- [闭包面试题解析](https://segmentfault.com/a/1190000004187681)

```js
function fun(n, o){
  console.log(o);
  return {
    fun: function(m){
      return fun(m, n);
    }
  }
}

// 三行 a, b, c 输出分别是什么？ 
var a = fun(0); a.fun(1); a.fun(2); a.fun(3);
var b = fun(0).fun(1).fun(2).fun(3);
var c = fun(0).fun(1); c.fun(2); c.fun(3);
```

### 请说明`.forEach`循环时和`.map()`循环的主要区别，使用场景分别是什么？
**`forEach`**
- 遍历数组中的元素
- 为每个元素执行回调
- 无返回值

```js
  const a = [1, 2, 3];
  const doubled = a.forEach((num, index)=>{
    
  })
```

**`map`**
- 遍历数组中的元素
- 通过对每个元素调用函数，将每个元素“映射”到一个新元素，从而创建一个新数组
- 返回创建的新数组

```js
  const a = [1, 2, 3];
  const doubled = a.map(num => {
    return num*2;  
  })
```

`.forEach()`和`.map`的主要区别在于`.map()`返回一个新的数组。如果想得到一个结果，但是不改变原始数组，用`.map()`。如果只是需要在数组上做迭代修改，用`.forEach()`。

### 你怎么看`AMD` VS `CommonJS`？

### 模块化开发历史

* 2009年初，commonjs规范还未出来，此时前端开发人员编写的代码都是非模块化的，
    - 那个时候开发人员经常需要十分留意文件加载顺序所带来的依赖问题
* 与此同时 nodejs开启了js全栈大门，而requirejs在国外也带动着前端逐步实现模块化
    - 同时国内seajs也进行了大力推广
    - AMD 规范 ，具体实现是requirejs define('模块id',[模块依赖1,模块依赖2],function(){  return ;}) , ajax请求文件获取数据
    - CMD 规范， seajs淘宝玉伯开发， CMD和commonjs模块部分差不多，
        + nodejs和seajs非常像 通过require引入模块，module.exports导出模块
    - UMD 通用模块定义，一种既能兼容amd也能兼容commonjs 也能兼容浏览器环境运行的万能代码
* npm/bower集中包管理的方式备受青睐，12年browserify/webpack诞生
* 定义一个立即执行的模块

```javascript

(function (root, factory) {  
    if (typeof exports === 'object') { 
        // Commonjs, 在commonjs的环境之下
        module.exports = factory();  // factory的调用会返回你的模块对象      
    } else if (typeof define === 'function' && define.amd) {  
        // AMD  在requirejs模块加载框架的运行之中
        define(factory);  //factory调用以后获取到其return的返回值模块对象 
    } else {  
        //  没有使用模块加载器的方式
        window.eventUtil = factory();  
    }  
})(this, function() {  
    // module  
    return {  
        //具体模块代码
        addEvent: function(el, type, handle) {  
            //...  
        },  
        removeEvent: function(el, type, handle) {  
              
        },  
    };  
});  

```


### 数组去重
- [数组去重](http://www.jb51.net/article/118657.htm)

```js
  // 方法一：
  // 外层循环元素，内层循环比较值，相同则跳过
  Array.prototype.distinct = function() {
    var arr = this,
        result = [],
        i, j,
        len = arr.length;
    for(i = 0; i < len; i++) {
      for(j = i + 1; j < len; j++) {
        if(arr[i] === arr[j]) {
          j = ++i;
        }
      }
      result.push(arr[i]);
    }
    return result;
  };
  
  // 方法二
  // 外层循环元素，内城循环比较值，相同则删除
  Array.prototype.distinct = function() {
    var arr = this,
        i, j,
        len = arr.length;
    for(i = 0; i < len; i++) {
      for(j = i + 1; j < len; j++) {
        if(arr[i] == arr[j]) {
          arr.splice(j, 1);
          len--;
          j--;
        }
      }
    }
    return arr;
  };

  // 方法三：
  // 利用对象的属性不能相同的特点
  Array.prototype.distinct = function() {
    var arr = this,
        i,
        obj = {},
        result = [],
        len = arr.length;
    for(i = 0; i < len; i++) {
      if(!obj[arr[i]]){
        obj[arr[i]] = 1;
        result.push(arr[i]);
      }
    }
    return result;
  };

  // 数组递归去重
  // 运用递归去重，先排序，从最后开始比较，相同则删除
  Array.prototype.distinct = function() {
    var arr = this,
        len = arr.length;
    arr.sort(function(a, b){
      return a - b;
    });
    function loop(index) {
      if(index >= 1) {
        if(arr[index] === arr[index-1]) {
          arr.splice(index, 1);
        }
        loop(index - 1);+
      }
    }
    loop(len - 1);
    return arr;
  };


  // 方法五
  // 利用indexOf以及forEach
  Array.prototype.distinct = function() {
    var arr = this,
        result = [],
        len = arr.length;
    arr.forEach(function(v, i, arr) {
      var bool = arr.indexOf(v, i+1);
      if(bool === -1) {
        result.push(v);
      }
    })
    return result;
  }

  // 方法五
  // 利用ES6的Set成员的唯一性
  function dedupe(array) {
    return Array.from(new Set(array));
  }

  // 拓展运算符(...)
  [...new Set(arr)]
```

## `TCP`传输的三次握手四次挥手策略

