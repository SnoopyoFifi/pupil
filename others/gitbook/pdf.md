# 生成pdf

> 输出pdf文件步骤如下:

1. 由于生成PDF文件依赖于`ebook-convert`，故首先在该处[ebook-convert下载链接](http://calibre-ebook.com/download)点击下载所需要的版本，安装即可。以及[phantomjs](http://phantomjs.org/download.html)解压缩。
2. 并将二者目录添加至系统变量中。
3. 打开上述软件，在`gitbook`根目录中打开`cmd` ，使用命令 `gitbook pdf ./pdf名称` 。