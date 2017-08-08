# book.json

> book.json 常用配置

```json
{
    "title": "前端知识",
    "description": "一个小学生的学习笔记",
    "author": "snoopy X",
    "output.name": "site",
    "language": "zh-hans",
    "gitbook": "3.2.2",
    "root": ".",
    "structure": {
        "readme": "README.md"
    },
    "links": {
        "sidebar": {
            "Home": "https://github.com/SnoopyoFifi"
        }
    },
    "plugins": [
        "-lunr",
        "-search",
        "-highlight",
        "-livereload",
        "-sharing",
        "sharing-plus@0.0.2",
        "search-plus@^0.0.11",
        "simple-page-toc@^0.1.1",
        "github@^2.0.0",
        "github-buttons@2.1.0",
        "edit-link@^2.0.2",
        "-disqus@^0.1.0",
        "prism@^2.1.0",
        "prism-themes@^0.0.2",
        "advanced-emoji@^0.2.1",
        "anchors@^0.7.1",
        "include-codeblock@^3.0.2",
        "ace@^0.3.2",
        "emphasize@^1.1.0",
        "katex@^1.1.3",
        "splitter@^0.0.8",
        "mermaid@^0.0.9",
        "tbfed-pagefooter@^0.0.1",
        "expandable-chapters-small@^0.1.7",
        "sectionx@^3.1.0",
        "local-video@^1.0.1",
        "sitemap-general@^0.1.1",
        "anchor-navigation-ex@0.1.8",
        "favicon@^0.0.2",
        "todo@^0.1.3",
        "3-ba@^0.9.0",
        "anchor-navigation-ex"
    ],
    "pluginsConfig": {
        "theme-default": {
            "showLevel": true
        },
        "prism": {
            "css": [
                "prism-themes/themes/prism-base16-ateliersulphurpool.light.css"
            ]
        },
        "github": {
            "url": "https://github.com/SnoopyoFifi"
        },
        "github-buttons": {
            "repo": "SnoopyoFifi/pupil",
            "types": [
                "star"
            ],
            "size": "small"
        },
        "include-codeblock": {
            "template": "ace",
            "unindent": true,
            "edit": true
        },

        "sharing": {
          "douban": true,
          "facebook": false,
          "google": true,
          "hatenaBookmark": false,
          "instapaper": false,
          "line": false,
          "linkedin": false,
          "messenger": false,
          "pocket": false,
          "stumbleupon": false,
          "twitter": false,
          "viber": false,
          "vk": false,
          "qzone": true,
          "qq": true,
          "weibo": true,
          "whatsapp": false,
          "all": [
              "douban", "qzone", "qq",
              "weibo", "google"
          ]
        },
        "tbfed-pagefooter": {
            "copyright": "Copyright © SnoopyoFifi.com 2017",
            "modify_label": "该文件修订时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        },
        "3-ba": {
            "token": "ff100361cdce95dd4c8fb96b4009f7bc"
        },
        "simple-page-toc": {
            "maxDepth": 3,
            "skipFirstH1": true
        },
        "edit-link": {
            "base": "https://github.com/SnoopyoFifi/gitbook-use/edit/master",
            "label": "Edit This Page"
        },
        "sitemap-general": {
            "prefix": "http://gitbook.zhangjikai.com"
        },
        "anchor-navigation-ex": {
            "float": {
                "showLevelIcon": true,
                "level1Icon": "fa fa-fighter-jet",
                "level2Icon": "fa fa-fighter-jet",
                "level3Icon": "fa fa-fighter-jet"
            }
        },
        "sectionx": {
            "tag": "b"
        },
        "favicon": {
            "shortcut": "favicon.ico",
            "bookmark": "favicon.ico"
        }

    }
}
```

## title

> "title": "GitBook 使用教程", // 设置书本的标题

## description

> "description": "记录 GitBook 的配置和一些插件的使用",  // 简单的书本描述

## author

> "author": "snoopy.X", // 作者信息

## language

> "language": "zh-hans", // gitbook使用的语言，配置使用简体中文
>
> en, ar, bn, cs, de, en, es, fa, fi, fr, he, it, ja, ko, no, pl, pt, ro, ru, sv, uk, vi, zh-hans, zh-tw

## gitbook

> "gitbook": "3.2.2", // 指定gitbook的版本

## root

> "root": ".", // 指定存放Gitbook文件的根目录

## structure

> 指定 Readme、Summary、Glossary 和 Languages 对应的文件名，下面是这几个文件对应变量以及默认值：

| 变量                    | 含义和默认值                                   |
| :-------------------- | :--------------------------------------- |
| `structure.readme`    | `Readme file name (defaults to README.md)` |
| `structure.summary`   | `Summary file name (defaults to SUMMARY.md)` |
| `structure.glossary`  | `Glossary file name (defaults to GLOSSARY.md)` |
| `structure.languages` | `Languages file name (defaults to LANGS.md)` |

## links

> 在侧边栏添加链接

![title](title.jpg)

 

 ## styles

> 自定义页面样式， 默认情况下各generator对应的css文件

```
"styles": {
    "website": "styles/website.css",
    "ebook": "styles/ebook.css",
    "pdf": "styles/pdf.css",
    "mobi": "styles/mobi.css",
    "epub": "styles/epub.css"
}
```

> 例如:使`<h1> <h2>`标签有下边框， 可以在`website.css`中设置

```
h1 , h2{
    border-bottom: 1px solid #EFEAEA;
}
```

## plugins

> 配置使用的插件

```
"plugins": [
    "disqus"
]
```

> 添加新插件之后需要运行`gitbook install`来安装新的插件

Gitbook默认带有5个插件：

- highlight
- search
- sharing
- font-settings
- livereload

> 如果要去除自带的插件， 可以在插件名称前面加`-`

```
"plugins": [
    "-search"
]