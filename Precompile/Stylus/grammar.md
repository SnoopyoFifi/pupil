# grammer
[stylus中文文档](http://www.zhangxinxu.com/jq/stylus/)

## 选择器
  * 缩排
    > 使用缩排和凹排来代替花括号以及冒号
    
    ```
      body 
        color white
    ```

  * 规则集
    > 允许使用逗号为多个选择器同时定义属性(使用新行是同样的效果)

    ```
      ul, li 
        list-style none

      ul
      li 
        list-style none
    ```

  * 父级引用
    > 字符`&`指向父选择器
    
    ```
      textarea
      input
        color #fff
        &:hover 
          color hotpink
    ```

  * 消除歧义
    > 在函数中`padding -n`此类表达式可能引起歧义，需用括号包裹
      
    ```
      pad(n)
        padding (-n)
      body 
        pad(5px)
    ```
    
## 变量
  * 表达式变量
    > 可以指定表达式为变量，变量名可能包括`$`字符
    
    ```
      font-size = 14px
      html 
        font font-size "microsoft yahei"

      $font-size = 14px
      body 
        font $font-size "microsoft yahei"
    ```
  
  * 属性查找
    > 不需要分配值给变量就可以定义引用属性，简单的前置`@`在属性名前来访问其对应的值
    
    ```
      #logo
        position: absolute
        top: 50%
        left: 50%
        width: w = 150px
        height: h = 80px
        margin-left: -(w/2)
        margin-top: -(h/2)

      #logo
        position: absolute
         top: 50%
        left: 50%
        width: 150px
        height: 80px
        margin-left: -(@width/2)
        margin-right: -(@height/2)
    ```

    > 属性会"向上冒泡"查找堆栈直到被发现，或者返回null
    
    ```
      body
        color: red
        ul
          li
            color: blue
              a 
                background-color: @color
    ```
    
## 插值
  * 属性插值
    > 通过使用`{}`来插入值
    
    ```
      vendor(prop, args)
        -webkit-{prop} args
        -moz-{prop} args
        {prop} args
      border-radius()
        verdor('border-radius',arguments)

      button
        border-radius 1px 2px / 3px 4px
    ```

  * 选择器插值
    > 插值也可以在选择器上起作用,如: 指定表格前5行的高度
    
    ```
      table
        for row in 1 2 3 4 5
          tr:nth-child({row})
            height: 10px * row
    ```

## 混入书写(Mixins)
  * 混入
    > 混入和函数定义方法一致，但是应用不同，当下面`border-radius()`选择器中调用的时候，属性会被扩展并复制在选择器中
    
    ```
      border-radius(n)
        -webkit-border-radius n
        -moz-border-radius n
        border-radius n
      form input[type=button]
        border-radius(5px)
        // border-radius 5px
      
      // 利用arguments这个局部变量，传递可以包含多值的表达式
      border-radius(n)
        -webkit-border-radius arguments
        -moz-border-radius arguments
        border-radius arguments
      from input[type=button]
        border-radius 1px 2px / 3px 4px
    ```
    
  * 父级引用
    > 混合书写可以利用父级引用字符`&`

    ```
      stripe(even = #fff, odd= #eee)
        tr
          background-color odd
          &.even
          &:nth-child(even)
            background-color even

      table
        strip()
        td 
          padding 4px 10px
      table#users
        stripe(#33b371, #ccc)
        td 
          color white
    ```
  
  * 混合书写中的混合书写
    > 混合书写可以利用其它混合书写
    
    ```
      inline-list()
        li 
          display inline
      comma-list()
        inline-list()
        li
          &:after
            content ', '
          &:last-child:after
            content ''
      ul 
        comma-list()
    ```

## 方法
  * 函数返回值
    > `Stylus`中内置了强大的函数定义，其定义与混入相同，但可以返回值
    
    ```
      add(a, b)
        a + b

      html
        font-size add(10px, 4)
    ```

  * 默认参数
    > 可选参数往往有个默认给定的表达式，也可以使用函数调用作为默认值
    
    ```
      add(a, b = a)
        a + b
      add(10, 5)
      // 15
      add(10)
      // 20

      add(a, b = unit(a, px))
        a + b
    ```
  
  * 函数体
    > 通过内置`unit()`把单位都变成`px`，所以可以无视单位进行参数赋值

    ```
      add(a, b = a)
        a = unit(a, px)
        b = unit(b, px)
        a + b
      
      add(15%, 10deg)
      // 25
    ```
    
  * 多个返回值
    > 变量可以赋多个值，函数也可返回多个，同时注意返回值标识符(加括号或者`return`)
    
    ```
      sizes = 15px 10px
      sizes[0]
      // 15px

      sizes()
        15px 10px
      sizes()[0]

      swap(a, b)
        b a

      swap(a, b)
        (b a)
      swap(a, b)
        return b a
    ```

  * 条件
    > 例如:创建一个函数用来决定参数是否是字符串
    
    ```
      stringish(val)
        if val is a 'string' or val is a 'ident'
          yes
        else
          no

      stringish('snoopy') == yes
      stringish(snoopy) == yes
      stringish(0) == no
    ```

  * 别名
    > 给函数起个别名
    
    ```
      plus = add

      plus(1, 3)
    ```

  * 变量函数
    > 可以把函数当做变量传递到新的函数中
    
    ```
      invoke(a, b, fn)
        fn(a, b)

      add(a, b)
        a + b

      body
        padding invoke(5, 10, add)
        padding invoke(5, 10, sub)

      body{
        padding: 15;
        padding: -5;  
      }    
    ```

  * 参数
    > `arguments`是所有函数体都有的局部变量，包含传递的所有参数

    ```
      sum()
        n = 0
        for num in arguments
          n = n + num

      sum(1, 2, 3, 4)
    ```

## 关键字参数
  * 关键字参数
    > 允许根据相关参数名引用参数
  
    ```
      body {
        color: rgba(255, 200, 100, 0.5);
        color: rgba(red: 255, green: 200, blue: 100, alpha: 0.5);
        color: rgba(alpha: 0.5, blue: 100, red: 255, 200);
        color: rgba(alpha: 0.5, blue: 100, 255, 200);
      }

      p(rgba)
      inspect: rgba(red, green, blue, alpha)
    ```

## 注释
  * 单行注释
    > 跟JavaScript一样，双斜杠，CSS中不输出。
    
    ```
      // 我是注释!
      body
        padding 5px // 蛋疼的padding`
    ```

  * 多行注释
    > 多行注释看起来有点像CSS的常规注释。然而，它们只有在compress选项未启用的时候才会被输出。
    
    ```
      /*
       * 给定数值合体
       */
      add(a, b)
        a + b
    ```


  * 多行缓冲注释
    > 跟多行注释类似，不同之处在于开始的时候，这里是/*!. 这个相当于告诉Stylus压缩的时候这段无视直接输出。
    
    ```    
      /*!
       * 给定数值合体
       */

      add(a, b)
        a + b
    ```

## `@import`
  * 字面量`css`
    >任何`.css`扩展的文件名将作用为字面量

    ```
      @import "reset.css"
    ```

  * `Stylus`导入
    > 当使用`@import`没有`.css`扩展是，会被认为是`Stylus`片段

## `@media`
  * `@media`
    > `@media`工作原理和在常规`CSS`中一样，但是，要使用`Stylus`的块状符号
  
    ```
      @media print
        #header
        #footer
          display none

      @media print {
        #header,
        #footer {
          display: none;
        }
      }
    ```

## `@font-face`
  * 自定义字体
    > `@font-face`跟其在`CSS`中作用表现一样，在后面简单地添加个块状属性即可
    
    ```
      @font-face
        font-family Fifi
        font-style normal
        src url(fonts/**/*.ttf)

      .infifi
        font-family fifi
    ```

## `@keyframes`
  * 关键帧
    > `Stylus`支持`@keyframes`规则，当编译的时候转换成 `@-webkit-keyframes` 

    ```
      @keyframes pulse
      0%
        background-color red
        opacity 1.0
        -webkit-transform scale(1.0) rotate(0deg)
      33%
        background-color blue
        opacity 0.75
        -webkit-transform scale(1.1) rotate(-5deg)
      67%
        background-color green
        opacity 0.5
        -webkit-transform scale(1.1) rotate(5deg)
      100%
        background-color red
        opacity 1.0
        -webkit-transform scale(1.0) rotate(0deg)
    ```

  * 扩展
    > 使用`@keyframe`，通过`vendors`变量，会自动添加私有前缀(webkit、moz、official)
    
    ```
      @keyframes foo {
        from {
          color: black
        }
        to {
          color: white
        }
      }
      
      // 解析为
      @-moz-keyframes foo {
        0% {
          color: #000;
        }

        100% {
          color: #fff;
        }
      }
      @-webkit-keyframes foo {
        0% {
          color: #000;
        }

        100% {
          color: #fff;
        }
      }
      @keyframes foo {
        0% {
          color: #000;
        }

        100% {
          color: #fff;
        }
      }
  
      // 使用了vendors
      vendors = official
      @keyframes foo {
        from {
          color: black
        }
        to {
          color: white
        }
      }
      // 解析为
      @keyframes foo {
        0% {
          color: #000;
        }

        100% {
          color: #fff;
        }
      }
    ```
    
## `@extend`
  * 继承
    > `Stylus`的`@extend`指令受`SASS`实现的启发，目前`Stylus`与`SASS`不同之处在于`SASS`不允许`@extend`嵌套选择器。
    
    ```
      .message {
        padding: 10px;
        border: 1px solid #eee;
      }
      .warning {
        @extend .message;
        color: #E2E21E;
      }

      // @extend级联写法
      red = #E33E1E
      yellow = #E2E21E
      .message
        padding: 10px
        font: 14px Helvetica
        border: 1px solid #eee
      .warning
        @extends .message
        border-color: yellow
        background: yellow + 70%
      .error
        @extends .message
        border-color: red
        background: red + 70%
      .fatal
        @extends .error
        font-weight: bold
        color: red

      // 允许嵌套选择器
      form
      input[type=text]
        padding: 5px
        border: 1px solid #eee
        color: #ddd
      textarea
        @extends form input[type=text]   
        padding: 10px
    ```


## 运算符

## 内置方法 

## 其余参数

## 条件

## 迭代

## `url()`
