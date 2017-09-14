# InterviewQuestion

## 闭包

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

```js
  
```

