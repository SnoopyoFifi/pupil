# CSS3

- box-shadow 

`box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);`

**参数说明**：



- 美化具有placeholder属性的Input输入框

```html
  <style>
    
    /* 通用 */
    ::-webkit-input-placeholder { color:#f00; }
    ::-moz-placeholder { color:#f00; } /* firefox 19+ */
    :-ms-input-placeholder { color:#f00; } /* ie */
    input:-moz-placeholder { color:#f00; }

  </style>
```


- transform


    /* transition: opacity .2s linear .2s, top .1s linear .2s; *
    /* 执行变换的属性 变换延续的时间 在延续时间段，变换的速率变化  变换延迟时间*/


- `::selection` 改变选择文本的前景色&背景色

```html
<style>
   /*Webkit,Opera9.5+,Ie9+*/
  ::selection {
    background: 颜色值；
    color:颜色值；
  }
   /*Mozilla Firefox*/
  ::-moz-selection {
    background: 颜色值；
    color:颜色值；
  }
</style>
```

- 禁止鼠标点击事件

```html
<style>
  .disabled {
    pointer-events: none;
    cursor: default;
    opacity: 0.6;
  }
</style>
```
