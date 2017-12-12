# Git

## Git安装

- Window安装
  + [win下git安装](http://git-scm.com/download/win)

- Linux安装
  + CentOS发行版：`sudo yum install git`

  + Ubuntu发行版：`sudo apt-get install git`

- Mac安装

  + 打开Terminal直接输入git命令，会自动提示，按提示引导安装即可。

## Git工作原理

- `Git`与其他版本控制工具的比较
  - 底层维护存储文件的系统不同
    - `SVN` 、`CVS` 底层采用的为增量式的文件系统，当文件变动发生提交时，该文件系统存储记录的是文件内容的差异信息；
    - `Git` 底层采用的为**文件快照** 的文件系统，文件快照保存整个文件内容，同时保存指向快照的索引链接；
    - 文件快照的文件系统，提高了`Git` 分支的使用效率，`Git` 分支本质上是一个指向索引对象的可变指针，而每一个索引对象又指向文件快照。相对于`SVN` 、`CVS` 的分支，`Git` 创建分支是瞬间完成的，而无需将源代码做完整拷贝。
  - `Git` 版本控制系统的设计思想是"去中心化"
    - 传统的 `CVS`、`SVN` 等工具采用的是 `C/S` 架构，只有一个中心代码仓库，位于服务器端。一旦由于服务器系统宕机、网络不通等各种原因造成中心仓库不可用，整个 `CVS` 、`SVN` 系统的代码检入与检出就瘫痪了；
    - 为了摆脱对中心仓库的依赖，`Git` 的初始设计目标之一就是分布式控制管理。`Git` 分布式设计是支持离线工作的，在网络不通的情况下，照样可以频繁地提交代码，只不过先提交到本地仓库，等到了网络连通，再上传到远程的镜像仓库。

- Git管理文件的4种状态
  + <u>未追踪</u>（untracked）
  + <u>已提交</u>（committed）
  + <u>已修改</u>（modified）
  + <u>已暂存</u>（staged）

- Git项目的3个工作区域
  - **工作目录** (Working Directory): 工作目录是对项目的某个版本独立提取出来的内容。这些从Git仓库的压缩数据库中提取出来的文件，即操作系统中看到的文件夹。
  - **Git 仓库** (版本库、Repository): `.git`目录是Git用来保存项目的元数据和对象数据库的地方。这是Git 中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。**版本库可理解为文件仓库。由Git管理每个文件的新增、修改及删除，但这个仓库可以追溯历史。可还原至任意历史节点。**
  - **暂存区域** : 在`.git` 目录中，重要的就是称为Stage（或者叫Index）的暂存区，还有**`Git` 为我们自动创建的第一个分支`master` ,以及指向`master` 的一个指针叫 `HEAD`**。 暂存区域就是一个文件，保存了下次将提交的文件列表信息。

![image021](./images/git-stage.png)

- Git项目的2个仓库
  + **Git本地仓库** : Git本地仓库指的是开发者计算机中的仓库。
  + **[Git远程仓库](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)** : Git远程仓库是指托管在网络上的项目仓库。

- 基本的Git工作流程如下
  + 在工作目录中新增、删除、修改文件。
  + 暂存文件，将文件的快照放入暂存区域。
  + 提交文件，找到暂存区域的文件，将快照永久性存储到Git仓库目录。

##  Git基础

- 使用前配置

  - `git config`

    ```
    Git 自带一个 git config 的工具来帮助设置控制 Git 外观和行为的配置变量。
    ```

    变量存储在三个不同的位置: 

    - `/etc/gitconfig` 文件: 包含系统上每一个用户及他们仓库的通用配置。 如果使用带有 `--system` 选项的 `git config` 时，它会从此文件读写配置变量。
    - `~/.gitconfig` 或 `~/.config/git/config` 文件：只针对当前用户。 可以传递 `--global` 选项让 Git 读写此文件。
    - 当前使用仓库的 Git 目录中的 `config` 文件（就是 `.git/config`）：针对该仓库。

    > 想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有 `--global` 选项的命令来配置。

    ​	

  - 配置用户信息

    ```
    git config --global user.name "自已的名字"

    git config --global user.email "自已的邮箱地址"

    --global 配置当前用户所有仓库
    ```

  -  Git别名

    ```
    git config --global alias.co checkout

    git config --global alias.br branch

    git config --global alias.ci commit

    git config --global alias.st status
    ```

  - 检查配置信息

    ```
    // 列出所有 Git 当时能找到的配置
    git config --list

    // 来检查 Git 的某一项配置
    git config user.name
    ```

- `.gitignore` 忽略某些文件

  > 要养成一开始就设置好 `.gitignore` 文件的习惯，以免将来误提交这类无用的文件。

  ```
  # 此为注释 – 将被 Git 忽略
  # 忽略所有 .a 结尾的文件
  *.a
  # 但 lib.a 除外
  !lib.a
  # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
  /TODO
  # 忽略 build/ 目录下的所有文件
  build/
  # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
  doc/*.txt
  # ignore all .txt files in the doc/ directory
  doc/**/*.txt
  ```

  - 所有空行或者以注释符号 `＃` 开头的行都会被 Git 忽略。

  - 可以使用标准的 glob 模式(指 shell 所使用的简化了的正则表达式)匹配。
    - 星号（`*`）匹配零个或多个任意字符；
    - `[abc]`匹配任何一个列在方括号中的字符；
    - 问号（`?`）只匹配一个任意字符；
    - 如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 `[0-9]` 表示匹配所有 0 到 9 的数字）。

  - 匹配模式最后跟反斜杠（`/`）说明要忽略的是目录。

  - 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（`!`）取反。

    ​

- `Git` 的使用

  - 初始化仓库 `git init`

    ```
    git init
    ```

    > `git init`会在当前项目目录中创建一个名为`.git`的隐藏目录，这个目录包含了暂存区和仓库两个区域，有了这个隐藏目录就可以使用git来管理项目了，通过`ls -al`可以查看。

  - 本地仓库的操作

    - 查看文件状态 `git status`
      > 初始化仓库后便可以进行开发了，进入到刚刚创建好并初始为仓库的目录，添加我们开发需要的文件。
      >
      > 通过`git status`可以检测当前仓库文件的状态（未追踪untracked）。

    - 添加/删除文件 `git add <file>`

      - `git add -A`  暂存区与工作区保持一致
      - `git add . `    暂存区新建文件及更改文件
      - `git add -u`  暂存区删除文件及更改文件
      - `git rm  <file>`　 暂存区删除文件，可多个，空格分隔
      - `git rm --cached <file>`    会直接从暂存区删除文件，工作区则不做出改变
      - `git diff`    工作区与暂存区相比的差异

      **注意**：

      - `Git`会忽略空的目录，主流做法是在空文件夹里放置一个`.gitkeep`文件;
      - 所有的版本控制系统，只能跟踪文本文件的改动，比如`TXT`文件，网页，所有的程序代码等等，`Git`也不例外。版本控制系统可以告诉你每次的改动，如第N行文字删除、改动等。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，如图片改动，仅可知`100KB`改成了`120KB`。

    - 提交文件到分支  `git commit -m "<message>"`

      > 将暂存区的所有修改提交到分支，须输入描述信息

      - `git commit --amend`   更改之前一次提交的描述信息
      - **`git commit -a -m "<message>"`**   把暂存区的所有修改或者已删除的且已经被`git` 管理的文档提交到分支，须输入描述信息(可省略`git add` 过程)

    - 比较差异

      > 当内容被修改，我们无法确定修改哪些内容时，可以通过git diff来进行差异比较。

      - `git diff tool` 比较的是工作区和暂存的差异
      - `git diff tool "SHA"` 比较与特定提交的差异
      - `git diff tool "SHA" "SHA"` 比较某两次提交的差异
      - `git diff tool <branch name>` 比较与某个分支的差异
    
    - 撤销更改 `git checkout -- <file1> <file2> ...`

      > 将文件在工作区的修改全部撤销，可一次撤销多个文件的修改，用空格隔开。要想恢复刚撤销的更改 再次执行 `git checkout -- <file1>`

    - 版本穿梭 `git reset --hard <revision>`

      - 查看版本
        - `git log`  显示当前分支提交版本库的日志
        - `git reflog`  显示操作的日志，包含对应的版本号及信息，可查询到之前的版本号并再次回滚
      - 切换版本

        > 切换版本，即重置某一版本(强制，暂存区和工作区均重置)

        - `HEAD` 表示当前版本，也就是最新的提交，上一个版本为 `HEAD^` ， 上上一个版本为 `HEAD^^` ；
        - 要把当前版本回退到最新版本，使用 `git reset --hard` ；
        - 回滚到上一个版本， 使用 `git reset --hard HEAD^` , 此时， `git log` 就仅显示了当前版本及其之前的信息；
        - 也可输入版本号前七位，回滚到某个指定版本， 使用 `git reset --hard 8c38ca3`。
      - 小结
        - 每次`commit` 成功后，都会自动生成版本号，可根据版本号在版本库中任意切换版本；
        - `Git`的版本回退速度非常快，因为其内部有个指向当前版本的`HEAD`指针，当进行回退版本的时候，仅仅是将`HEAD`指针指向改变了。

  - 远程仓库的操作

    - 克隆远程仓库 `git clone <repository>`  

      > 通常`git`库都是已建立的，首先需将远程 `git`库的文件 clone 至本地。

    - 添加远程仓库

      > 如果先使用`git init` 添加了本地仓库，然后又想在`Github` 创建一个`Git`仓库，并且让这两个仓库进行远程同步，则需要添加本地仓库至远程仓库。

      - `git remote add <name> <url>`   添加远程仓库
        - 远程库的名字(`name`)默认为 `origin` 。
      - `git push -u origin master`  推送本地仓库至远程仓库
        - 上述命令实际上是将当前`master`分支推送到了远程；
        - 这样origin就代表` git@github.com:Botue/repo.git`， 当我们通过`git clone `从共享仓库获内容时，会自动帮我们添加`origin`到对应的仓库地址。
        - 由于远程仓库是空的，第一次推送`master`分支时，加上了`-u`参数, `Git`不但会把本地的`master`分支内容推送到远程新的`master`, 还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取是就可以简化命令(`git push`) 。

    - 从远程库获取

      - `git pull origin <branch name>` 从远程库获取最新版本并`merge` 到本地
      - `git fetch origin <branch name>`  从远程获取最新版本到本地，不会自动`merge`， 要加上这个`git merge origin/<branch name>` ，才相当于上面的命令

  - 分支管理

    > `Git`相对于其他版本控制工具，其一个突出的优点就是，分支的创建、查看、切换、删除等，以及分支的合并及冲突解决，都是及其迅速的。

    - 创建、查看、切换、合并、删除分支

      - `git branch` 查看分支
    
      - `git branch -a`  查看本地和远程所有分支
    
      - `git branch <branch name>` 创建分支
    
      - `git checkout <branch name>`  切换分支
    
      - `git chekcout -b <branch name>`  切换并创建分支
    
      - `git merge <branch name>`   合并指定分支到当前分支
    
      - `git branch -d <branch name>`  删除指定分支
    

    - 冲突解决

      - 冲突的产生

        > 比如在某个时间点，从`master`上分支出`foxfix`分支，`foxfix`分支上对文件做了更新，准备`merge`至`master`；如果`master`分支在该时间点后对文件`snoopy`做了更新并提交；此时，就可能产生冲突。

      - 解决冲突

        > Git用`<<<<<<< , ======= ,  >>>>>>>` 标记出不同分支的内容；
        >
        > 文件存在冲突，必须解决冲突后再提交；
        >
        > `git status`也可以告诉我们冲突的文件；
        >
        > 必须手动修改后保存并提交。

    - 远程分支

      > 远程分支的操作其实和本地大同小异，只是需要指向远程；
      >
      > 当你从远程仓库克隆时，实际上`Git`自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是`origin`。

      - `git remote`  显示远程库信息

      - `git remote -v ` 显示远程更详细信息

      - `git push origin dev`  推送远程其他分支，如：`dev`

      - `git pull origin dev`  获取远程分支，如：`dev`
      
      - `git push origin -d  <branch name>`  删除远程分支

      - 推送远程分支冲突解决

        > 远程分支`push`，可能会产生冲突，此时如何解决？其实同分支冲突解决雷同，只须多加一步，即首先 `pull` 最新的远程分支，再`merge`，若仍有冲突，则须手动解决冲突后再次 `push`即可。

    - 分支策略

      > 通常应用于团队的分支管理策略如下：

      - 首先， `master` 分支应该是非常稳定的，基本上仅用来发布新版本；
      - 其次，代码的`coding`都在`dev`分支上；
      - dev分支是不稳定的，到某个时候，比如2.0版本发布时，把`dev`分支合并到`master`上，在`master`分支发布2.0版本；
      - 然后，自然每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

## `Git`本地分支与远程分支详解

> github上已经有master分支 和dev分支

- 推送本地分支至远程

  - `git checkout -b dev` 新建并切换到本地dev分支

  - `git pull origin dev` 本地分支与远程分支相关联

1. 克隆代码
  - `git clone https://github.com/SnoopyoFifi/pupil.git`
  > 这个git路径是无效的，示例而已

2. 查看所有分支
  - `git branch --all`  
  > 默认只有master分支，所以会看到如下两个分支
  > master[本地主分支] origin/master[远程主分支]
  > 新克隆下来的代码默认master和origin/master是关联的，也就是他们的代码保持同步

3. 创建本地新的dev分支
  - `git branch dev`  创建本地分支
  
  - `git branch` 查看分支
  
  > 这是会看到master和dev，而且master上会有一个星号
  > 这个时候dev是一个本地分支，远程仓库不知道它的存在
  > 本地分支可以不同步到远程仓库，我们可以在dev开发，然后merge到master，使用master同步代码，当然也可以同步

4. 发布dev分支
  
  > 发布dev分支指的是同步dev分支的代码到远程服务器
  
  - `git push origin dev:dev`  
  
  > 这样远程仓库也有一个dev分支了

5. 在dev分支开发代码
  
  - `git checkout dev`  切换到dev分支进行开发
  
  > 开发代码之后，我们有两个选择
  
  - 第一个：如果功能开发完成了，可以合并主分支

    - git checkout master  # 切换到主分支
    - git merge dev  # 把dev分支的更改和master合并
    - git push  # 提交主分支代码远程
    - git checkout dev  # 切换到dev远程分支
    - git push  # 提交dev分支到远程
  
  - 第二个：如果功能没有完成，可以直接推送

    - git push  # 提交到dev远程分支

  > 注意：在分支切换之前最好先commit全部的改变，除非你真的知道自己在做什么

6. 删除分支

  - `git push origin :dev`   删除远程`dev`分支，危险命令哦

  > 下面两条是删除本地分支

    - `git checkout master`  切换到master分支
    
    - `git branch -d dev`  删除本地dev分

## 生成密钥

  - `ssh-keygen -t rsa `然后一路回车，这里会在当前用户生成了一个`.ssh`的文件夹

  ![image040](..\images\image040.png)

  - 将`id_rsa.pub`公钥的内容复制

  - 打开gitHub的个人中心

   ![image041](.\images\image041.png)

  - 打到SSHkeys

   ![image042](.\images\image042.png)


##  命令汇总

- git config配置本地仓库

> 常用git config --global user.name、git config --global user.email

- git config --list查看配置详情
- git init 初始一个仓库，添加--bare可以初始化一个共享（裸）仓库
- git status 可以查看当前仓库的状态
- git add “文件” 将工作区中的文件添加到暂存区中，其中file可是一个单独的文件，也可以是一个目录、“*”、-A
- git commit -m '备注信息' 将暂存区的文件，提交到本地仓库
- git log 可以查看本地仓库的提交历史
- git branch查看分支
- git branch “分支名称” 创建一个新的分支
- git checkout “分支名称” 切换分支
- git checkout -b deeveloper 创建并切到developer分支
- git merge“分支名称” 合并分支
- git branch -d “分支名称” 删除分支
- git clone “仓库地址”获取已有仓库的副本
- git push origin “本地分支名称:远程分支名称” 将本地分支推送至远程仓库，
- git push origin hotfix（通常的写法）相当于git push origin hotfix:hotfix
- git push origin hotfix:newfeature

> 本地仓库分支名称和远程仓库分支名称一样的情况下可以简写成一个，即git push “仓库地址” “分支名称”，如果远程仓库没有对应分支，将会自动创建

- git remote add “主机名称” “远程仓库地址” 添加远程主机，即给远程主机起个别名，方便使用
- git remote 可以查看已添加的远程主机
- git remote show “主机名称”可以查看远程主机的信息


## 补充

  - 免密提交、拉取
   > git pull push 不用输入用户名和密码的方法 免输密码
  
   1. 在计算机的安装盘下找到 '用户' 这个文件夹打开。

   2. 找到'用户' 文件夹下面有个和你计算机的名字一样的文件夹。

   3. 新建'.gitconfig' 文件

   4. 用编辑器打开新建文件，输入:
    
    [user]
      name = SnoopyoFifi
      email = wsmm1111@sina.cn
    [core]
      autocrlf = true
      excludesfile = C:\\Users\\admin\\Documents\\gitignore_global.txt
    [push]
      default = simple
    [alias]
      st = status
      co = checkout
      ci = commit
      br = branch
    [credential]
      helper = store

   5.保存后，随意打开一个项目，pull 或者 push 一次，下次就不需要输入密码了。


## 专题
- `git checkout`

  > `git checkout`有三个不同的作用：检出文件、检出提交和检出分支。

  > 检出提交会使工作目录和这个提交完全匹配。可用查看项目之前的状态，而不改变当前的状态。

  > 检出文件能够查看某个特定文件的旧版本，而工作目录剩下的文件不变。

  > 检出分支，创建分支和切换分支。

  - 查看之前的版本

    使用`git log --oneline`查看当前项目状态。首先，找到想要看的那个版本的 ID。

    ```
    git log --oneline
    ```

    假设你的项目历史看上去和下面一样：

    ```
    b7119f2 继续做些丧心病狂的事
    872fa7e 做些丧心病狂的事
    a1e8fb5 对 hello.py 做了一些修改
    435b61d 创建 hello.py
    9773e52 初始导入
    ```

    可以这样使用 `git checkout` 来查看对 `hello.py` 做了一些修改这个提交：

    ```
    git checkout a1e8fb5
    ```

    这让工作目录和 `a1e8fb5` 提交所处的状态完全一致。可以查看文件，编译项目，运行测试，甚至编辑文件而不需要考虑是否会影响项目的当前状态。所做的一切 *都不会* 被保存到仓库中。需要回到项目的当前状态：

    ```
    git checkout master
    ```

    一旦回到 `master`分支之后，你可以使用 `git revert` 或 `git reset` 来回滚任何不想要的更改。

  - 检出文件

    > 如果只对某个文件感兴趣，可以用 `git checkout` 来获取它的一个旧版本。比如说，如果只想从之前的提交中查看 `hello.py` 文件，可以使用下面的命令：

    ```
    git checkout a1e8fb5 hello.py
    ```

    记住，和检出提交不同，这里 *确实* 会影响项目的当前状态。旧的文件版本会显示为需要提交的更改，允许回滚到文件之前的版本。如果不想保留旧的版本，可以用下面的命令检出到最近的版本：

    ```
    git checkout HEAD hello.py
    ```

  - 检出分支
    ```
    # 创建新分支
    git branch hotfix
    # 切换到新分支
    git checkout hotfix

    # 上面命令等同
    git checkout -b hotfix
    ```

  
