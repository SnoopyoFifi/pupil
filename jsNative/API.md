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
> `.forEach()`方法没有返回值，不需要在回调函数里写`return`。

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

> 什么是`ajax`

- ajax：一种请求数据的方式，不需要刷新整个页面； 
- ajax的技术核心是: XMLHttpRequest 对象； 
- ajax 请求过程：创建 XMLHttpRequest 对象、连接服务器、发送请求、接收响应数据；

> `ajax` 封装函数

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
```

> `ajax`请求步骤

- **创建**

   - IE7 及其以上原生支持`XHR`对象，可直接使用：var oAJAX = new XMLHttpRequest();
   - IE6 及其之前的版本中，`XHR`对象是通过`XSXML`库中的`ActiveX`对象实现的，可使用： var oAjax = new ActiveXObject('Microsoft.XMLHTTP');

- **连接和发送**

   - `open()`函数的三个参数： 请求方式、请求地址、是否异步请求；
   - `GET`请求方式是通过`URL`参数将数据提交到服务器的，`POST`则是通过将数据作为`send`的参数提交到服务器；
   - `POST`请求中，在发送数据之前，要设置表单提交的内容类型；
   - 提交到服务器的参数要经过 `encodeURIComponent()`方式进行编码，实际上在参数列表'key=value'的形式中，`key`和`value`都需要进行编码，因为会包含特殊字符。每次请求的时候都会在参数列表中拼入一个'v=xx'的字符串，这样是为了拒绝缓存，每次都直接请求到服务器上。

> 拓展：
   - `encodeURI()` ：用于整个 URI 的编码，不会对本身属于 URI 的特殊字符进行编码，如冒号、正斜杠、问号和井号；其对应的解码函数 `decodeURI()`；
   - `encodeURIComponent() `：用于对 URI 中的某一部分进行编码，会对它发现的任何非标准字符进行编码；其对应的解码函数 `decodeURIComponent()`；

- **接收**
   
   - 接收到响应后，响应的数据会自动填充`XHR`对象，相关属性如下：
     + responseText：响应返回的主体内容，为字符串类型； 
     + responseXML：如果响应的内容类型是 "text/xml" 或 "application/xml"，这个属性中将保存着相应的xml 数据，是 XML 对应的 document 类型； 
     + status：响应的HTTP状态码； 
     + statusText：HTTP状态的说明
   
   - XHR对象的readyState属性表示请求/响应过程的当前活动阶段，这个属性的值如下
      - 0-未初始化，尚未调用open()方法； 
      - 1-启动，调用了open()方法，未调用send()方法； 
      - 2-发送，已经调用了send()方法，未接收到响应； 
      - 3-接收，已经接收到部分响应数据； 
      - 4-完成，已经接收到全部响应数据； 
      - 只要 `readyState` 的值变化，就会调用 `readystatechange` 事件，(其实为了逻辑上通顺，可以把`readystatechange`放到`send`之后，因为`send`时请求服务器，会进行网络通信，需要时间，在`send`之后指定`readystatechange`事件处理程序也是可以的，我一般都是这样用，但为了规范和跨浏览器兼容性，还是在`open`之前进行指定吧)。

   - 在`readystatechange`事件中，先判断响应是否接收完成，然后判断服务器是否成功处理请求，`xhr.status` 是状态码，状态码以2开头的都是成功，304表示从缓存中获取，上面的代码在每次请求的时候都加入了随机数，所以不会从缓存中取值，故该状态不需判断。

- **注意**：`ajax` 请求是不能跨域的！

> jsonp原理及其组成

- JSONP(JSON with Padding) 是一种跨域请求方式。

- 主要原理是利用了script 标签可以跨域请求的特点，由其 src 属性发送请求到服务器，服务器返回 js 代码，网页端接受响应，然后就直接执行了，这和通过 script 标签引用外部文件的原理是一样的。

- JSONP由两部分组成：回调函数和数据，回调函数一般是由网页端控制，作为参数发往服务器端，服务器端把该函数和数据拼成字符串返回。

> `jsonp` 跨域函数封装

```js
  // jsonp封装函数调用
  jsonp({
    url: 'http://www.baidu.com',
    callback: 'callback', // 回调函数的名称前后端需一致
    data: {id: '1000120'},
    success: function(json){
      alert('jsonp_ok');
    },
    error: function(){
      alert('error');
    },
    time: 10000    
  })
  function jsonp(options) {
    options = options || {};
    if (!options.url || !options.callback) {
      throw new Error("参数不合法");
    }

    //创建 script 标签并加入到页面中
    var callbackName = ('jsonp_' + Math.random()).replace(".", "");
    var oHead = document.getElementsByTagName('head')[0];
    options.data[options.callback] = callbackName;
    var params = formatParams(options.data);
    var oS = document.createElement('script');
    oHead.appendChild(oS);

    //创建jsonp回调函数
    window[callbackName] = function (json) {
      oHead.removeChild(oS);
      clearTimeout(oS.timer);
      window[callbackName] = null;
      options.success && options.success(json);
    };

    //发送请求
    oS.src = options.url + '?' + params;

    //超时处理
    if (options.time) {
        oS.timer = setTimeout(function () {
            window[callbackName] = null;
            oHead.removeChild(oS);
            options.error && options.error({ message: "超时" });
        }, time);
    }
  };

  //格式化参数
  function formatParams(data) {
    var arr = [];
    for (var name in data) {
        arr.push(encodeURIComponent(name) + '=' + encodeURIComponent(data[name]));
    }
    return arr.join('&');
  }
