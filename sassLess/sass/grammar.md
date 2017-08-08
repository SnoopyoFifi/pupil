# grammer

> [Sass 基础教程：](http://www.sasschina.com/guide/) 

## 使用变量

```scss
  $main-color: #f90;
  $basic-border: 1px solid $main-color;  // 变量中可以在应用其他变量
  $plain-font: "Myriad Pro","Arial","Helvetica Neue","sans-serif";

  nav {
    $width: 100px;  // {} 规则块 内的变量是独立的
    width: $width;
    color: $main-color;
    border: $basic_border; // 中划线定义 可以用下划线引用
  }
```

## 默认变量值
> !default 表示如果这个变量被声明赋值了，那就用它声明的值，否则就用这个默认值

```scss
  $fancybox-width: 400px !default;
  .fancybox {
    width: $fancybox-width;
  }
```

## 嵌套

```scss
  <!-- 后代选择器嵌套写法 -->
  #content {
    background-color: #f5f5f5;
    article {
      h1 {
        color: #333;
      }
      p {
        margin-bottom: 1.4em;
      }
    }
  }
  
  <!-- a:hover --> a {&:hover} -->
  article {
    color: blue;
    &:hover {
      color: red;
    }
  }

  <!-- ie添加类名，编写特殊样式 -->
  #content aside {
    color: red;
    body.ie & { color: green; }
  }

  <!-- 并集选择器嵌套写法 -->
  .container {
    h1, h2, h3 {
      margin-bottom: .8em;
    }
  }
  nav, aside {
    a {
      color: blue;
    }
  }

  <!-- 子组合选择器和同层组合选择器： -->
  <!--  + 同层相邻组合选择器 选择 header 后面紧跟的 p元素  -->
  header + p {
    font-size: 1.1em;
  }
   <!-- ~ 同层全体组合选择器 选择 article 后同层的 article 元素 -->
  article ~ article {
    border-top: 1px dashed #ccc;
  }
  <!-- > 子组合选择器 选择一个元素的直接子元素  -->
  article > section {
    border: 1px solid #ccc;
  }

  article {
    ~article { border-top: 1px dashed #ccc; }
    > section { background-color: #eee; }
    dl > {
      dt { color: #333; }
      dd { color: #555; }
    }
    nav + &{ margin-top: 0; }
  }

  <!-- 嵌套属性  -->
  nav {
    border: {
      style: solid;
      width: 1px;
      color: #ccc;
    }
  }
  nav {
    border: 1px solid #ccc {
      left: 0px;
      right: 0px;
    }
  }

```

## 导入
### 导入sass文件
> sass局部文件，以下划线开头命名，这样sass就不会在编译时单独编译这个文件输出css，而把这个文件用作导入;
> 如：想导入 themes/_night-sky.scss这个局部文件里的变量，在样式表中写法为： @import "themes/night-sky"

### 嵌套导入
> 生成的结果和直接在选择器内写 _blue-theme.scss 文件的内容完全一样；
> 通过嵌套导入只对站点中某一特定区域运用某种颜色主题或者其他通过变量配置的样式。

```scss
.blue-theme {@import "blue-theme";}
```

### 原生的css导入 
> 将原生css文件改名为.scss后缀，即可直接导入 

## 混合器

> @mixin 标识给大段样式赋予名称，@include 便可以引用这个名字重用这段样式
```scss
  @mixin rounded-corners {
    -moz-border-radius: 5px;
    -webkit-border-radius: 5px;
    border-radius: 5px;
  }
  .notice {
    background-color: green;
    border: 2px solid #000;
    @include rounded-corners;
  }
```

> 使用场景
> 能找到一个很好的短名字来描述这些属性修饰的样式，那么往往能构造一个合适混合器。类似于html的类名
```scss
  <!-- 混合器中的css规则 -->
  @mixin no-bullets {
    list-style: none;
    li {
      list-style-image: none;
      list-style-type: none;
      margin-left: 0px;
    }
  }
  ul.plain {
    color: #444;
    @include no-bullets;
  }

  <!-- 给混合器传参 -->
  @mixin link-colors($normal, $hover, $visited) {
    color: $normal;
    &:hover { color: $hover; }
    &:visited { color: $visited; }
  }
  a {
    @include link-colors(blue, red, green);
  }
  a {
    @include link-colors (
      $normal: blue,
      $visited: green,
      $hover: red
    )
  }
  <!-- 默认参数值 -->
  @mixin link-colors (
    $normal,
    $hover: $normal,
    $visited: $normal
  )
  {
    color: $normal;
    &:hover { color: $hover; }
    &:visited { color: $visited; }
  }
  a {
    @include link-colors(red);
  //  $hover 和 $visited 也会被自动赋值为red
  }

```

## 静默注释

```scss
  body {
    color /* 这块注释内容不会出现在生成的css中 */: #333;
    padding: 0 /* 这块注释内容也不会出现在生成的css中 */ 1px;
  }
  body {
    color: #333; // 这种注释内容不会出现在生成的css文件中
    padding: 0; /* 这种注释内容会出现在生成的css文件中 */
  }

```

## 使用选择器继承来精简css

```scss
  .error {
    border: 1px solid red;
    background-color: #fdd;
  }
  .seriousError {
    @extend .error;
    border-width: 3px;
  }`
```

>  .seriousError 不仅会继承.error 自身所有的样式，任何跟.error有关的组合选择器样式也会被.seriousError 以组合选择器的形式继承 

```scss
  .error a { // 应用到.seriousError a
    color: red;
    font-weight: 700;
  }
  h1.error { // 应用到h1.seriousError
    font-size: 1.2rem;
  }
```
