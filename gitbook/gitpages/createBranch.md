# github创建新的仓库与分支

1. 登陆到Github，创建一个新的仓库，名称我们就命名为`snoopy-book`，这样我就得到一个`snoopy-book`仓库。
2. 克隆仓库到本地： `git clone 仓库地址`
3. 创建一个新分支： `git checkout -b gh-pages`，注意，分支名必须为`gh-pages`。
4. 将分支push到仓库： `git push -u origin gh-pages`。
5. 切换到主分支：`git checkout master`。