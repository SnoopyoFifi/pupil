# 生成gitpages

## github创建新的仓库与分支

1. 登陆到Github，创建一个新的仓库，名称我们就命名为snoopy-book，这样我就得到一个snoopy-book仓库。
2. 克隆仓库到本地： git clone 仓库地址
3. 创建一个新分支： git checkout -b gh-pages，注意，分支名必须为gh-pages。
4. 将分支push到仓库： git push -u origin gh-pages。
5. 切换到主分支：git checkout master。

## 同步静态网站代码到分支

1. 切换出master分支目录。我们需要将`gh-pages`分支内容存放在另外一个目录中；
2. 克隆`gh-pages`分支： `git clone -b gh-pages 仓库地址 book-end` ；这步我们只是克隆了`gh-pages`分支，并存放在一个新的目录`book-end` ；
3. copy静态网站（_book中的所有内容，注意配置`.gitignore`）到`book-end`目录中； 
4. push到仓库:`cd book-end`->`git rm README.md`-> `git pull` ->`git commit -m 'modify'`->`git push` ；
5. 提交`gh-pages`分支的修改；
6. copy源文件到`master`分支， 配置`.gitignore`注意添加`book-end`， 提交`master`主分支的修改。

以后每次修改只要将修改内容copy到`book-end`中即可。
