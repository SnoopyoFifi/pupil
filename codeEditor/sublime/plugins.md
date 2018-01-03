# 常用插件介绍

1. [插件官网](https://packagecontrol.io/)

2. 快捷语法： `Emmet`

3. markdown 相关插件:
  - MarkdownEditing
  - Markdown Extended
  - Markdown Preview(alt + m)
  - MarkdownLivePreview
  - Markdown HTML Preview(ctrl+shift+m)
  - MarkdownLight
  - MarkdownHighlighting

4. md预览、生成： `htmlOmniMarkupPreviewer`
  - Ctrl+Alt+O: Preview Markup in Browser.
  - Ctrl+Alt+X: Export Markup as HTML.
  - Ctrl+Alt+C: Copy Markup as HTML.

5. 丰富侧边拦：`SideBarEnhancements`

6. 文件图标icon： A File Icon

7. 让输入法跟随；`IMESupport`

8. 打开命令行工具(cmder): `Terminal`
  - 配置终端路径
    * 去package setting 找到Terminal的user setting
        { 
          "terminal": "D:/download/cmder/Cmder.exe", 
          "parameters": ["/START", "%CWD%"] 
        } 
  - 当前目录打开：ctrl+shift+t
  - 当前项目根目录打开：ctrl+alt+shift+t

9. 代码格式化 

  - `HTML-CSS-JS Prettify`

    - "selector_separator_newline": false： 不需要每个CSS选择器单独占一行
    - "allowed_file_extensions": ["..这是老的，新增在-->","vue"],：将vue的组件当成html来进行格式化
    - 默认快捷键：`Ctrl + Shift + H`

  - `Prettify Code` 

    - 默认快捷键：`Ctrl + Shift + r + p` 

  - `JsFormat`

    - js代码格式化

    - 默认快捷键：`Ctrl + Alt + F`

10. 函数注释解析： `DocBlockr`

  ```js
  /**
   * 这里的注释内容【会】被压缩工具压缩
   */

  /*！
   * 这里的注释内容【不会】被压缩工具压缩
   * 与上面一个注释块不同的是，第2个*换成了!
   */
  ```

11. 语法高亮

   - `JavaScript Next`

     - js高亮显示

   - `CSS3`

     - css3语法高亮

12. CSS属性排序： `CSScomb` 

   - 默认快捷键：`Ctrl + Shift + C`

13. 快速查找css类样式：`Goto-CSS-Declaration`

   > 安装后按快捷键 `win + Alt + .` 跳转到 css 文件该 class 的声明处，方便修改查看，注意对应的css文件要同时打开才行

14. sublime静态文件服务： `sublimeServer`

   - 在setting里面可以修改服务器的端口号
   - 启动服务后可以复制地址到手机端，把localhost改成电脑IP即可通过手机查看效果

15. 匹配括号，引号和 html 标签：`Bracket Highlighter`　　

   > 对于很长的代码很有用。安装好之后，不需要设置插件会自动生效

16. 快速生成文件模板：`SublimeTmpl` 

   > 新建文件模板，先自定义文件模板在templates文件夹里，再打开Default ( Windows).sublime-keymap、Default.sublime-commands、Main.sublime-menu、SublimeTmpl.sublime-settings这四个文件照着里面的格式自定义想要新建的类型

17. 主题管理：`Themr`

   > 切换主题的时候，不用自己修改配置文件了，用这个可以方便的切换主题

18. 搭建Python IDE：`Anaconda`

19. 支持 GBK, BIG5, EUC-KR, EUC-JP, Shift_JIS 等编码：`ConvertToUTF8`

20. 自动提示补齐代码：`Sublime​Linter`

   > 支持 `JavaScript、Python、PHP` 等等常用语言。

21. 中文翻译

   - `ChineseTranslator
     - 默认快捷键：`Ctrl+Shift+C`

   - `ctranslator`
     - 默认快捷键：`CTRL + Alt + H`：

22. 调用外部软件打开pdf,.zip等文件： Non-Text-Files

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


23. Typescript

[Typescript](http://www.interoperabilitybridges.com/media/155452/typescript_support_for_sublime_text.zip)

24. **auto Prefixer**
  
  > Prefixr，CSS3 私有前缀自动补全插件，显然也很有用哇