# CodeSnippet

>  判断字符串长度

英文占1个字符，中文汉字占2个字符

```js
function strlen(str){
  var len = 0;
  for (var i=0; i<str.length; i++) {
    var c = str.charCodeAt(i);
    if ((c >= 0x0001 && c <= 0x007e) || (0xff60<=c && c<=0xff9f)) {
      len++;
    }
    else {
      len+=2;
    }
  }
  return len;
}
```


>  阻止事件冒泡和浏览器的默认行为

1. 阻止事件冒泡，使成为捕获事件触发机制
```js
function stopBubble(e) {
  // 如果提供了事件对象，则是一个非IE浏览器
    if (e && e.stopPropagation) {
      // 因此它支持w3c的stopPropagation()方法
    e.stopPropagation();
    } else {
        // 否则，使用IE的方式
    window.event.canceBubble = true;
    }
}
```

2. a链接点击后阻止其跳转，即阻止了事件默认行为
```js
function stopDefault(e) {
  // 如果提供了事件对象，则是一个非IE浏览器
  if(e && e.preventDefault) {
        e.preventDefault();
  } else {
        wondow.event.returnValue = false;
  }
  return false;
}
```

> 绑定事件兼容性封装 

```js
window.onload = function(){
  var EventUtil = {
    // 绑定事件
    addHandler: function(element, type, handler){
      // 若浏览器支持 addEventListener， 则使用 addEventListener来添加事件
      if(element.addEventListener){
        element.addEventListener(type, hanlder, false);
      } else if (element.attachEvent) {
        element.attachEvent('on' + type, handler);
      } else {
        // 若以上两种添加事件的方法都不支持，则使用默认的行为来添加事件
        element['on' + type] = handler;
      }
    }
    // 移除事件
    removeHandler: function(element, type, handler) {
      if (element.removeEventListener) {
        element.removeEventListener(type, handler, false);
      } else if(element.detachEvent) {
        element.detachEvent('on' + type, handler);
      } else {
        element['on' + type] = null;
      }
    }
  }
}

// 事件绑定函数的调用
EventUtil.addHandler(需要绑定事件的标签, "需要绑定的事件", "绑定事件的处理方法");

EventUtil.removeHandler(需要删除事件的标签, "需要删除的事件", "绑定事件的处理方法");

```

> 常用正则表达式

```js
{
  //手机，邮箱验证正则式
  reMobileEmail: /^(1[34578]\d{9}|[a-zA-Z0-9_\.\-]+@(([a-zA-Z0-9])+\.)+([a-zA-Z0-9]{2,4}))$/,
  //手机
  reMobile: /^(1[34578]\d{9})$/,
  //邮件
  reEmail: /^[a-zA-Z0-9_\.\-]+@(([a-zA-Z0-9])+\.)+([a-zA-Z0-9]{2,4})$/
}
```

> 表单验证 

>返回顶部

