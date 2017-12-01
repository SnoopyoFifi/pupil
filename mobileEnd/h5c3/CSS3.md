# CSS3

> CSS3新属性

## box-shadow 盒子阴影

  ```

    box-shadow: 水平偏移值  垂直偏移值  模糊半径(可选)  扩展半径(可选)  颜色(可选);

    box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);

    box-shadow: -5px 0 5px -5px green,   /*左边阴影*/
                0 -5px 5px -5px pink,    /*顶部阴影*/
                0 5px  5px -5px yellow,  /*底部阴影*/
                5px 0 5px -5px red;      /*右边阴影*/

    box-shadow: inset 0 3px #2f4351;
  ```

  - **参数说明**：

     - 可选的扩展半径: 正值时，整个阴影都延展扩大，反之则缩小

  ![](../images/boxshadowstyles.png)

## transform-style 3D呈现 

  > 属性指定嵌套元素是怎样在三维空间中呈现

  - **参数说明**：
    - `transform-style: flat;` 表示所有子元素在2D平面呈现；
    - `transform-style: preserve-3d;` 表示所有子元素在3D空间中呈现。

## transform-origin 变形原点

  > 设置旋转元素的基点位置 

## backface-visibiliy 隐藏内容的背面

## transform 变形

  ```
    transform: 旋转元素(rotate)  缩放元素(scale)  移动元素(translate)  倾斜元素(skew)  矩阵变形(matrix)  透视(perspective);
  ```

  | 值                                        | 描述                                       |
  | ---------------------------------------- | ---------------------------------------- |
  | none                                     | 定义不进行转换。                                 |
  | matrix(*n*,*n*,*n*,*n*,*n*,*n*)          | 定义 2D 转换，使用六个值的矩阵。                       |
  | matrix3d(*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*) | 定义 3D 转换，使用 16 个值的 4x4 矩阵。               |
  | translate(*x*,*y*)                       | 定义元素在2D X轴和Y轴同时移动。 省略第二个参数则为0；参数为负，则表示往相反的方向移动。 |
  | translate3d(*x*,*y*,*z*)                 | 定义元素在3D X轴、Y轴和Z轴同时移动。                    |
  | translateX(*x*)                          | 表示只在X轴(水平方向)移动元素。                        |
  | translateY(*y*)                          | 表示只在Y轴(垂直方向)移动元素。                        |
  | translateZ(*z*)                          | 表示只在Z轴移动元素，前提是元素本身或者元素的父元素设定了透视值。        |
  | scale(*x*[,*y*]?)                        | 表示使元素在X轴和Y轴同时缩放。可以是正数、负数和小数。负数是先翻转元素然后再缩放。缺少第二个参数，那么其值等于第一个参数。 |
  | scale3d(*x*,*y*,*z*)                     | 定义 3D 缩放转换。                              |
  | scaleX(*x*)                              | 表示只在X轴(水平方向)缩放元素。                        |
  | scaleY(*y*)                              | 表示只在Y轴(垂直方向)缩放元素。                        |
  | scaleZ(*z*)                              | 表示只在Z轴缩放元素。前提是元素本身或者元素的父元素设定了透视值         |
  | rotate(*angle*)                          | 定义 2D 旋转，正数是顺时针旋转，负数是逆时针旋转。              |
  | rotate3d(*x*,*y*,*z*,*angle*)            | 定义 3D 旋转。                                |
  | rotateX(*angle*)                         | 定义沿着 X 轴的 3D 旋转。                         |
  | rotateY(*angle*)                         | 定义沿着 Y 轴的 3D 旋转。                         |
  | rotateZ(*angle*)                         | 定义沿着 Z 轴的 3D 旋转。                         |
  | skew(*x-angle*,*y-angle*)                | 包含两个参数值，分别表示X轴和Y轴倾斜的角度。第二个参数为空，则为0，参数为负表示向相反方向倾斜。 |
  | skewX(*angle*)                           | 表示只在X轴(水平方向)倾斜。                          |
  | skewY(*angle*)                           | 表示只在Y轴(垂直方向)倾斜。                          |
  | perspective(*n*)                         | 为 3D 转换元素定义透视视图。                         |

  **注意**：
  - `persprctive`

    - `perspective` 变换函数对于 3D 变换来说至关重要。
    - 该函数会设置查看者的位置，并将可视内容映射到一个视锥上，继而投影到一个 2D 视平面上。
    - 如果不指定透视，则 Z 空间中的所有点将平铺到同一个 2D 视平面中，并且变换结果中将不存透视深概念。
    - 作用于元素的子元素。
    - 关联属性：`perspective-origin`
    - perspective有两种写法，
      - 一种是设置所有的子元素有一个共同的透视值，perspective作为一个属性值来写；
      - 一种是直接作用于元素本身，perspective作为transform的一个函数来写如：

  ```
  .wrap{-webkit-perspective:1000px;}
  .wrap .child{-webkit-transform:perspective(1000px);}
  ```

