# 常用插件介绍

-  [插件官网](https://packagecontrol.io/)

1. 丰富侧边拦：SideBarEnhancements

2. 中文翻译： ChineseTranslator（Ctrl+shift+c）/ ctranslator(CTRL + Alt + H )

3. markdown:
  - MarkdownEditing
  - Markdown Extended
  - Markdown Preview(alt + m)
  - MarkdownLivePreview
  - Markdown HTML Preview(ctrl+shift+m)
  - MarkdownLight
  - MarkdownHighlighting

4. OmniMarkupPreviewer
  - Ctrl+Alt+O: Preview Markup in Browser.
  - Ctrl+Alt+X: Export Markup as HTML.
  - Ctrl+Alt+C: Copy Markup as HTML.

5. Emmet

6. Anaconda

7. icon： A File Icon

8. 打开命令行工具(cmder): Terminal
  - 配置终端路径
    * 去package setting 找到Terminal的user setting
        { 
          // window下终端路径 
          “terminal”: “C:\MyAPP\cmder\Cmder.exe”, 
          // window下终端参数 
          “parameters”: [“/START”, “%CWD%”] 
        } 
  - 当前目录打开：ctrl+shift+t
  - 当前项目根目录打开：ctrl+alt+shift+t

9. 快速生成文件模板：SublimeTmpl 

> 新建文件模板，先自定义文件模板在templates文件夹里，再打开Default ( Windows).sublime-keymap、Default.sublime-commands、Main.sublime-menu、SublimeTmpl.sublime-settings这四个文件照着里面的格式自定义想要新建的类型

10. js代码格式化： JsFormat (Ctrl+Alt+F)
  
11. 让输入法跟随；IMESupport。

12. 调用外部软件打开pdf,.zip等文件： Non-Text-Files
```json
 //  Preferences > Settings - User 中添加如下配置
 "open_externally_patterns": [
        "*.jpg",
        "*.jpeg",
        "*.png",
        "*.gif",
        "*.zip",
        "*.pdf"
    ] 
```

13. 函数注释解析： Doc​Blockr
 
```js
/**
 * 这里的注释内容【会】被压缩工具压缩
 */

/*！
 * 这里的注释内容【不会】被压缩工具压缩
 * 与上面一个注释块不同的是，第2个*换成了!
 */
```

14. js高亮显示： JavaScript Next

15. css3语法高亮：CSS3

16. HTML-CSS-JavaScript 代码格式化： HTML-CSS-JS Prettify

  - "selector_separator_newline": false： 不需要每个CSS选择器单独占一行
  - "allowed_file_extensions": ["..这是老的，新增在-->","vue"],：将vue的组件当成html来进行格式化
  - 默认快捷键：Ctrl+Shift+H

17. CSS属性排序： CSScomb (ctrl+shift+c)
