# 常用插件

> 常用插件及其配置：

## Disqus

>  添加disqus评论

[插件地址](https://plugins.gitbook.com/plugin/disqus)

```
"plugins": [
   "disqus"
],
"pluginsConfig": {
   "disqus": {
       "shortName": "gitbookuse"
   }
}
```

## Duoshuo

> 添加多说

[插件地址](https://plugins.gitbook.com/plugin/duoshuo)

```
{
    "plugins": [
        "duoshuo"
    ],
    "pluginsConfig": {
        "duoshuo": {
            "short_name": "your duoshuo's shortname",
            "theme": "default"
        }
    }
}
```

## Search Plus

> 支持中文搜索, 需要将默认的 `search` 和 `lunr` 插件去掉。

[插件地址](https://plugins.gitbook.com/plugin/search-plus)

```
{
    "plugins": ["-lunr", "-search", "search-plus"]
}
```

## Prism

使用 `Prism.js` 为语法添加高亮显示，需要将 `highlight` 插件去掉。该插件自带的主题样式较少，可以再安装 `prism-themes`插件，里面多提供了几种样式，具体的样式可以参考 [这里](https://github.com/PrismJS/prism-themes)，在设置样式时要注意设置 css 文件名，而不是样式名。

[Prism 插件地址](https://plugins.gitbook.com/plugin/prism)    [prism-themes 插件地址](https://plugins.gitbook.com/plugin/prism-themes)

```
{
    "plugins": [
        "prism",
        "-highlight"
    ],
    "pluginsConfig": {
        "prism": {
            "css": [
                "prism-themes/themes/prism-base16-ateliersulphurpool.light.css"
            ]
        }
    }
}
```

如果需要修改背景色、字体大小等，可以在 `website.css` 定义 `pre[class*="language-"]` 类来修改，下面是一个示例：

```
pre[class*="language-"] {
    border: none;
    background-color: #f7f7f7;
    font-size: 1em;
    line-height: 1.2em;
}
```

## Advanced Emoji

> 支持emoji表情

[emoij表情列表](http://www.emoji-cheat-sheet.com/)
[插件地址](https://plugins.gitbook.com/plugin/advanced-emoji)

```
"plugins": [
    "advanced-emoji"
]
```

使用示例：
```
![:bowtie:](https://assets-cdn.github.com/images/icons/emoji/bowtie.png) ![:smile:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f604.png) ![:laughing:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f606.png) ![:blush:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f60a.png) ![:smiley:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f603.png) ![:relaxed:](https://assets-cdn.github.com/images/icons/emoji/unicode/263a.png)
```

## Github

> 添加github图标， url链接到github上

[插件地址](https://plugins.gitbook.com/plugin/github)

```json
"plugins": [
    "github"
],
"pluginsConfig": {
    "github": {
        "url": "https://github.com/SnoopyoFifi/snoopy-book"
    }
}
```

## Github Buttons

> 添加项目在 github 上的 star，watch，fork情况

[插件地址](https://plugins.gitbook.com/plugin/github-buttons)

```
{
    "plugins": [
        "github-buttons"
    ],
    "pluginsConfig": {
        "github-buttons": {
            "repo": "zhangjikai/gitbook-use",
            "types": [
                "star",
                "watch",
                "fork"
            ],
            "size": "small"
        }
    }
}
```

## Ace Plugin

[插件地址](https://plugins.gitbook.com/plugin/ace)

使 GitBook 支持ace 。默认情况下，line-height 为 1，会使代码显得比较挤，而作者好像没提供修改行高的选项，如果需要修改行高，可以到 `node_modules -> github-plugin-ace -> assets -> ace.js` 中加入下面两行代码 (30 行左右的位置)：

```
editor.container.style.lineHeight = 1.25;
editor.renderer.updateFontSize();
```

不过上面的做法有个问题就是，每次使用 `gitbook install` 安装新的插件之后，代码又会重置为原来的样子。另外可以在 `website.css` 中加入下面的 css 代码来指定 ace 字体的大小

```
.aceCode {
  font-size: 14px !important;
}
```

使用插件：

```
"plugins": [
    "ace"
]
```

使用示例:

```
{%ace edit=true, lang='c_cpp'%} // This is a hello world program for C. #include <stdio.h>

int main(){ printf("Hello World!"); return 1; } {%endace%}
```

## Emphasize

> 为文字加上底色

[插件地址](https://plugins.gitbook.com/plugin/emphasize)

```
"plugins": [
    "emphasize"
]
```

使用示例:

````
This text is {% em %}highlighted !{% endem %}

This text is {% em %}highlighted with markdown!{% endem %}

This text is {% em type="green" %}highlighted in green!{% endem %}

This text is {% em type="red" %}highlighted in red!{% endem %}

This text is {% em color="#ff0000" %}highlighted with a custom color!{% endem %}
````



## KaTex

> 为了支持数学公式, 我们可以使用`KaTex`和`MathJax`插件, 官网上说`Katex`速度要快于`MathJax`

[插件地址](https://plugins.gitbook.com/plugin/katex)
[MathJax使用LaTeX语法编写数学公式教程](http://iori.sinaapp.com/17.html)

```
"plugins": [
    "katex"
]
```

使用示例:
```
When {% math %}a \ne 0{% endmath %}, there are two solutions to {% math %}(ax^2 + bx + c = 0){% endmath %} and they are {% math %}x = {-b \pm \sqrt{b^2-4ac} \over 2a}.{% endmath %}

$$ \int_{-\infty}^\infty g(x) dx $$

$$ 1 \over 3 $$
```


## Include Codeblock

使用代码块的格式显示所包含文件的内容. 该文件必须存在。插件提供了一些配置，可以区插件官网查看。如果同时使用 ace 和本插件，本插件要在 ace 插件前面加载。

[插件地址](https://plugins.gitbook.com/plugin/include-codeblock)

```
{
    "plugins": [
        "include-codeblock"
    ],
    "pluginsConfig": {
        "include-codeblock": {
            "template": "ace",
            "unindent": "true",
            "theme": "monokai"
        }
    }
}
```

```
## Splitter

使侧边栏的宽度可以自由调节

![gitbook-splitter-demo](gitbook-splitter-demo.gif)

[插件地址](https://plugins.gitbook.com/plugin/splitter)

```
"plugins": [
    "splitter"
]
```

## Mermaid

> 支持渲染[Mermaid](https://github.com/knsv/mermaid)图表

[插件地址](https://plugins.gitbook.com/plugin/mermaid)

```
"plugins": [
    "mermaid"
]
```

## Sharing

sharing-plus: `npm install gitbook-plugin-sharing-plus@0.0.2`

> 分享当前页面, gitbook的默认插件, 使用下面方式来禁用

```
 plugins: ["-sharing"]
```

配置:

```
"pluginsConfig": {
    "sharing": {
        "weibo": true,
        "facebook": true,
        "twitter": true,
        "google": false,
        "instapaper": false,
        "vk": false,
        "all": [
            "facebook", "google", "twitter",
                "weibo", "instapaper"
        ]
    }
}
```

## Tbfed-pagefooter

> 为页面添加页脚

[插件地址](https://plugins.gitbook.com/plugin/tbfed-pagefooter)

```
"plugins": [
   "tbfed-pagefooter"
],
"pluginsConfig": {
    "tbfed-pagefooter": {
        "copyright":"Copyright &copy zhangjikai.com 2017",
        "modify_label": "该文件修订时间：",
        "modify_format": "YYYY-MM-DD HH:mm:ss"
    }
}
```

## Expandable-chapters-small

> 使左侧的章节目录可以折叠

[插件地址](https://plugins.gitbook.com/plugin/expandable-chapters-small)

```
plugins: ["expandable-chapters-small"]
```

## Sectionx

> 将页面分块显示，标签的 tag 最好是使用 b 标签，如果使用 h1-h6 可能会和其他插件冲突。

[插件地址](https://plugins.gitbook.com/plugin/sectionx)

```
{
    "plugins": [
       "sectionx"
   ],
    "pluginsConfig": {
        "sectionx": {
          "tag": "b"
        }
      }
}
```

使用示例
```
Insert markdown content here (you should start with h3 if you use heading).
```

## GA

> Google 统计

[插件地址](https://plugins.gitbook.com/plugin/ga)

```
"plugins": [
    "ga"
 ],
"pluginsConfig": {
    "ga": {
        "token": "UA-XXXX-Y"
    }
}
```

## 3-ba

> 百度统计

[插件地址](https://plugins.gitbook.com/plugin/3-ba)

```
{
    "plugins": ["3-ba"],
    "pluginsConfig": {
        "3-ba": {
            "token": "xxxxxxxx"
        }
    }
}
```

## Donate

> 打赏插件

[插件地址](https://plugins.gitbook.com/plugin/donate)

```
"plugins": [
    "donate"
],
"pluginsConfig": {
    "donate": {
        "wechat": "https://zhangjikai.com/resource/weixin.png",
        "alipay": "https://zhangjikai.com/resource/alipay.png",
        "title": "",
        "button": "赏",
        "alipayText": "支付宝打赏",
        "wechatText": "微信打赏"
    }
}
```

## Local Video

> 使用Video.js 播放本地视频

[插件地址](https://plugins.gitbook.com/plugin/local-video)

```
"plugins": [ "local-video" ]
```

使用示例：为了使视频可以自适应，我们指定视频的`width`为100%，并设置宽高比为`16:9`，如下面所示

```
{% raw %}
<video id="my-video" class="video-js" controls preload="auto" width="100%"
poster="https://zhangjikai.com/resource/poster.jpg" data-setup='{"aspectRatio":"16:9"}'>
  <source src="https://zhangjikai.com/resource/demo.mp4" type='video/mp4' >
  <p class="vjs-no-js">
    To view this video please enable JavaScript, and consider upgrading to a web browser that
    <a href="http://videojs.com/html5-video-support/" target="_blank">supports HTML5 video</a>
  </p>
</video>
{% endraw %}

```

另外我们还要再配置下css，即在website.css中加入

```
.video-js {
    width:100%;
    height: 100%;
}
```

````
{% raw %}

To view this video please enable JavaScript, and consider upgrading to a web browser that supports HTML5 video

{% endraw %}
````



## Simple-page-toc

> 自动生成本页的目录结构。另外 GitBook 在处理重复的标题时有些问题，所以尽量不适用重复的标题。

 [插件地址](https://plugins.gitbook.com/plugin/simple-page-toc)

```
{
    "plugins" : [
        "simple-page-toc"
    ],
    "pluginsConfig": {
        "simple-page-toc": {
            "maxDepth": 3,
            "skipFirstH1": true
        }
    }
}
```

使用方法: 在需要生成目录的地方加上` <!-- toc -->`

## Anchors

> 添加 Github 风格的锚点样式

[插件地址](https://plugins.gitbook.com/plugin/anchors)

```
"plugins" : [ "anchors" ]
```

## Anchor-navigation-ex

添加Toc到侧边悬浮导航以及回到顶部按钮。需要注意以下两点：

- 本插件只会提取 h[1-3] 标签作为悬浮导航
- 只有按照以下顺序嵌套才会被提取

```
# h1
## h2
### h3
必须要以 h1 开始，直接写 h2 不会被提取
## h2
```

[插件地址](https://plugins.gitbook.com/plugin/anchor-navigation-ex)

```
{
    "plugins": [
        "anchor-navigation-ex"
    ],
    "pluginsConfig": {
        "anchor-navigation-ex": {
            "isRewritePageTitle": true,
            "isShowTocTitleIcon": true,
            "tocLevel1Icon": "fa fa-hand-o-right",
            "tocLevel2Icon": "fa fa-hand-o-right",
            "tocLevel3Icon": "fa fa-hand-o-right"
        }
    }
}
```

## Edit Link

> 如果将 GitBook 的源文件保存到github或者其他的仓库上，使用该插件可以链接到当前页的源文件上。

[插件地址](https://plugins.gitbook.com/plugin/edit-link)

```
"plugins": ["edit-link"],
"pluginsConfig": {
    "edit-link": {
        "base": "https://github.com/USER/REPO/edit/BRANCH",
        "label": "Edit This Page"
    }
}
```

## Sitemap-general

> 生成sitemap

[插件地址](https://plugins.gitbook.com/plugin/sitemap-general)

```
{
    "plugins": ["sitemap-general"],
    "pluginsConfig": {
        "sitemap-general": {
            "prefix": "http://gitbook.zhangjikai.com"
        }
    }
}
```

## Favicon

> 更改网站的 favicon.ico

[插件地址](https://plugins.gitbook.com/plugin/favicon)

```
{
    "plugins": [
        "favicon"
    ],
    "pluginsConfig": {
        "favicon": {
            "shortcut": "assets/images/favicon.ico",
            "bookmark": "assets/images/favicon.ico",
            "appleTouch": "assets/images/apple-touch-icon.png",
            "appleTouchMore": {
                "120x120": "assets/images/apple-touch-icon-120x120.png",
                "180x180": "assets/images/apple-touch-icon-180x180.png"
            }
        }
    }
}
```



## Todo

> 添加 Todo 功能。默认的 checkbox 会向右偏移 2em，如果不希望偏移，可以在 `website.css` 里加上下面的代码:

```
input[type=checkbox]{
    margin-left: -2em;
}
```

[插件地址](https://plugins.gitbook.com/plugin/todo)

```
"plugins": ["todo"]
```

使用示例：

-  write some articles
-  drink a cup of tea