```

> 封装函数几点说明

- 因为 script 标签的 src 属性只在第一次设置的时候起作用，导致 script 标签没法重用，所以每次完成操作之后要移除；

- JSONP这种请求方式中，参数依旧需要编码；

- 如果不设置超时，就无法得知此次请求是成功还是失败。


## 常用表单验证正则表达式

[正则表达式说明](http://caibaojian.com/javascript-zhengze.html)

> 用户名正则

```js
//用户名正则，4到16位（字母，数字，下划线，减号）
var uPattern = /^[a-zA-Z0-9_-]{4,16}$/;
//输出 true
console.log(uPattern.test("caibaojian"));

```

> 密码强度正则

```js
//密码强度正则，最少6位，包括至少1个大写字母，1个小写字母，1个数字，1个特殊字符
var pPattern = /^.*(?=.{6,})(?=.*\d)(?=.*[A-Z])(?=.*[a-z])(?=.*[!@#$%^&*? ]).*$/;
//输出 true
console.log("=="+pPattern.test("caibaojian#"));

```

> 整数正则

```js
//正整数正则
var posPattern = /^\d+$/;
//负整数正则
var negPattern = /^-\d+$/;
//整数正则
var intPattern = /^-?\d+$/;
//输出 true
console.log(posPattern.test("42"));
//输出 true
console.log(negPattern.test("-42"));
//输出 true
console.log(intPattern.test("-42"));

```

> 数字正则

可以是整数也可以是浮点数

```js
//正数正则
var posPattern = /^\d*\.?\d+$/;
//负数正则
var negPattern = /^-\d*\.?\d+$/;
//数字正则
var numPattern = /^-?\d*\.?\d+$/;
console.log(posPattern.test("42.2"));
console.log(negPattern.test("-42.2"));
console.log(numPattern.test("-42.2"));

```

> Email正则

```js
//Email正则
var ePattern = /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/;
//输出 true
console.log(ePattern.test("99154507@qq.com"));

```

> 手机号码正则

```js
//手机号正则
var mPattern = /^1[34578]\d{9}$/; //http://caibaojian.com/regexp-example.html
//输出 true
console.log(mPattern.test("15507621888"));

```

> 身份证号正则

```js
//身份证号（18位）正则
var cP = /^[1-9]\d{5}(18|19|([23]\d))\d{2}((0[1-9])|(10|11|12))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/;
//输出 true
console.log(cP.test("11010519880605371X"));

```

>  URL正则

```js
//URL正则
var urlP= /^((https?|ftp|file):\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
//输出 true
console.log(urlP.test("http://caibaojian.com"));

```

> IPv4地址正则

```js
//ipv4地址正则
var ipP = /^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/;
//输出 true
console.log(ipP.test("115.28.47.26"));

```

> 十六进制颜色正则

```js
//RGB Hex颜色正则
var cPattern = /^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/;
//输出 true
console.log(cPattern.test("#b8b8b8"));

```

> 日期正则 

```js
//日期正则，简单判定,未做月份及日期的判定
var dP1 = /^\d{4}(\-)\d{1,2}\1\d{1,2}$/;
//输出 true
console.log(dP1.test("2017-05-11"));
//输出 true
console.log(dP1.test("2017-15-11"));
//日期正则，复杂判定
var dP2 = /^(?:(?!0000)[0-9]{4}-(?:(?:0[1-9]|1[0-2])-(?:0[1-9]|1[0-9]|2[0-8])|(?:0[13-9]|1[0-2])-(?:29|30)|(?:0[13578]|1[02])-31)|(?:[0-9]{2}(?:0[48]|[2468][048]|[13579][26])|(?:0[48]|[2468][048]|[13579][26])00)-02-29)$/;
//输出 true
console.log(dP2.test("2017-02-11"));
//输出 false
console.log(dP2.test("2017-15-11"));
//输出 false
console.log(dP2.test("2017-02-29"));

```

> QQ号码正则 

```js
//QQ号正则，5至11位
var qqPattern = /^[1-9][0-9]{4,10}$/;
//输出 true
console.log(qqPattern.test("65974040"));

```

> 微信号正则

```js
//微信号正则，6至20位，以字母开头，字母，数字，减号，下划线
var wxPattern = /^[a-zA-Z]([-_a-zA-Z0-9]{5,19})+$/;
//输出 true
console.log(wxPattern.test("caibaojian_com"));

```

> 车牌号正则

```js
//车牌号正则
var cPattern = /^[京津沪渝冀豫云辽黑湘皖鲁新苏浙赣鄂桂甘晋蒙陕吉闽贵粤青藏川宁琼使领A-Z]{1}[A-Z]{1}[A-Z0-9]{4}[A-Z0-9挂学警港澳]{1}$/;
//输出 true
console.log(cPattern.test("粤B39006"));

```

> 包含中文正则

```js
//包含中文正则
var cnPattern = /[\u4E00-\u9FA5]/;
//输出 true
console.log(cnPattern.test("蔡宝坚"));
```

