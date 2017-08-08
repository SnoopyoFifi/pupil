# 同步静态网站代码到分支

1. 切换出master分支目录。我们需要将`gh-pages`分支内容存放在另外一个目录中；
2. 克隆`gh-pages`分支： `git clone -b gh-pages 仓库地址 book-end` ；这步我们只是克隆了`gh-pages`分支，并存放在一个新的目录`book-end` ；
3. copy静态网站（_book中的所有内容，注意配置`.gitignore`）到`book-end`目录中； 
4. push到仓库:`cd book-end`->`git rm README.md`-> `git pull` ->`git commit -m 'modify'`->`git push` ；
5. 提交`gh-pages`分支的修改；
6. copy源文件到`master`分支， 配置`.gitignore`注意添加`book-end`， 提交`master`主分支的修改。

以后每次修改只要将修改内容copy到`book-end`中即可。