## transition 过渡

  ```
    transition: 过渡的属性 过渡延续的时间 过渡的效果 过渡延迟时间;

    transition: all .2s ease 2s;  /*所有属性都执行过渡*/

    transition: opacity .2s linear .2s, /*透明度执行过渡*/
                top .1s linear .2s,     /*top值执行过渡*/
                transform .3s;

  ```

  - **参数说明**：

    - 执行过渡的属性(`transition-property`)：初始值为`all`，适用于所有元素包括`:before`和`:after`；
    - 过渡延续的时间(`transition-duration`)：初始值为0，适用于所有元素包括`:before`和`:after`；
    - 过渡的效果(`transition-timing-function` 同 `animation-timing-function`)：
      + ease：缓解效果；
      + linear：线性效果；
      + ease-in：渐显效果；
      + ease-out：渐隐效果；
      + ease-in-out：渐显渐隐效果；
      + cubic-bezier：特殊的立方贝塞尔曲线效果。
    - 过渡延迟的时间(`transition-delay`)：可为负值，表示设置时间前的动画将被截断。

## `@keyframe`动画

  | 属性                                       | 描述                                      |
  | ---------------------------------------- | --------------------------------------- |
  | [@keyframes](http://www.runoob.com/cssref/css3-pr-animation-keyframes.html) | 规定动画。                                   |
  | [animation](http://www.runoob.com/cssref/css3-pr-animation.html) | 所有动画属性的简写属性，除了 animation-play-state 属性。 |
  | [animation-name](http://www.runoob.com/cssref/css3-pr-animation-name.html) | 规定 @keyframes 动画的名称。                    |
  | [animation-duration](http://www.runoob.com/cssref/css3-pr-animation-duration.html) | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。               |
  | [animation-timing-function](http://www.runoob.com/cssref/css3-pr-animation-timing-function.html) | 规定动画的速度曲线。默认是 "ease"。                   |
  | [animation-delay](http://www.runoob.com/cssref/css3-pr-animation-delay.html) | 规定动画何时开始。默认是 0。                         |
  | [animation-iteration-count](http://www.runoob.com/cssref/css3-pr-animation-iteration-count.html) | 规定动画被播放的次数。默认是 1。                       |
  | [animation-direction](http://www.runoob.com/cssref/css3-pr-animation-direction.html) | 规定动画是否在下一周期逆向地播放。默认是 "normal"。          |
  | [animation-play-state](http://www.runoob.com/cssref/css3-pr-animation-play-state.html) | 规定动画是否正在运行或暂停。默认是 "running"。            |

  **参数说明**：

  - `@keyframe` 

    > `@keyframes`相当于一个命名空间，后面跟一个名词，如果在类样式中的`animation-name`定义了与之对应的`name`，那么就可以执行动画了。

     - 简单动画

      > 定义动画时，简单的动画可以直接使用关键字from和to，即从一种状态过渡到另一种状态。

    ```html
    <style>
      @-webkit-keyframes demo{
          from{left:0;}
          to{left:400px;}
      }
    </style>
    ```

     - 复杂动画：

      > 下面的百分百有点像flash里帧的概念。表示设置某个时间段内任意时间点的样式。

    ```html
    <style>
      @-webkit-keyframes demo{
          0%{left:0;}
          50%{left:200px;}
          100%{left:400px;}
      }
    </style>
    ```

     - 实例：

    ```html
    <style>
       .animation_name{
          left:0;
          top:100px;
          position:absolute;
          -webkit-animation:0.5s 0.5s ease infinite alternate;
          -webkit-animation-name:demo;
          -moz-animation:0.5s 0.5s ease infinite alternate;
          -moz-animation-name:demo;
      }
      @-webkit-keyframes demo{
          0%{left:0;}
          100%{left:400px;}
      } 
    </style>
    <div class="demo_box animation_name">看我没事来回跑</div>  
    ```

  - `animation-delay`
    
    > 设置动画延迟执行的时间。
    
     - 0：不延迟，立即执行。
     - 正数：按照设置的时间延迟。
     - 负数：设置时间前的动画将被截断。

  - `animation-timing-function`

    > 同上`transition-timing-function`

  - `animation-direction`

    > 检索或设置对象动画循环播放次数大于1次时，动画是否反向运动。
      
     - normal：正常方向。
     - reverse：动画反向运行,方向始终与normal相反。（FF14.0.1以下不支持）
     - alternate：动画会循环正反方向交替运动，奇数次（1、3、5……）会正常运动，偶数次（2、4、6……）会反向运动，即所有相关联的值都会反向。
     - alternate-reverse：动画从反向开始，再正反方向交替运动，运动方向始终与alternate定义的相反。（FF14.0.1以下不支持）

  - `animation-fill-mode`

    > 检索或设置对象动画时间之外的状态。
    
     - none：默认值。不设置对象动画之外的状态
     - forwards：结束后保持动画结束时的状态，但当animation-direction为0，则动画不执行，持续保持动画开始时的状态
     - backwards：结束后返回动画开始时的状态
     - both：结束后可遵循forwards和backwards两个规则。

  - `animation-iteration-count`   > 自定义动画执行次数。设置值可为0或正整数；infinite：无限循环。

    ```html
      <style>
        .demo_box{
          -webkit-animation:f1 2s 0.5s forwards linear;
          -moz-animation:f1 2s 0.5s forwards linear;
          position:relative;
          left:10px;
          width:100px;
          height:100px;
          margin:10px 0;
          overflow:hidden;
        }
        .one{ 
            -webkit-animation-iteration-count:1;
            -moz-animation-iteration-count:1;
        }
        .infinite{
            -webkit-animation-iteration-count:infinite;
            -moz-animation-iteration-count:infinite;
        }
        .some{
            -webkit-animation-iteration-count:2,1;
            -moz-animation-iteration-count:2,1;
        }

        @-webkit-keyframes f1{
            0%{left:10px;}
            100%{left:500px;}
        }
        @-moz-keyframes f1{
            0%{left:10px;}
            100%{left:500px;}
        }                  
      </style>
      <div class="demo_box one">动画执行1次</div>
      <div class="demo_box infinite">动画执行无数次</div>
      <div class="demo_box some">这个不知道</div>  
    ```
    
  - `animation-play-state`
    >  检索或设置对象动画的状态。running：运动；paused：暂停。

     - 实例：

    ```html
    <style>
      .play-state{
        -webkit-animation:f1 2s 0.5s 2  linear forwards alternate;
        -moz-animation:f1 2s 0.5s 2  linear forwards alternate;
        position:relative;
        left:10px;
        width:100px;
        height:100px;
        margin:10px 0;
        overflow:hidden;
      }
      .play-state:hover{ 
          -webkit-animation-play-state:paused;
          -moz-animation-play-state:paused;
      }
      @-webkit-keyframes f1{
          0%{left:10px;}
          100%{left:500px;}
      }
      @-moz-keyframes f1{
          0%{left:10px;}
          100%{left:500px;}
      }   
    </style>
    <div class="demo_box play-state">鼠标移过来我就停，移走就运动，好听话哦！</div>    
    ```

## 伪元素

  - 常见伪类：`:hover、:link、:active、:target、:not()、:focus`

  - 常见伪元素：`::first-letter、::first-line、::before、::after、::section`

### `::before & ::after`

  > `content` 属性，必须有值，至少为空，用来定义插入的内容。其值可取下列值：

  - `string`：使用引号包一段字符串，将会向元素内容中添加字符串。
    
  - `attr()`：通过`attr()`调用当前元素的属性，比如: `attr(data)`获取自定义属性`data-*`的值

  - `url()/uri()`：

  - `counter()`

- `::section`

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


- 移动端css初始化

  [github源码](https://github.com/benfrain/app-reset/blob/master/app-reset.css?utm_source=caibaojian.com)

  ```html
    <style>

    /*Hat tip to @thierrykoblentz for this approach: https://css-tricks.com/inheriting-box-sizing-probably-slightly-better-best-practice/ */
    html {
        box-sizing: border-box;
    }

    /*Yes, the universal selector. No, it isn't slow: https://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/*/
    * {
        /* Later browsers can be more easily reset with `all: unset`. However, further declarations on these elements follow for older browsers. REMEMBER accessibility for outlines etc. This undoes a LOT of default UA styling, use with EXTREME caution!! */
        all: unset;
        /*This prevents users being able to select text. Stops long presses in iOS bringing up copy/paste UI for example. Note below we specifically switch user-select on for inputs for the sake of Safari. Bug here: https://bugs.webkit.org/show_bug.cgi?id=82692*/
        user-select: none;
        /*This gets -webkit specific prefix as it is a non W3C property*/
        -webkit-tap-highlight-color: rgba(255,255,255,0);
        /*Older Androids need this instead*/
        -webkit-tap-highlight-color: transparent;
        /* Most devs find border-box easier to reason about. However by inheriting we can mix box-sizing approaches.*/
        box-sizing: inherit;
    }

    *:before,
    *:after {
        box-sizing: inherit;
    }

    /* Switching user-select on for inputs and contenteditable specifically for Safari (see bug link above)*/
    input[type],
    [contenteditable] {
      user-select: text;
    }

    body,
    h1,
    h2,
    h3,
    h4,
    h5,
    h6,
    p {
        /*We will be adding our own margin to these elements as needed.*/
        margin: 0;
        /*You'll want to set font-size as needed.*/
        font-size: 1rem;
        /*No bold for h tags unless you want it*/
        font-weight: 400;
    }

    /* 
    Thanks to L. David Baron for this:
    https://twitter.com/davidbaron/status/794138427952222210 */
    base, basefont, datalist, head, meta, script, style, title,
    noembed, param, template {
        display: none;
    }

    a {
        text-decoration: none;
        color: inherit;
    }

    /*No bold for b tags by default*/
    b {
        font-weight: 400;
    }

    /*Prevent these elements having italics by default*/
    em,
    i {
        font-style: normal;
    }

    /*IMPORTANT: This removes the focus outline for most browsers. Be aware this is a backwards accessibilty step! Mozilla (i.e. Firefox) also adds a dotted outline around a tags and buttons when they receive tab focus which I haven't found an unhacky way of removing.*/
    a:focus,
    button:focus {
        outline: 0;
    }

    button {
        appearance: none;
        background-color: transparent;
        border: 0;
        padding: 0;
    }

    input,
    fieldset {
        appearance: none;
        border: 0;
        padding: 0;
        margin: 0;
        /*inputs and fieldset defaults to having a min-width equal to its content in Chrome and Firefox (https://code.google.com/p/chromium/issues/detail?id=560762), we may not want that*/
        min-width: 0;
        /*Reset the font size and family*/
        font-size: 1rem;
        font-family: inherit;
    }

    /* For IE, we want to remove the default cross ('X') that appears in input fields when a user starts typing - Make sure you add your own! */
    input::-ms-clear {
        display: none;
    }

    /*This switches the default outline off when an input receives focus (really important for users tabbing through with a keyboard) so ensure you put something decent in for your input focus instead!!*/
    input:focus {
        outline: 0;
    }

    input[type="number"] {
        /*Mozilla shows the spinner UI on number inputs unless we use this:*/
        -moz-appearance: textfield;
    }

    /*Removes the little spinner controls for number type inputs (WebKit browsers/forks only)*/
    input[type="number"]::-webkit-inner-spin-button,
    input[type="number"]::-webkit-outer-spin-button {
        appearance: none;
    }

    /*SVG defaults to inline display which I dislike*/
    svg {
        display: inline-flex;
    }

    img {
        /*Make images behave responsively. Here they will scale up to 100% of their natural size*/
        max-width: 100%;
        /*Make images display as a block (UA default is usually inline)*/
        display: block;
    }

    /*Removes the default focusring that Mozilla places on select items. From: http://stackoverflow.com/a/18853002/1147859 
    Ensure you set `#000` to the colour you want your text to appear */
    select:-moz-focusring {
        color: transparent;
        text-shadow: 0 0 0 #000;
    }

    </style>
  ```

## `flexbox`

  
