# InterviewQuestion

## 闭包
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

## 模块化开发历史

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


## 数组去重
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

