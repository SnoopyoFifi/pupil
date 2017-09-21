# Hg-Git

## 分布式版本控制(DVCS)　
- DVCS

> 分布式版本控制 (DVCS) 是一种不需要中心服务器的管理文件版本的方法，但是它也可以使用中心服务器。更改可以被合并到 DVCS 的任何其他用户的系统中，因此可以实现非常灵活的工作流。

- DVCS 的两个主要优点是：
  - 它比集中的版本控制更灵活，因为它除了支持传统的（集中式）工作流，还支持其他各种工作流；
  - `Git` 分布式设计思想所带来的另外一大好处是支持离线工作。它比集中式服务器快得多，因为大多数操作在客户机本地进行，而不需要网络操作。

## [Hg 和 Git 命令对照](http://www.worldhello.net/2011/03/10/2370.html)

| 比较项目       | Hg 命令                                    | Git 命令                                   |
| ---------- | ---------------------------------------- | ---------------------------------------- |
|            | http://host/path/to/repos                | git://host/path/to/repos.git             |
| URL        | ssh://user@host/path/to/repos            | ssh://user@host/path/to/repos.git        |
|            | file:///path/to/repos                    | user@host​path/to/repos.git              |
|            | /path/to/repos                           | file:///path/to/repos.git                |
|            |                                          | /path/to/repos.git                       |
| 配置         | `[ui]username = Firstname Lastname <mail@addr>` | `[user]    name = Firstname Lastname    email = mail@addr` |
| 版本库初始化     | hg init <path>                           | git init [--bare] <path>                 |
| 版本库克隆      | hg clone <url> <path>                    | git clone <url> <path>                   |
| 获取版本库更新    | hg pull --update                         | git pull                                 |
| 更新至历史版本    | hg update -r <rev>                       | git checkout <commit>                    |
| 更新到指定日期    | hg update -d <date>                      | git checkout HEAD@'{<date>}'             |
| 更新至最新提交    | hg update                                | git checkout master                      |
| 切换至里程碑     | hg update -r <tag>                       | git checkout <tag>                       |
| 切换至分支      | hg update -r <branch>                    | git checkout <branch>                    |
| 还原文件/强制覆盖  | hg update -C <path>                      | git checkout -- <path>                   |
| 添加文件       | hg add <path>                            | git add <path>                           |
| 删除文件       | hg rm <path>                             | git rm <path>                            |
| 添加及删除文件    | hg addremove                             | git add -A                               |
| 移动文件       | hg mv <old> <new>                        | git mv <old> <new>                       |
| 撤消添加、删除等操作 | hg revert <path>                         | git reset -- <path>                      |
| 清除未跟踪文件    | hg clean                                 | git clean -fd                            |
| 获取文件历史版本   | hg cat -r<rev> <path> > <output>         | git show <commit>:<path> > <output>      |
| 反删除文件      | hg add <path>                            | git add <path>                           |
| 工作区差异比较    | hg diff                                  | git diff                                 |
|            |                                          | git diff --cached                        |
|            |                                          | git diff HEAD                            |
| 版本间差异比较    | hg diff -r <rev1> -r <rev2> <path>       | git diff <commit1> <commit2> -- <path>   |
| 查看工作区状态    | hg status                                | git status -s                            |
| 提交         | hg commit -m "<msg>"                     | git commit -a -m "<msg>"                 |
| 推送提交       | hg push                                  | git push                                 |
| 显示提交日志     | hg log \ less                           | git log                                  |
|            | hg glog \ less                          | git log --graph                          |
| 逐行追溯       | hg annotate                              | git annotate, git blame                  |
| 显示里程碑/分支   | hg tags                                  | git tag                                  |
|            | hg branches hg bookmarks                 | git branch                               |
|            | hg heads                                 | git show-ref                             |
| 创建里程碑      | hg tag [-m "<msg>"] [-r <rev>] <tagname> | git tag [-m "<msg>"] <tagname> [<commit>] |
| 删除里程碑      | hg tag --remove <tagname>                | git tag -d <tagname>                     |
| 创建分支       | hg branch <branch> hg bookmark <branch>  | git branch <branch> <commit>             |
|            |                                          | git checkout -b <branch> <commit>        |
| 删除分支       | hg commit --close-branch hg bookmark -d <branch> | git branch -d <branch>                   |
| 导出项目文件     | hg archive -r <rev> <output.tar.gz>      | git archive -o <output.tar> <commit>     |
|            |                                          | git archive -o <output.tar> --remote=<url> <commit> |
| 反转提交       | hg backout <rev>                         | git revert <commit>                      |
| 提交拣选       | -                                        | git cherry-pick <commit>                 |
| 分支合并       | hg merge <rev>                           | git merge <commit>                       |
| 变基         | hg rebase                                | git rebase                               |
| 冲突解决       | hg resolve --tool=<tool>                 | git mergetool                            |
|            | hg resolve -m <path>                     | git add <path>                           |
| 更改提交说明     | Hg + MQ                                  | git commit --amend                       |
| 撤消最后一次提交   | hg rollback                              | git reset [ --soft \ --hard ] HEAD^     |
| 撤消多次提交     | Hg + MQ                                  | git reset [ --soft \ --hard ] HEAD~<n>  |
| 撤消历史提交     | Hg + MQ                                  | git rebase -i <commit>^                  |
| 启动Web浏览    | hg serve                                 | git instaweb                             |
| 二分查找       | hg bisect                                | git bisect                               |
| 内容搜索       | hg grep                                  | git grep                                 |
| 提交导出补丁文件   | hg export                                | git format-patch                         |
| 工作区根目录     | hg root                                  | git rev-parse --show-toplevel            |
| 杂项         | .hgignore 文件                             | .gitignore 文件                            |
|            | pager 扩展                                 | 内置分页器                                    |
|            | color 扩展                                 | color.* 配置变量                             |
|            | mq 扩展                                    | StGit, Topgit                            |
|            | graphlog 扩展                              | git log --graph                          |
|            | hgk 扩展                                   | gitk                                     |
