# Promise对象

## 什么是`Promise`

```js
  var promise = new Promise(function(resolve, reject){
    // ...
  })
```

- `Promise`对象是用来处理异步请求的构造函数，从它可以获取异步操作的消息。

- `Promise`提供统一的`API`，各种异步操作都可以使用同样的方法进行处理。

- `Promise`对象特点：
  + 三种状态：`Pending`(进行中)、`Fulfilled`(已成功)、`Rejected`(已失败)， 只有异步结果可以改变其状态。
  + 其状态改变后不可变Resolved(已定型)，但任何时候都可以得到这个结果，这点区别于事件监听。

- `Promise`对象缺点：
  + 一旦新建其实例对象，就立即执行无法取消；
  + 如果不设置回调函数，外部无法获取其内部抛出的错误；
  + 其处于`Pending`状态时，无法确定异步操作是刚刚开始还是即将完成。

## 用法

> `Promise`的使用： 

```js
  var promise = new Promise(function(resolve, reject) {
    if(/*异步操作成功*/) {
      resolve(value);
    } else {
      reject(error);
    }
  })

  // 写法一；
  promise.then(function(value){}, function(error){});
  // 写法二：
  promise.then(function(value){}).catch(function(error){});
```

> 栗子一:(`resolve` 的参数)

```js
  var p1 = new Promise(function(resolve, reject){
    setTimeout(() => reject(new Error('fail')), 3000) 
  })
  var p2 = new Promise(function(resolve, reject){
    setTimeout(() => resolve(p1), 1000)
  })
  p2.then(result => console.log(result))
    .catch(error => console.log(error))
```

> 栗子二：(`Promise`实例新建后立即执行)

```js
  let promise = new Promise(function(resolve, reject){
    console.log('Promise');
    resolve();
  })
  promise.then(function(){
    console.log('Resolve');
  })
  console.log('Hi!')
  // Promise
  // Hi!
  // Resolve
```

**说明**：
- `Promise`构造函数创建实例对象`promise`；
- 创建实例对象时，构造函数传入一个回调函数，该回调函数接受两个参数`resolve`、`reject`；
- `resolve`函数的作用是，将`Promise`对象的状态从`Pending`变为`Resolved`，在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；
- `reject`函数的作用是，将`Promise`对象的状态从`Pending`变为`Reject`，在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去；
- 实例生成后，可以用`then`方法分别指定`Resolve`状态和`Reject`状态的回调函数(即resolve和reject)；
- 提倡使用写法二；
- 如果调用`resolve`和`reject`函数时带有参数，那么该参数会被传递给回调函数；
- 且`reject`函数的参数通常是`Error`对象的实例；`resolve`函数的参数除了正常的值外，可能是另一个`Promise`实例(栗子一)；
- `catch`方法是.then(null,rejection)的别名(都是定义在原型对象上的)，用来指定发生错误的回调函数；
- `Promise`新建后就会立即执行，随后执行当前脚本所有同步任务，最后才会执行then方法的指定的回调函数(栗子二)；

## 应用





### `Ajax`操作

> `Ajax`操作是典型的异步操作

```js

  // ajax 封装函数调用
  ajax({
    url: "./TestXHR.aspx",   
    type: "POST",                    
    data: { name: "super", age: 20 },  
    dataType: "json",
    success: function (response, xml) {
        // 此处放成功后执行的代码
    },
    error: function (status) {
        // 此处放失败后执行的代码
    }
  });
  function ajax(options) {
    options = options || {};
    options.type = (options.type || "GET").toUpperCase();
    options.dataType = options.dataType || "json";
    var params = formatParams(options.data),
        xhr;

      //创建 - 非IE6 - 第一步
      if (window.XMLHttpRequest) {
        xhr = new XMLHttpRequest();
      } else { //IE6及其以下版本浏览器
        xhr = new ActiveXObject('Microsoft.XMLHTTP');
      }

      //接收 - 第三步
      xhr.onreadystatechange = function () {
          if (xhr.readyState == 4) {
              var status = xhr.status;
              if (status >= 200 && status < 300) {
                  options.success && options.success(xhr.responseText, xhr.responseXML);
              } else {
                  options.error && options.error(status);
              }
          }
      }

      //连接 和 发送 - 第二步
      if (options.type == "GET") {
          xhr.open("GET", options.url + "?" + params, true);
          xhr.send(null);
      } else if (options.type == "POST") {
          xhr.open("POST", options.url, true);
          //设置表单提交时的内容类型
          xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
          xhr.send(params);
      }
  }

  //格式化参数
  function formatParams(data) {
    var arr = [];
    for (var name in data) {
        arr.push(encodeURIComponent(name) + "=" + encodeURIComponent(data[name]));
    }
    arr.push(("v=" + Math.random()).replace(".",""));
    return arr.join("&");
  }



  // 用Promise对象改写
  
  function ajax(options) {
    options = options || {};
    options.type = (options.type || "GET").toUpperCase();
    options.dataType = "json";
    var params = formatParams(options.data),
        xhr;

    var p = new Promise(function(resolve, reject){
      
      //创建 - 非IE6 - 第一步
      if (window.XMLHttpRequest) {
        xhr = new XMLHttpRequest();
      } else { //IE6及其以下版本浏览器
        xhr = new ActiveXObject('Microsoft.XMLHTTP');
      }

      //接收 - 第三步
      xhr.onreadystatechange = function () {
          if (xhr.readyState == 4) {
              var status = xhr.status;
              if (status >= 200 && status < 300) {
                  var result = JSON.parse(this.responseText);
                  resovle(result);
              } else {
                  reject(new Error(this.statusText));
              }
          }
      }

      //连接 和 发送 - 第二步
      if (options.type == "GET") {
          xhr.open("GET", options.url + "?" + params, true);
          xhr.send(null);
      } else if (options.type == "POST") {
          xhr.open("POST", options.url, true);
          //设置表单提交时的内容类型
          xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
          xhr.send(params);
      }
    });
    return p;
  }

  ajax({
    url: "./TestXHR.aspx",   
    type: "POST",                    
    data: { name: "super", age: 20 },  
    dataType: "json"
  }).then(function(result){
    console.log('Content:'+ result);
  }).catch(function(error){
    console.error('出错了', error);
  })

```

