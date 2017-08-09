# Hg

> hg  基本工作流程

- 克隆远程仓库或初始化本地仓库
- 本地修改
- 和远程仓库进行同步

> 简单的使用说明（以官方的实例仓库为栗子）

```js
  # 克隆远程仓库到本地
  hg clone http://qijun.xie:z6K66fQ=@192.168.2.220/hg_yun

  # 添加文件到版本库（一般是新增文件，没有进行版本跟踪过的）
  hg add hello.c

  # 提交一个修改到版本库
  hg commit -m "commit message"

  # 将本地修改同步到服务器
  hg push

  # 同步服务器的修改到本地
  hg pull && hg update
```

> hg 使用图解：

> hg 各种命令及其之间的联系

![command&relations](../images/800px-Mercurial_commandd_and_their_relations.png)

> hg 使用指导

![hg-tutorial](../images/hg_tutorial.jpg)



























