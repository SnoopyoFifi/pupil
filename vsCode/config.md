# 常用配置

# 基本配置

![这里写图片描述](http://img.blog.csdn.net/20170223212332364?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3JwZXI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![这里写图片描述](http://img.blog.csdn.net/20170223212842090?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3JwZXI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

------

# 快捷键自定义（Ctrl+K Ctrl + S）

![这里写图片描述](http://img.blog.csdn.net/20170223213149376?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3JwZXI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

- 那个`when`支持条件表达式返回一个布尔值
- 支持的快捷键组合快捷键的键值 
  ![这里写图片描述](http://img.blog.csdn.net/20170223213903716?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3JwZXI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

[**更加详细的可以阅读这里：**](https://code.visualstudio.com/docs/customization/keybindings) 你可以看到when的具体范围解释，非常详细。。这里我就不一一列举出来了。。。直接在链接的文章内搜索`when Clause Contexts`

------

# 代码片段

进入代码片段自定义有两种方式： 
\1. 【菜单栏->文件->首选项->用户代码片段】 
\2. 全局命令【ctrl+shift + p => snippet】

VSCODE的代码片段支持30多种编程语言，所以也免了代码片命名唯一和全局生效【所有文件】的尴尬

这里就选择一个sass的说下，内部有这么一段注释嗯

```
{
    /*
     // Place your snippets for Sass here. Each snippet is defined under a snippet name and has a prefix, body and 
     // description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
     // $1, $2 for tab stops, ${id} and ${id:label} and ${1:label} for variables. Variables with the same id are connected.
     // Example:
     "Print to console": {
        "prefix": "log",
        "body": [
            "console.log('$1');",
            "$2"
        ],
        "description": "Log output to console"
    }
*/
    "utf-8": {
        "prefix": "utf-8",
        "body": [
            "@charset 'UTF-8';"
        ],
        "description": "插入文件编码"
    },
    "impout": {
        "prefix": "impcfg",
        "body": [
            "@import '../../../assets/scss_styles/custom_scss/_custom-export.scss';"
        ],
        "description": "插入配置文件"
    },
    "toRem": {
        "prefix": "rem",
        "body": [
            "toRem($0)"
        ],
        "description": "插入px转换函数"
    },
        "removeDedault": {
        "prefix": "ra",
        "body": [
            "@include remove-a-default-behavior"
        ],
        "description": "移除a的下划线"
    }

}123456789101112131415161718192021222324252627282930313233343536373839404142434445
```

直接给效果图再来解释比较好理解 
![这里写图片描述](http://img.blog.csdn.net/20170223215407348?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3JwZXI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

- `toRem`: 只是一个单纯的描述

- `prefix`: 是触发snippet的简写

- ```
  body
  ```

  : 是展开的代码片段

   

  ​

  - 1,2表示占位符，用于用户展开代码片段所需要替换的，也可以写成`${1:label}`键值对的方式

- `description` : 用户你在输出snippet之前，方便自己识别的注释，而不用强行记忆那些简写的