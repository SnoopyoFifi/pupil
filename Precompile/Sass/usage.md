# usage

```scss
// _base.scss
// 初始化待完善。。。
  // 使用`utf-8`字符集
  @charset "utf-8";

  // 导入`scss`文件
  @import "../mixin/searchbtn";
  @import "../mixin/tabstyle";

  // 定义常用变量
  $main-color: #33b371;   // 主色调
  $width-small: 1024px;   // 小屏
  $width-medium: 1280px;  // 中屏
  $width-large: 1366px;   // 大屏
  $width-greatest: 1680px;// 超大屏
  
  html,body {
    height: 100%;
    width: 100%;
    background: transparent;
  }
  
  body,h1,h2,h3,h4,h5,h6,p,div,ul,ol,dl,li,dt,dd{
    margin: 0;
    padding: 0;
    list-style: none;
  }
  i, em, s, b {
    font-style: normal;
    font-weight: normal;
    text-decoration: none;
  }
  a {
    text-decoration: none;
    &:link {
      text-decoration: none
    }
    &:visited {
      text-decoration: none
    }
    &:hover {
      text-decoration: none
    }
    &:active {
      text-decoration: none
    }
  }

  input,img {
    border: 0 none;
    outline-style: none;
    padding: 0;
    margin: 0;
    vertical-align: bottom;
    font-family: "Microsoft yahei";
  }s
  input,button,textarea  {
    border: 0 none;
    outline-style: none;
    background-color: #fff;
    font-family: "Microsoft yahei";
  }

  .fl {
    float: left;
  }
  .fr {
    float: right;
  }
  .clearfix:after {
    content: "";
    height: 0;
    line-height: 0;
    display: block;
    clear: both;
    visibility: hidden;
  }
  .clearfix {
    zoom: 1;
  }

  // 单行隐藏
  .one_txt_cut{
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }

  // 两行隐藏
  .two_txt_cut {
    text-overflow: -o-ellipsis-lastline;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }

  // 多行隐藏
  .more_txt_cut {
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
    overflow: hidden;
  }

  // 禁止点击
  .events-disabled {
    pointer-events: none;
    cursor: default;
    opacity: 0.6;
  }

  // 禁止选择
  .user-select {
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }

  // 版心
  .w {
    width: 988px;
    margin: 0 auto;
    text-align: center;
    // @media screen and (max-width:  $width-large)  {
    //   width: 790px !important;
    // }
    @media screen and (max-width:  $width-medium)  {
      width: 790px !important;
    }
    @media screen and (max-width: $width-small)  {
      width: 790px !important;
    }
  }
  
  // html5
  article, aside, dialog, footer, header, section, footer, nav, figure, menu {
    display:block
  };


```